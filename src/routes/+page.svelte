<script>
	import Nav from './nav.svelte';
	import axios from 'axios';

	let subreddit = '';

	const handleFormSubmit = (/** @type {{ detail: any; }} */ event) => {
		const subreddit = event.detail;

		axios
			.get('http://localhost:8000', { params: { subreddit, num_posts: 20 } })
			.then((response) => response.data)
			.then((data) => (links = data.links))
			.catch((err) => console.error(err.message));
	};

	/**
	 * @type {string[]}
	 */
	let links = [];
</script>

<Nav on:formSubmit={handleFormSubmit} />

{#if subreddit}
	<h2>Reddit images for {subreddit}</h2>
{/if}

<div class="container">
	{#each links as link, i}
		{#if i % 3 === 0}
			<div class="row">
				{#each links.slice(i, i + 3) as row_link}
					<div class="col-sm-4">
						<img class="img-fluid" src={row_link} alt="" />
					</div>
				{/each}
			</div>
		{/if}
	{/each}
</div>

<style>
	h2 {
		text-align: center;
	}
</style>
