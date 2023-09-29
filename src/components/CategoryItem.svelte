<script>
	import InventoryItem from '../components/InventoryItem.svelte';

	export let category;
	export let items;

	function removeComma(category) {
		return category.slice(0, -1); //TODO: Find a more elegant solution
	}
</script>

{#if items.length !== 0}
	<div class="category-item">
		<div class="category-title-container">
			<h2 class="category-title">{removeComma(category)}</h2>
			<div class="category-line" />
		</div>
		<ul class="category-items-container">
			{#each items as item}
				<InventoryItem {item} />
			{/each}
		</ul>
	</div>
{/if}

<style>
	.category-line {
		flex-grow: 1;
		border-bottom: #a2a2a2 solid 1px;
		height: 1.5rem;
		display: inline-block;
		transform: translateY(-50%);
	}
	.category-title-container {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		margin: 2rem 0 0.5rem 0;
	}

	.category-title {
		font-size: 1.5rem;
		padding-right: 1rem;
	}
</style>
