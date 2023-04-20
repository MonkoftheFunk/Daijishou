<script>
	export let item;
   export let baseUri;
   export let detail;
   let preview;
   if (detail && detail.wallpaperList && detail.wallpaperList.length) {
      for (let wallpaper of detail.wallpaperList) {
         if (wallpaper.filename != '') {
            preview = wallpaper.filename;
         }
      }
   }
</script>

<article>
	<h2><a href=#/theme/{item.platformWallpapersPackRootPath}>
       <img src="{baseUri}platform_wallpapers_packs/{item.platformWallpapersPackPreviewThumbnailPath}" alt="{item.platformWallpapersPackName}"/>
	{item.platformWallpapersPackName}</a></h2>
	<p>{item.platformWallpapersPackDescription}</p>
   <p class="meta">by {item.platformWallpapersPackAuthors}</p>
   {#if preview}
          <img src="{baseUri}platform_wallpapers_packs/{item.platformWallpapersPackRootPath}/{preview}" alt="<not found>"/>
   {/if}
</article>

<style>
	article {
		position: relative;
		padding: 0 0 0 2em;
		border-bottom: 1px solid #eee;
	}

	h2 {
		font-size: 1em;
		margin: 0.5em 0;
	}

	a {
		color: #333;
	}
	
	img {
		width: 64px;
	}
</style>
