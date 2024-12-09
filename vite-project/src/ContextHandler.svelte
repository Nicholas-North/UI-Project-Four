<script>
    // Base Imports
    import {onMount} from 'svelte';
    import {getContext} from 'svelte';
    import {setContext} from 'svelte';

    // Component Imports
    import Banner from './Components/Banner.svelte';
    import NavBar from './Components/NavBar.svelte';
    import Map from './Pages/Map.svelte';
    import Information from './Pages/Information.svelte';
    import Post from './Pages/Post.svelte';

    // Variable Declarations
    let ActiveContext = 'Map';
    let NavLinks = [
        {name: 'Map', label: 'Map'},
        {name: 'Information', label: 'Information'},
        {name: 'Post', label: 'Post'}
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
        {:else if ActiveContext === 'Information'}
            <Information />
        {:else if ActiveContext === 'Post'}
            <Post />
        {:else}
            <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
        {/if}
    </div>

</main>

<style>

</style>