<script lang="ts">
	import type { PageData } from './$types';
	import { removeEmptyElements } from '$helper';
	import Cover from '$components/elements/Cover.svelte';
	import Artist from '$components/elements/Artist.svelte';
	import Header from '$components/elements/Header.svelte';
	import List from '$components/elements/List.svelte';

	export let data: PageData;

	$: ({ artist, topTracks, albums, releatedArtists } = data);
</script>

<Header name={artist.name} genres={artist.genres} images={artist.images} />

<div class="wrapper">
	{#if removeEmptyElements(topTracks.tracks)?.length}
		<div class="container">
			<List title="Popular" tracks={removeEmptyElements(topTracks.tracks)} />
		</div>
	{/if}
	<div class="container">
		{#if removeEmptyElements(albums.items)?.length}
			<h1 class="title my-4">Albums</h1>
			<div class="wrapper-cover">
				{#each albums.items as album}
					<Cover {...album} />
				{/each}
			</div>
			<div class="flex justify-center mt-4">
				<a href="/artist/{artist.id}/albums" class="btn secondary" aria-label="Artist detail page">
					<span class="sr-only">show all</span>
					Show all albums
				</a>
			</div>
		{/if}
	</div>

	<div class="bg-primary-dark p-8 mt-8">
		<div class="container">
			<h1 class="title text-gray-light text-center">Releated Artists</h1>
			<div class="flex flex-wrap gap-4 sm:gap-7 place-content-center">
				{#each releatedArtists.artists as releatedArtist}
					<Artist {...releatedArtist} />
				{/each}
			</div>
		</div>
	</div>
</div>
