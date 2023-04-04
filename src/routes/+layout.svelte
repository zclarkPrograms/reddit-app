<!--<script>
	import Nav from './nav.svelte';

	const handleFormSubmit = (/** @type {{ detail: any; }} */ event) => {
		const subreddit = event.detail;

		console.log(subreddit);
	};
</script>
-->

<div class="app">
	<!--<Nav on:formSubmit={handleFormSubmit} />-->

	<main>
		<slot />
	</main>
</div>
