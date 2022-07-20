<script>
    // import {onMount, onDestroy, beforeUpdate, afterUpdate} from 'svelte';
    import { onMount } from "svelte";
    import Header from "../Components/Header.svelte";
    import Loader from "../Components/Loader.svelte";
    import Information from "../Components/Information.svelte";
    import { donasi } from "../data/donasi.js";
    import router from "page";

    export let params;
    let data,
        amount,
        name,
        email,
        aprove = false;
        
        // function getCharity(id){
            //     return donasi.find(function(char){
                //         return char.id === parseInt(id);
                //     })
                // }
                
                // ---------------------------------------
                // untuk mendapatkan data lengkap tiap id
    async function getCharity(id) {
        const res = await fetch(
            `https://charity-api-bwa.herokuapp.com/charities/${id}`
            );
            return res.json();
        }
        // untuk mendapatkan data yang dipilih sesuai id
        let datas = getCharity(params.id)
        // onMount(async () => {
            //     data = await getCharity(params.id);
            // });
            // ----------------------------------------
            

    // onMount(function(){
    //     setTimeout(() => {
    //         data = getCharity(params.id);
    //     }, 2500);
    // });

    // const interval = setInterval(() => {
    //     second += 1;
    //     console.log(second)
    // }, 1000);

    // onDestroy(function(){
    //     console.log('ondestroy');
    //     clearInterval(interval);
    // });

    // function handleButtonClick() {
    //     console.log("button");
    // }

    // mengirim data
    async function handleForm() {
        console.log(amount);
        data.pledged = data.pledged + parseInt(amount);
        try {
            const res = await fetch(
                `https://charity-api-bwa.herokuapp.com/charities/${params.id}`,
                {
                    method: "PUT",
                    headers: {
                        "content-type": "application/json",
                    },
                    body: JSON.stringify(data),
                }
            );
            console.log(res);
            router.redirect("/success");
        } catch (err) {
            console.log(err);
        }
    }
    // -------------------------
</script>

<!-- <style>
    #xs-input-checkbox{
        display: flex;
        align-items: center;
    }
    #xs-donate-agree{
        width: 35px;
    }
    label[for='xs-donate-agree']{
        margin: 0;
    }
</style> -->
<Header />
<!-- welcome section -->
<!--breadcumb start here-->
{#await datas}
<Loader/>
{:then charity}
    <section
        class="xs-banner-inner-section parallax-window"
        style="background-image:url('/assets/images/slide1.png')"
    >
        <div class="xs-black-overlay" />
        <div class="container">
            <div class="color-white xs-inner-banner-content">
                <h2>Donate Now</h2>
                <p>{charity.title}</p>
                <ul class="xs-breadcumb">
                    <li class="badge badge-pill badge-primary">
                        <a href="/" class="color-white">Home /</a> Donate
                    </li>
                </ul>
            </div>
        </div>
    </section>
    <!--breadcumb end here--><!-- End welcome section -->
    <main class="xs-main">
        <!-- donation form section -->
        <section class="xs-section-padding bg-gray">
            <div class="container">
                <div class="row">
                    <div class="col-lg-6">
                        <div class="xs-donation-form-images">
                            <img
                                src={charity.thumbnail}
                                class="img-responsive"
                                alt="Family Images"
                            />
                        </div>
                    </div>
                    <div class="col-lg-6">
                        <div class="xs-donation-form-wraper">
                            <div class="xs-heading xs-mb-30">
                                <h2 class="xs-title">{charity.title}</h2>
                                <p class="small">
                                    To learn more about make donate charity with
                                    us visit our "<span class="color-green"
                                        >Contact us</span
                                    >" site. By calling
                                    <span class="color-green"
                                        >+44(0) 800 883 8450</span
                                    >.
                                </p>
                                <span class="xs-separetor v2" />
                            </div>
                            <!-- .xs-heading end -->
                            <form
                                action="#"
                                method="post"
                                id="xs-donation-form"
                                class="xs-donation-form"
                                name="xs-donation-form"
                                on:submit|preventDefault={handleForm}
                            >
                                <div class="xs-input-group">
                                    <label for="xs-donate-name"
                                        >Donation Amount <span
                                            class="color-light-red">**</span
                                        ></label
                                    >
                                    <input
                                        type="text"
                                        name="name"
                                        id="xs-donate-name"
                                        class="form-control"
                                        placeholder="Minimum of $5"
                                        bind:value={amount}
                                    />
                                </div>
                                <!-- .xs-input-group END -->
                                <div class="xs-input-group">
                                    <label for="xs-donate-name"
                                        >Your Name
                                        <span class="color-light-red">**</span
                                        ></label
                                    >
                                    <input
                                        type="text"
                                        name="name"
                                        id="xs-donate-name"
                                        class="form-control"
                                        required="true"
                                        placeholder="Your Name"
                                        bind:value={name}
                                    />
                                </div>
                                <div class="xs-input-group">
                                    <label for="xs-donate-email"
                                        >Your Email
                                        <span class="color-light-red">**</span
                                        ></label
                                    >
                                    <input
                                        type="email"
                                        name="email"
                                        id="xs-donate-email"
                                        class="form-control"
                                        required="true"
                                        placeholder="hardiansyahrangga14@gmail.com"
                                        bind:value={email}
                                    />
                                </div>
                                <div
                                    class="xs-input-group"
                                    id="xs-input-checkbox"
                                >
                                    <input
                                        type="checkbox"
                                        name="agree"
                                        id="xs-donate-agree"
                                        bind:checked={aprove}
                                    />
                                    <label for="xs-donate-agree"
                                        >I Agree
                                        <span class="color-light-red">**</span
                                        ></label
                                    >
                                </div>
                                <!-- .xs-input-group END -->
                                <button type="submit" class="btn btn-warning" disabled={!aprove}
                                    ><span class="badge"
                                        ><i class="fa fa-heart" /></span
                                    > Donate now</button
                                >
                            </form>
                            <!-- .xs-donation-form #xs-donation-form END -->
                        </div>
                    </div>
                </div>
                <!-- .row end -->
            </div>
            <!-- .container end -->
        </section>
        <!-- End donation form section -->
    </main>
{/await}
<Information />
