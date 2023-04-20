<script>
   import { onMount } from 'svelte';
	import { beforeUpdate } from "svelte";
	import Summary from "./Summary.svelte";
	var baseUri = '../'; //https://monkofthefunk.github.io/Daijishou/themes/
   let details = [];
	let items;
   
    onMount(async () => {
   	fetch(`${baseUri}platform_wallpapers_packs/`)
   		.then(r => r.json())
   		.then(data => {
   			items = data.platformWallpapersPackList;
           for (let index = 0; index < items.length; index++) {
                 fetch(`${baseUri}platform_wallpapers_packs/${items[index].platformWallpapersPackRootPath}`)
                    .then(r => r.json())
                    .then(d => {
                       details[items[index].platformWallpapersPackRootPath] = d;
                    });
           }

   			window.scrollTo(0, 0);
   		});
    });
</script>

{#if items}
	{#each items as item}
		<Summary {item} {details} {baseUri} />
	{/each}
{:else}
	<p class="loading">loading...</p>
{/if}

<style>

	.loading {
		opacity: 0;
		animation: 0.4s 0.8s forwards fade-in;
	}

	@keyframes fade-in {
		from { opacity: 0; }
		to { opacity: 1; }
	}
</style>