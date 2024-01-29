<script lang="ts">
	import '../app.scss';
	import type { LayoutData } from './$types';
	import SlectTheme from '$components/layout/Theme.svelte';
	import NativePlayer from '$components/player/NativePlayer.svelte';
	import { setContext } from 'svelte';
	import { writable } from 'svelte/store';
	export let data: LayoutData;

	/**
	 * Store user
	 * Doc: https://kit.svelte.dev/docs/state-management#using-stores-with-context
	 */
	// Create a store and update it when necessary...
	const user = writable();
	$: user.set(data?.user || {});
	// ...and add it to the context for child components to access
	setContext('user', user);
</script>

<div class="flex flex-col h-screen">
	<div class="py-5 bg-gray-light dark:bg-gray-dark fixed inset-x-0 z-50">
		<div class="container flex items-center justify-between">
			<a
				href="/"
				class="text-2xl font-extrabold tracking-tight ring-2 px-2 py-1 ring-black dark:ring-primary hover:ring-primary"
				>MUSIC</a
			>
			<div class="flex items-center space-x-4 sm:space-x-6">
				<a href="/search" aria-label="Music Search"><i class="gg-search" /></a>
				<SlectTheme />
			</div>
		</div>
	</div>
	<div class="flex-grow mt-20"><slot /></div>
	<br>
	<br>
	<div class="bg-primary-dark text-gray-light space-y-2" >
		<div class="container sm:flex text-center sm:text-left justify-between pb-8 pt-4">
			<div class="text-sm">
				<a href="https://kit.svelte.dev/" target="_blank" class="text-primary-light font-semibold"
					>SvelteKit</a
				>
				MUSIC app by
				<a
					target="_blank"
					class="text-primary-light font-semibold">Gabby, Alberti and Zucca</a
				>
			</div>
		</div>
	</div>
</div>
<div class="fixed z-20 bottom-0 inset-x-0">
	<NativePlayer />
</div>
