<script context="module">
	export async function preload(page, session) {
		const data = await this.fetch("https://jsonplaceholder.typicode.com/users");
		const users = await data.json();
		return { users };
	}
</script>

<script>
	import Item from "../components/Item.svelte";
	import Search from "../components/search.svelte";

	export let users;

	// test nested object in object
	if (users.length)
		users[0].address.foo = {
			bar: { brr: "test nested" },
		};

	let search = "";
	let fieldsForSearch = ["name", "id", "email"];

	$: usersBySearch = search
		? users.filter((el) =>
				fieldsForSearch.some((field) =>
					el[field].toString().toLowerCase().includes(search.toLowerCase())
				)
		  )
		: users;

	function handleSearch(e) {
		search = e.detail.target.value;
	}
</script>

<svelte:head>
	<title>Sapper project template</title>
</svelte:head>

<h1 class="text-6xl mb-10">List from API</h1>
<Search {search} on:search={handleSearch} />
{#if usersBySearch.length}
	<ul class="list-none   mb-3">
		{#each usersBySearch as user (user.id)}
			<li class="p-3 my-5 rounded-md bg-green-100">
				<Item {user} />
			</li>
		{/each}
	</ul>
{:else}
	<div class="text-3xl">No users</div>
{/if}
