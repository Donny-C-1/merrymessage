<script>
    import { page } from "$app/state";

    let name = $state("");
    let message = $state("");
    let link = $state("");

    function onsubmit(e) {
        e.preventDefault();

        link = new URL("/message", page.url.href);
        let payload = btoa(JSON.stringify({ name, message }));

        link.searchParams.set("p", payload);
    }
</script>

<main>
    <h1>Welcome to MerryMessage</h1>
    <p>Create a christmas message to your loved ones</p>
    
    <form action="post" {onsubmit}>
        <label for="name">Receiver's Name</label>
        <input type="text" id="name" name="name" bind:value={name} />
        <label for="message">Message:  </label>
        <textarea name="message" id="message" bind:value={message}></textarea>
        <button>Generate link</button>
    </form>

    <div>
        <p>The link is: {link}</p>
    </div>
</main>