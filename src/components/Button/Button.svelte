<script lang="ts">
	export let type: string = 'button';
	export let href: string | null = null;
	export let variant: 'success' | 'outline' | 'success outline' | 'rounded' | '' = '';
	export let disabled: boolean = false;
	export let loading: boolean = false;
	export let title: string | null = null;
</script>

{#if href}
	<a {title} {href} class={variant}><slot /></a>
{:else}
	<button {title} {type} class={variant} disabled={loading || disabled} on:click>
		{#if loading}
			loading...
		{:else}
			<slot />
		{/if}
	</button>
{/if}

<style>
	button,
	a {
		transition: all 0.3s;
		font: inherit;
		border: 1px solid #cf0056;
		background: #cf0056;
		padding: 0.5rem 1rem;
		color: white;
		border-radius: 5px;
		box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.26);
		cursor: pointer;
		text-decoration: none;
	}

	button:focus {
		outline: none;
	}

	button:hover,
	button:active,
	a:hover,
	a:active {
		background: #e40763;
		border-color: #e40763;
		box-shadow: 1px 1px 8px rgba(77, 51, 51, 0.26);
	}

	button:disabled,
	button:disabled:hover,
	button:disabled:active {
		background: #ccc;
		border-color: #ccc;
		color: #959595;
		box-shadow: none;
		cursor: not-allowed;
	}

	.success {
		background: #01a129;
		border-color: #01a129;
	}

	.success:hover,
	.success:active {
		background: #1ac745;
		border-color: #1ac745;
	}

	.outline {
		background: transparent;
		color: #cf0056;
		box-shadow: none;
	}

	.outline:hover,
	.outline:active {
		background: #ffc7de;
		box-shadow: none;
	}

	.outline:disabled,
	.outline:disabled:hover,
	.outline:disabled:active {
		background: transparent;
		color: #ccc;
	}

	.outline.success {
		border-color: #01a129;
		color: #01a129;
	}

	.outline.success:hover,
	.outline.success:active {
		background: #c2ffd1;
	}

	.rounded {
		color: white !important;
		text-decoration: none !important;
		border-radius: 50%;
		height: 42px;
		width: 42px;
		display: flex;
		align-items: center;
		justify-content: center;
		padding: 0;
		font-size: 1.375rem;
	}
</style>
