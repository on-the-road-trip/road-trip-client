<script lang="ts">
	import { onDestroy } from 'svelte';
	import type { Status } from '$typings/common';
	import { portal } from '$utils/portal';

	export let open: boolean = true;
	export let severity: Status | null = null;
	export let message: string = '';
	let timeout: NodeJS.Timeout;

	$: {
		if (open) {
			timeout = setTimeout(() => {
				message = '';
				severity = null;
			}, 4000);
		} else clearTimeout(timeout);
	}

	onDestroy(() => clearTimeout(timeout));
</script>

<div use:portal={'#overlay'}>
	<figure class:open class={severity}>
		<span class="material-icons">{severity !== 'success' ? severity : 'check_circle'}</span>
		{message}
	</figure>
</div>

<style>
	figure {
		bottom: 1rem;
		transition: all 0.3s;
		border-radius: 8px;
		transform: translateY(200%);
		display: flex;
		align-items: center;
		margin: 0 1rem;
		position: fixed;
		margin: 0 1rem;
		padding: 1rem;
		z-index: 1000;
	}
	.open {
		display: flex;
		transform: translateY(0);
	}

	@media (min-width: 500px) {
		figure.open {
			margin-left: 1rem;
		}
	}

	.material-icons {
		margin-right: 5px;
	}

	.error {
		background: red;
		color: white;
		border-color: transparent;
	}

	.success {
		background: green;
		color: white;
		border-color: transparent;
	}

	.info {
		background: blue;
		color: white;
	}

	.warning {
		background: #ffcc00;
		color: white;
	}
</style>
