<script>
	export let message;
	export let type;
</script>

<p class={type}>
	{message}
</p>

<style>
	.success {
		color: #4caf50;
	}
	.error {
		color: #f44336;
	}

	.warning {
		color: #ff9800;
	}

	p {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 50vh;
		font-family: 'Staatliches', cursive;
		font-size: 1.5rem;
	}
</style>
