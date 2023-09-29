<script>
	import { onMount } from 'svelte';
	import MenuHeader from '../components/MenuHeader.svelte';
	import SearchBox from '../components/SearchBox.svelte';
	import Loading from '../components/Loading.svelte';
	import CategoryItem from '../components/CategoryItem.svelte';
	import InfoMessage from '../components/InfoMessage.svelte';
	import CategoryButton from '../components/CategoryButton.svelte';
	const BASE_URL = 'http://127.0.0.1:8393/api';
	let inventory = undefined;
	let categories = [];
	let searchQuery = '';
	let selectedCategory = 'all';
	const messageTypes = {
		ERROR: 'error',
		INFO: 'info',
		SUCCESS: 'success',
		WARNING: 'warning'
	};

	onMount(async () => {
		await getItems(searchQuery);
		categories = await apiGet('/categories');
	});

	async function getItems(searchQuery, selectedCategory = 'all') {
		const res = await apiGet(
			`/inventory?pageSize=1000&search=${searchQuery}&category=${selectedCategory}`
		);
		inventory = res.items;
	}
	async function apiGet(endpoint, bearerToken = null) {
		const requestOptions = {
			method: 'GET',
			headers: {
				'Content-Type': 'application/json',
				Authorization: `Bearer ${bearerToken}`
			}
		};
		const response = await fetch(`${BASE_URL}${endpoint}`, requestOptions);
		return await response.json();
	}

	function getCategoryItems(inventory, category) {
		return inventory.filter((item) => item.category === category);
	}
	async function searchEventHandler(e) {
		await getItems(e.detail.search, selectedCategory);
	}
	async function categoryEventHandler(e) {
		if (e.detail.category === selectedCategory) {
			selectedCategory = 'all';
		} else {
			selectedCategory = e.detail.category;
		}

		await getItems(searchQuery, selectedCategory);
	}
</script>

<MenuHeader />
<SearchBox on:myEvent={searchEventHandler} />
<ol id="category-list">
	{#each categories as category}
		<CategoryButton
			on:handleCategorySelection={categoryEventHandler}
			{category}
			selected={category === selectedCategory}
		/>
	{/each}
</ol>
<div id="data">
	{#if inventory === undefined}
		<Loading />
	{:else if inventory.length === 0}
		<InfoMessage type={messageTypes.INFO} message="Sorry, dat hebben we helaas niet..." />
	{/if}
	<ol>
		{#each categories as category}
			<CategoryItem category="{category}," items={getCategoryItems(inventory, category)} />
		{/each}
	</ol>
</div>

<style>
	#data {
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		margin: 0;
	}
	#category-list {
		display: flex;
		flex-direction: row;
		gap: 1.5rem;
		overflow-x: scroll;
		margin: 0 0 2rem 0;
		-ms-overflow-style: none; /* IE and Edge */
		scrollbar-width: none; /* Firefox */
	}

	/* Hide scrollbar for Chrome, Safari and Opera */
	#category-list::-webkit-scrollbar {
		display: none;
	}
</style>
