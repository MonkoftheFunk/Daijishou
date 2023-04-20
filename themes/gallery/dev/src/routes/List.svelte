<script>
   import { onMount } from 'svelte';
	import { beforeUpdate } from "svelte";
	import Summary from "./Summary.svelte";
   
   let detail;
	let items;
   export let baseUri;
   async function load() {
      var buri = baseUri;
   	detail = await fetch(`${buri}platform_wallpapers_packs/index.json`)
   		.then(r => r.json())
   		.then(data => {
            let det;
   			items = data.platformWallpapersPackList;
           for (let index = 0; index < items.length; index++) {
                 det = fetch(buri + 'platform_wallpapers_packs/' + items[index].platformWallpapersPackRootPath + '/index.json')
                    .then(r => r.json())
                    .then(data => {
                       return data;
                    });
           }

   			return det;
   		});
    }
   onMount(load);
</script>

<svelte:window on:hashchange={load}/>

{#if items}
	{#each items as item}
		<Summary {item} {detail} {baseUri} />
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