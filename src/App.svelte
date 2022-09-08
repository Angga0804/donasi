<script>
	import router from 'page'
	import Index from "./Pages/Index.svelte"
	import About from "./Pages/About.svelte"
	import Contact from "./Pages/Contact.svelte"
	import Donation from "./Pages/Donation.svelte"
	import NotFound from "./Pages/NotFound.svelte"
	import Success from "./Pages/Success.svelte"
	import CobaLagi from './Pages/CobaLagi.svelte';


	let page, params;

	router('/', () => (page = Index));
	router('/about', () => (page = About));
	router('/contact', () => (page = Contact));
	router('/success', () => (page = Success));
	router('/cobalagi', () => (page = CobaLagi));
	// router('/donation', () => (page = Donation));

	router("/donation/:id", (ctx, next) => {
		params = ctx.params;
		next();
	}, () => (page = Donation));
	
	router('/*', ()=>(page = NotFound));

	router.start();
</script>

<svelte:component this={page} {params} />