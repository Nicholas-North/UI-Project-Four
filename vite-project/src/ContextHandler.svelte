<script>
    // Base Imports
    import {onMount} from 'svelte';
    import {getContext} from 'svelte';
    import {setContext} from 'svelte';

    // Component Imports
    import Banner from './Components/Banner.svelte';
    import NavBar from './Components/NavBar.svelte';
    import Map from './Pages/Map.svelte';

    // Variable Declarations
    let ActiveContext = 'Map';
    let NavLinks = [
        {name: 'Home', label: 'Home'},
        {name: 'Map', label: 'Map'},
        {name: 'Information', label: 'Information'}
    ]

    // Function Declarations
    function setActiveContext(context) {
        ActiveContext = context;
    }
    function getActiveContext() {
        return ActiveContext;
    }

    // Context Setting
    setContext('setActiveContext', setActiveContext);
    setContext('getActiveContext', getActiveContext);
</script>

<main>
    <Banner />
    <NavBar links={NavLinks} />
    <div class="content">
        {#if ActiveContext === 'Map'}
            <Map />
        {:else}
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        {/if}
    </div>

</main>

<style>

</style>