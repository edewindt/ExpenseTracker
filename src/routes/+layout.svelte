<script>
	import css from '$lib/app.css';
</script>

<main>
	<slot />
</main>

<style>
	main {
		display: flex;
		align-items: center;
		flex-direction: column;
		gap: 1.5rem;
	}
</style>
