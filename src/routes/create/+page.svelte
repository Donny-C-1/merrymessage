<script>
    import { page } from "$app/state";
    let name = $state("");
    let receiversName = $state("");
    let message = $state("");
    let link = $state();

    async function onsubmit(e) {
        e.preventDefault();

        let payload = btoa(encodeURIComponent(JSON.stringify({ name, receiversName, message })));
        link = new URL("./message", page.url.href);
        link.searchParams.set("p", payload);

        try {
            await navigator.clipboard.writeText(link);
            alert("Link copied to clipboard!");
        } catch (err) {
            alert("Error copying link.");
        }
    }
</script>

<main>
    <div class="hero">
        <h1>Create Your Festive Greeting Card 🎉</h1>
        <p>Fill in your details and generate a magical holiday message link!</p>

        <form {onsubmit}>
            <div class="input-group">
                <label for="name">Your Name</label>
                <input type="text" id="name" bind:value={name} placeholder="Your Name" required />
            </div>

            <div class="input-group">
                <label for="receiversName">Receiver's Name</label>
                <input type="text" id="receiversName" bind:value={receiversName} placeholder="Receiver's Name" required />
            </div>

            <div class="input-group">
                <label for="message">Your Message</label>
                <textarea id="message" rows="5" bind:value={message} placeholder="Write your heartfelt message..." required></textarea>
            </div>

            <div class="actions">
                {#if link}
                    <a class="preview" href={link.href} target="_blank">Preview Card</a>
                {/if}
                <button type="submit">Generate Link</button>
            </div>
        </form>

        <div class="sparkles">
            <span></span><span></span><span></span><span></span><span></span>
            <span></span><span></span><span></span><span></span><span></span>
        </div>
    </div>
</main>

<style>
main {
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(to bottom, #1f3b6e, #6a0dad, #fdd835); /* festive gradient */
    padding: 2rem;
    padding-bottom: 5rem;
    font-family: 'Quicksand', sans-serif;
    overflow: hidden;
}

.hero {
    background: rgba(255,255,255,0.1);
    padding: 2.5rem 2rem;
    border-radius: 24px;
    backdrop-filter: blur(12px);
    box-shadow: 0 15px 35px rgba(0,0,0,0.25);
    text-align: center;
    color: #fff;
    position: relative;
    width: 100%;
    max-width: 500px;
}

h1 {
    font-size: 2.5rem;
    margin-bottom: 0.75rem;
    font-weight: 700;
    text-shadow: 2px 2px 6px rgba(0,0,0,0.3);
}

p {
    font-size: 1.1rem;
    margin-bottom: 2rem;
    font-weight: 500;
}

.input-group {
    text-align: left;
    margin-bottom: 1.5rem;
}

label {
    display: block;
    margin-bottom: 0.25rem;
    font-weight: 600;
}

input, textarea {
    width: 100%;
    padding: 0.75rem 1rem;
    border-radius: 12px;
    border: 2px solid #fff;
    outline: none;
    font-size: 1rem;
    font-family: 'Quicksand', sans-serif;
    transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
    background: rgba(255,255,255,0.15);
    color: #fff;
    resize: vertical;
}

input::placeholder, textarea::placeholder {
    color: #ccc;
}

input:focus, textarea:focus {
    border-color: gold;
    transform: scale(1.02);
    box-shadow: 0 8px 20px rgba(255,215,0,0.5);
}

.actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 1rem;
}

button {
    background: linear-gradient(45deg, #ff4b1f, #ff9068);
    color: #fff;
    border: none;
    padding: 0.75rem 2rem;
    border-radius: 12px;
    font-size: 1rem;
    font-weight: 700;
    cursor: pointer;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
}

button:hover {
    transform: translateY(-3px);
    box-shadow: 0 12px 25px rgba(0,0,0,0.4);
}

.preview {
    background: rgba(255,255,255,0.2);
    padding: 0.75rem 1.5rem;
    border-radius: 12px;
    color: #fff;
    text-decoration: none;
    font-weight: 600;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.preview:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 20px rgba(255,255,255,0.3);
}

/* Sparkles animation */
.sparkles {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
}

.sparkles span {
    position: absolute;
    display: block;
    width: 6px;
    height: 6px;
    background: gold;
    border-radius: 50%;
    animation: sparkle 2s linear infinite;
    opacity: 0.8;
}

.sparkles span:nth-child(1) { left: 10%; animation-delay: 0s; }
.sparkles span:nth-child(2) { left: 25%; animation-delay: 0.3s; }
.sparkles span:nth-child(3) { left: 40%; animation-delay: 0.6s; }
.sparkles span:nth-child(4) { left: 55%; animation-delay: 0.9s; }
.sparkles span:nth-child(5) { left: 70%; animation-delay: 1.2s; }
.sparkles span:nth-child(6) { left: 85%; animation-delay: 1.5s; }
.sparkles span:nth-child(7) { left: 20%; animation-delay: 1.8s; }
.sparkles span:nth-child(8) { left: 35%; animation-delay: 2.1s; }
.sparkles span:nth-child(9) { left: 50%; animation-delay: 2.4s; }
.sparkles span:nth-child(10) { left: 65%; animation-delay: 2.7s; }

@keyframes sparkle {
    0% { transform: translateY(0) scale(0.2); opacity: 0.8; }
    50% { transform: translateY(-10px) scale(1.2); opacity: 1; }
    100% { transform: translateY(-50px) scale(0.5); opacity: 0; }
}

/* Responsive */
@media (max-width: 480px) {
    h1 { font-size: 2rem; }
    p { font-size: 1rem; }
    .actions { flex-direction: column; }
    button, .preview { width: 100%; text-align: center; }
}
</style>
