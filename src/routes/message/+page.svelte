<script>
    import { page } from "$app/state";
    import { onMount } from "svelte";

    let name = $state("");
    let message = $state("");

    onMount(() => {
        let payload = JSON.parse(decodeURIComponent(atob(page.url.searchParams.get("p"))));

        name = payload.name;
        message = payload.message;
    })
</script>

<main>
    <div class="card">
        <h1>Happy New Year {name}</h1>
        <p>{message}</p>
    </div>
</main>

<style>

    main {
        min-height: 100vh;
        background-color: pink;
    }
    .card {
        text-align: center;
        font-family: Quicksand;
        padding: 4rem 2rem;
    }
    h1 {
        font-size: 2rem;
    }

    p {
        font-weight: 500;
        font-size: 1.2rem;
        font-style: oblique;
        line-height: 2;
    }
</style>