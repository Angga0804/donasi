<script>
	import router from 'page'
	import Index from "./Pages/Index.svelte"
	import About from "./Pages/About.svelte"
	import Contact from "./Pages/Contact.svelte"
	import Donation from "./Pages/Donation.svelte"

	let page;

	router('/', () => (page = Index));
	router('/about', () => (page = About));
	router('/contact', () => (page = Contact));
	router('/donation', () => (page = Donation))

	router.start();
</script>

<svelte:component this={page} />