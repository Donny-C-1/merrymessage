<script>
    import { page } from "$app/state";
    import { onMount } from "svelte";

    let name = $state("");
    let receiversName = $state("");
    let message = $state("");
    let link = $state();

    onMount(() => $inspect(link))

    function onsubmit(e) {
        e.preventDefault();

        link = new URL("/message", page.url.href);
        let payload = btoa(JSON.stringify({ name, message }));

        link.searchParams.set("p", payload);
    }
</script>

<main>
    <h1>Create your greeting card</h1>
    <form action="" {onsubmit}>
        <div>
            <label for="name">Your Name:</label>
            <input type="text" name="name" id="name" bind:value={name} />
        </div>
        <div>
            <label for="name">Receiver's Name:</label>
            <input type="text" name="name" id="name" bind:value={receiversName} />
        </div>
        <label for="message">Your Message</label>
        <textarea name="message" id="message" bind:value={message}></textarea>
        <div>
            <a href={link}>Preview</a>
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