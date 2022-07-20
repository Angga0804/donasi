<script>
	import {onMount} from 'svelte'
	import DonasiList from "../Components/DonasiList.svelte";
	import Header from "../Components/Header.svelte";
	import Promo from "../Components/Promo.svelte";
	import Welcome from "../Components/Welcome.svelte";
	import Information from "../Components/Information.svelte";
	import Loader from '../Components/Loader.svelte';
    // import {donasi} from "../data/donasi.js"
	
	let title = "Charity"
	let data = getData();
	// let donasi = []

	async function getData(){
		const res = await fetch('https://charity-api-bwa.herokuapp.com/charities');
		const data = await res.json();
		if(res.ok){
			return data
		} else{
			throw new Error(data);
		}
	}

	
</script>

<!-- <div>
	<h1>{title}</h1>
</div> -->
<Header/>
<Welcome/>
{#await data}
<Loader/>
<!-- data menjadi donasi -->
{:then donasi}
<DonasiList {donasi}/>
{/await}
<Promo/>
<Information/>