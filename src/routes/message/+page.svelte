<script>
    import { page } from "$app/state";
    import { onMount } from "svelte";
    import { fade, scale } from "svelte/transition";

    let name = $state("");
    let receiversName = $state("");
    let message = $state("");
    let shareUrl = $state("");

    function combined(node) {
        const fadeTransition = fade(node, { duration: 500 });
        const scaleTransition = scale(node, { start: 0.95, duration: 500 });
        return {
            duration: 500,
            tick(t) {
                fadeTransition.tick(t);
                scaleTransition.tick(t);
            }
        };
    }

    onMount(() => {
        let payload = JSON.parse(
            decodeURIComponent(atob(page.url.searchParams.get("p")))
        );

        receiversName = payload.receiversName;
        name = payload.name;
        message = payload.message;

        const text = encodeURIComponent(
            `🎆 I made a New Year message for you!\n\nOpen it here 👉`
        );

        shareUrl = `https://wa.me/?text=${text}%20${encodeURIComponent(page.url.href)}`;
    });
</script>

<main>
    <div class="wrapper">
        <div class="card" in:combined>
            <div class="fireworks">
                <span></span><span></span><span></span><span></span>
            </div>

            <h1>🎆 Happy New Year, {receiversName}! 🎆</h1>
            <p class="message">{message}</p>
            <p class="from">— From: {name}</p>
        </div>

        <!-- Share Button -->
        <a
            class="share-btn"
            href={shareUrl}
            target="_blank"
            rel="noopener noreferrer"
        >
            Share on WhatsApp 💚
        </a>
    </div>
</main>

<style>
    main {
        min-height: 100vh;
        display: flex;
        justify-content: center;
        align-items: center;
        background: linear-gradient(to bottom, #0f2027, #203a43, #2c5364);
        padding: 2rem;
        font-family: 'Quicksand', sans-serif;
    }

    .wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1.5rem;
        width: 100%;
        max-width: 600px;
    }

    .card {
        position: relative;
        width: 100%;
        background: radial-gradient(circle at top left, #ffe29f, #ff7e5f);
        border-radius: 24px;
        padding: 3rem 2rem;
        box-shadow: 0 20px 40px rgba(0,0,0,0.25);
        text-align: center;
        color: #1a1a1a;
        overflow: hidden;
    }

    h1 {
        font-size: 2.5rem;
        margin-bottom: 1.5rem;
        font-weight: 700;
    }

    .message {
        font-size: 1.3rem;
        font-weight: 500;
        font-style: oblique;
        line-height: 1.8;
        margin-bottom: 2rem;
    }

    .from {
        font-size: 1.1rem;
        font-weight: 600;
        color: #333;
    }

    /* Share Button */
    .share-btn {
        background: linear-gradient(45deg, #25D366, #1ebe57);
        color: white;
        text-decoration: none;
        font-weight: 700;
        padding: 0.9rem 2rem;
        border-radius: 999px;
        font-size: 1.05rem;
        box-shadow: 0 10px 25px rgba(0,0,0,0.25);
        transition: transform 0.2s ease, box-shadow 0.2s ease;
    }

    .share-btn:hover {
        transform: translateY(-2px);
        box-shadow: 0 15px 30px rgba(0,0,0,0.35);
    }

    /* Fireworks */
    .fireworks {
        position: absolute;
        inset: 0;
        pointer-events: none;
    }

    .fireworks span {
        position: absolute;
        width: 6px;
        height: 6px;
        background: gold;
        border-radius: 50%;
        animation: burst 2s infinite ease-out;
        opacity: 0;
    }

    .fireworks span:nth-child(1) { left: 20%; animation-delay: 0s; }
    .fireworks span:nth-child(2) { left: 40%; animation-delay: 0.3s; }
    .fireworks span:nth-child(3) { left: 60%; animation-delay: 0.6s; }
    .fireworks span:nth-child(4) { left: 80%; animation-delay: 0.9s; }

    @keyframes burst {
        0% { transform: translateY(0) scale(0.2); opacity: 1; }
        50% { transform: translateY(-50px) scale(1.2); opacity: 0.8; }
        100% { transform: translateY(-100px) scale(0.5); opacity: 0; }
    }

    @media (max-width: 480px) {
        h1 { font-size: 2rem; }
        .message { font-size: 1.1rem; }
    }
</style>
