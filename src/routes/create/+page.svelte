<script>
    import { enhance } from "$app/forms";
    import { page } from "$app/state";

    let name = $state("");
    let receiversName = $state("");
    let message = $state("");
    let link = $state();

    async function onsubmit(e) {
        e.preventDefault();

        link = new URL("/message", page.url.href);

        let payload = btoa(encodeURIComponent(JSON.stringify({ name, message })));

        link.searchParams.set("p", payload);

        try {
            await navigator.clipboard.writeText(link);

            alert("Copied to clipboard");
        } catch (err) {
            alert("Error copying to clipboard");
        }
    }
</script>

<main>
    <h1>Create your greeting card</h1>
    <form action="" {onsubmit}>
        <div>
            <label for="name">Your Name:</label>
            <input type="text" name="name" id="name" bind:value={name} required />
        </div>
        <div>
            <label for="name">Receiver's Name:</label>
            <input type="text" name="name" id="name" bind:value={receiversName} required />
        </div>
        <label for="message">Your Message</label>
        <textarea name="message" id="message" rows="5" bind:value={message} required></textarea>
        <div>
            <a href={link?.href}>Preview</a>
            <button>Generate Link</button>
        </div>
    </form>
</main>

<style>
    h1 {
        text-align: center;
    }

    form {
        width: clamp(40rem, 90%, 10rem);
        margin-inline: auto;
        padding: 1rem;
        margin-bottom: 5rem;
    }

    input, textarea {
        display: block;
        margin-block: .25rem 1rem;
        width: 100%;
        padding: .5rem .5rem;
        border: 2px solid grey;
        border-radius: .25rem;
    }
</style>