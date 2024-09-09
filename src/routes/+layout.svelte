<script lang="ts">
	import Footer from '$lib/components/nav/footer.svelte';
	import Header from '$lib/components/nav/header.svelte';
	import '../app.css';
</script>

<div class="flex min-h-screen flex-col">
	<Header />
	<main class="flex flex-grow flex-col gap-4">
		<slot />
	</main>
	<Footer />
</div>
