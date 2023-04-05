<script lang="ts">
	import Nav from './nav.svelte';
	import axios from 'axios';

	let subreddit = '';

	const NUM_POSTS = 100;

	let finishedFetch = false;

	const handleFormSubmit = (event: CustomEvent) => {
		subreddit = event.detail;
		finishedFetch = false;

		axios
			.get('http://localhost:8000', { params: { subreddit, num_posts: NUM_POSTS } })
			.then((response) => response.data)
			.then((data) => {
				links = data.links;
				finishedFetch = true;
			})
			.catch((err) => console.error(err.message));
	};

	let links: string[] = [];

	const handleClick = (event: Event) => {
		const button = event.target as HTMLButtonElement;
	};
</script>

<Nav on:formSubmit={handleFormSubmit} />

{#if subreddit && finishedFetch}
	<h2 class="text-center">r/{subreddit}</h2>
{/if}

<div class="container-sm px-0">
	<div class="row gx-3">
		{#each links as link, i}
			<div class="col-sm-6 col-md-4 col-lg-3 mb-3">
				<button class="img-button" on:click={handleClick}>
					<img id={'' + i} class="img-fluid" src={link} alt="" />
				</button>
			</div>
		{/each}
	</div>
</div>

<style>
	.img-button {
		border: none;
		padding: 0;
	}

	.img-button,
	.img-fluid {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	@media (min-width: 800px) {
		.container-sm {
			max-width: 95%;
		}
	}

	@media (max-width: 800px) {
		.container-sm {
			max-width: 100%;
		}
	}
</style>
