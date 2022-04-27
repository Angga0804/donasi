<script>
	import DonasiList from "../Components/DonasiList.svelte";
	import Header from "../Components/Header.svelte";
	import Promo from "../Components/Promo.svelte";
	import Welcome from "../Components/Welcome.svelte";
	import Information from "../Components/Information.svelte";
    import {donasi} from "../data/donasi.js"
	
	let title = "Charity"
	
</script>

<!-- <div>
	<h1>{title}</h1>
</div> -->
<Header/>
<Welcome/>
<DonasiList {donasi}/>
<Promo/>
<Information/>