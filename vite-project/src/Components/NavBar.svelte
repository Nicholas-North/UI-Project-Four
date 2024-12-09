<script>
    import {getContext} from 'svelte';
    export let links = [];
    // Example Links
    // links = [
    //     {name: 'Default', label: 'Home'},
    //     ...
    // ];

    let currentContet = '';

    const setActiveContext = getContext('setActiveContext');
    const getActiveContext = getContext('getActiveContext');

    $: currentSection = getActiveContext();
</script>

<nav>
    <ul>
        {#each links as link}
            <li><a href={`#${link.name}`} on:click={() => setActiveContext(link.name)}>{link.label}</a></li>
        {/each}
    </ul>
</nav>
  
<style>
    :global(body) {
        margin: 0;
    }

    nav {
        width: 100%;
        background-color: #fff; /* White background */
        color: #6C584C;
        padding: 1rem; /* Adjust padding as needed */
        font-size: 22px;
        display: flex;
        justify-content: center; /* Center the navbar */
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Optional: adds a subtle shadow */
        position: fixed; /* Fix the navbar to the top */
        top: 60px; /* Adjust this value to match the height of the Banner */
        left: 0;
        z-index: 999; /* Ensure it stays on top of other content */
    }

    ul {
        list-style-type: none;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: left; /* Align items to the left */
        width: 100%; /* Make the ul take the full width */
    }

    li {
        margin: 0 5px; /* Add some spacing between the list items */
    }

    a {
        text-decoration: none;
        color: black; /* Adjust color as needed */
        padding: 5px 10px; /* Adjust padding to encapsulate the text */
        transition: background-color 0.3s; /* Smooth transition for hover effects */
        display: flex; /* Ensure the link takes the full height of the li */
        align-items: center;
        justify-content: center; /* Center text horizontally and vertically */
        height: 100%; /* Make the link take the full height of the li */
    }

    a:hover {
        background-color: #f0f0f0; /* Light background on hover */
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Slightly stronger shadow on hover */
    }
</style>