<script>
    import { page } from "$app/state";
    import { onMount } from "svelte";

    let name = $state("");
    let message = $state("");

    onMount(() => {
        let payload = JSON.parse(atob(page.url.searchParams.get("p")));

        name = payload.name;
        message = payload.message;
    })
</script>

<main>
    <h1>Hello {name}</h1>
    <p>{message}</p>
</main>