<script lang="ts">
	import { GOOGLE_API_KEY } from '$config/constants';
	import { onDestroy } from 'svelte';

	export let ready: boolean = false;
	let container: HTMLDivElement;
	export let map: google.maps.Map;
	let zoom = 5;
	let center = { lat: 39.809734, lng: -98.55562 };

	function onLoad() {
		ready = true;
	}

	$: if (ready && !map) {
		map = new google.maps.Map(container, {
			zoom,
			center
		});
	}

	onDestroy(() => {
		window.google = undefined;
	});
</script>

<svelte:head>
	<script
		defer
		async
		on:load={onLoad}
		src={`https://maps.googleapis.com/maps/api/js?key=${GOOGLE_API_KEY}&libraries=places,directions`}>
	</script>
</svelte:head>
<section>
	<div bind:this={container} id="map" />
	<slot name="overlay" />
</section>

<style>
	section {
		position: relative;
	}
	#map {
		width: 100vw;
		height: calc(100vh - 85px);
	}
</style>
