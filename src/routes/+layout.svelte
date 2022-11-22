<script>
	import '../app.postcss';
	import Header from './Header.svelte';
	import Footer from './Footer.svelte';
</script>

<div class="flex flex-col min-h-screen" data-theme="luxury">
	<Header />
	<main class="box-border flex flex-1 flex-col p-1 w-full max-w-5xl my-0 mx-auto">
		<slot />
	</main>
	<Footer />
</div>
