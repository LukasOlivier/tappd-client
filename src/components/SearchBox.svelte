<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	export let search = '';
</script>

<input
	type="text"
	bind:value={search}
	on:input={() =>
		dispatch('myEvent', {
			search: search
		})}
	placeholder="&#128269 Search for drinks / food"
/>

<style>
	input {
		flex-grow: 1;
		padding: 0.5rem;
		margin: 0 0 1rem 0;
		border: #686868 solid 1px;
		background: #f5f5f5;
		width: 100%;
	}
</style>
