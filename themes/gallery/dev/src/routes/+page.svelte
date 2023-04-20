<script>

	import { onMount } from 'svelte';
	import List from './List.svelte';
	import Item from './Item.svelte';

   let baseUri = 'https://raw.githubusercontent.com/TapiocaFox/Daijishou/main/themes/';
   let item;
	let id; 
	
	async function hashchange() {
		// the poor man's router!
		const path = window.location.hash.slice(1);

		if (path.startsWith('/theme')) {
			id = path.slice(6);
			item = await fetch(`${baseUri}platform_wallpapers_packs${id}/index.json`).then(r => r.json());

			window.scrollTo(0,0);
		} else if (path.startsWith('/')) {
			item = null;
			id = null;
		}
	}

	onMount(hashchange);
</script>

<svelte:window on:hashchange={hashchange}/>

<main>
	{#if item}
		<Item {id} {item} {baseUri} returnTo="#/"/>
	{:else }
		<List {baseUri} />
	{/if}
</main>

<style>
	main {
		position: relative;
		max-width: 800px;
		margin: 0 auto;
		min-height: 101vh;
		padding: 1em;
      color: white;
      background-color: rgb(24, 24, 24);
      font-family: "Overpass", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen, Ubuntu, Cantarell, "Fira Sans", "Droid Sans", "Helvetica Neue", sans-serif;
	}

	main :global(.meta) {
		color: #999;
		font-size: 12px;
		margin: 0 0 1em 0;
	}

	main :global(a) {
		color: fuchsia;
	}

   main :global(image) {
      max-width: 800px;
   }

   main :global(image.thumb) {
      max-width: 64px;
   }
   
</style>