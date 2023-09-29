<script>
	export let item;
</script>

<li class="slide-up item-container clickable">
	<p class="item-name">{item.name}</p>
	<p class="item-price">&#8364{item.price}</p>
</li>

<style>
	.item-container:hover {
		background: #e9e9e9;
	}
	.item-container {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		padding: 1.5rem 0;
	}
	.item-container:not(:last-child) {
		border-bottom: rgba(162, 162, 162, 0.43) solid 1px;
	}
</style>
