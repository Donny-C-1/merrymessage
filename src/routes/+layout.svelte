<script>
	import favicon from '$lib/assets/favicon.svg';
	import "$lib/styles/app.css";

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<div>
	{@render children()}
	<footer>&copy; {new Date().getFullYear()} | Made with 💜 by Donny C</footer>
</div>

<style>
	footer {
		position: fixed;
		bottom: 0;
		width: 100%;
		padding-block: 1rem;
		backdrop-filter: blur(20px);
		text-align: center;
		font-weight: 600;
	}
</style>