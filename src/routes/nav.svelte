<script lang="ts">
	import { createEventDispatcher } from 'svelte';

	export let subreddit: string = '';
	const dispatch = createEventDispatcher();
	const handleSubmit = (event: SubmitEvent) => {
		event.preventDefault();
		dispatch('formSubmit', subreddit);
	};
</script>

<nav class="navbar navbar-light bg-light justify-content-between">
	<h1>Reddit Images</h1>
	<form class="form-inline d-flex" on:submit={handleSubmit}>
		<input
			class="form-control"
			type="search"
			name="search"
			id="search"
			placeholder="Search"
			aria-label="Search"
			bind:value={subreddit}
		/>
		<button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
	</form>
</nav>

<style>
</style>
