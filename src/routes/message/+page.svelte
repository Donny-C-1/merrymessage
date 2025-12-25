<script>
    import { page } from "$app/state";
    import { onMount } from "svelte";

    let name = $state("");
    let message = $state("");

    onMount(() => {
        name = page.url.searchParams.get("name");
        message = page.url.searchParams.get("message");
    })
</script>

<main>
    <h1>Hello {name}</h1>
    <p>{message}</p>
</main>