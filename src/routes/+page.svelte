<script>
    let name = $state("");
    let message = $state("");
    function onsubmit(e) {
        e.preventDefault();

        alert(`Name: ${name} \n Message: ${message}`)
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
</main>