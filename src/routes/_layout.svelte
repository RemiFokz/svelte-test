<script>
	import Nav from "../components/Nav.svelte";

	export let segment;
</script>

<style>
	main {
		position: relative;
		max-width: 56em;
		background-color: white;
		padding: 2em;
		margin: 0 auto;
		box-sizing: border-box;
	}
</style>

<svelte:head>
	<link
		href="https://unpkg.com/tailwindcss@^1.0/dist/tailwind.min.css"
		rel="stylesheet" />
</svelte:head>
<Nav {segment} />

<main>
	<div class="container">
		<slot />
	</div>
</main>
