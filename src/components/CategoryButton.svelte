<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	export let category;
	export let selected;
</script>

<input
	type="button"
	bind:value={category}
	on:click={dispatch('handleCategorySelection', {
		category: category
	})}
	class:selected
/>

<style>
	.selected {
		background-color: #38a6ff;
		color: white;
	}

	input {
		padding: 0.2rem 0.5rem;
		border: none;
		font-family: 'Staatliches', cursive;
		background: #d9d9d9;
	}
</style>
