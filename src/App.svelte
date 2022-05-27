<script>
	import router from 'page'
	import Index from "./Pages/Index.svelte"
	import About from "./Pages/About.svelte"
	import Contact from "./Pages/Contact.svelte"

	let page;

	router('/', () => (page = Index));
	router('/about', () => (page = About));
	router('/contact', () => (page = Contact));

	router.start();
</script>

<svelte:component this={page} />