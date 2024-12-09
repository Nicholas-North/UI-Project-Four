<script>
    import {getContext, afterUpdate} from 'svelte';
    export let headers = [];
    export let data = [];
  
    let selectedFilter = headers[0];

    let filtered = getFilteredData();
    const getSelectedMarker = getContext('getSelectedMarker');
    const setSelectedMarker = getContext('setSelectedMarker');
    let selectedMarker = getSelectedMarker();
  
    // Function to filter and sort data
    function getFilteredData() {
        if (selectedFilter === 'All') {
        return data.sort((a, b) => new Date(b.posttime) - new Date(a.posttime));
        } else {
            return data
                .filter(item => item.origin === selectedFilter)
                .sort((a, b) => new Date(b.posttime) - new Date(a.posttime));
        }
    }
  
    // Function to handle filter change
    function handleFilterChange(filter) {
      selectedFilter = filter;
      filtered = getFilteredData();
    }

    function getIcon(type) {
        switch (type) {
            case 'Earthquake':
                return 'src\\assets\\earthquake.png';
            case 'Tornado':
                return 'src\\assets\\Tornado.png';
            case 'Hurricane':
                return 'src\\assets\\Hurricane.jpg';
            case 'Snow-Storm':
                return 'src\\assets\\Snowstorm.jpg';
            default:
                return 'src\\assets\\Weather_Logo.png';
        }
    } 

    function handle_click(id){
        setSelectedMarker(id);
        selectedMarker = getSelectedMarker();
    }

    afterUpdate(() => {
        selectedMarker = getSelectedMarker();
    });

</script>
  
<main>
    <div class="header-buttons">
    {#each headers as header}
        <button on:click={() => handleFilterChange(header)}>
        {header}
        </button>
    {/each}
    </div>

    <div class="data-list">
    {#each filtered as item}
        {#if selectedMarker !== null && selectedMarker.id === item.id}
            <div class="data-item highlight" on:click={()=> handle_click(item.id)}>
                <div class="item-header">
                    <img src={getIcon(item.type)} alt={item.type} class = icon/>
                    <div><strong>Type:</strong> {item.type}</div>
                    <div> {item.posttime}</div>
                </div>
                <div class="item-header">Urgency:<strong>{item.urgency}</strong></div>
                {#if item.imgsrc !==""}
                <div class="item-image">
                    <img src={item.imgsrc} alt={item.type} />
                </div> 
                {/if}
                <div class="item-description">{item.description}</div>
                <div class="item-header"><strong>Source:</strong> <a href="{item.source}" target="_blank">{item.source}</a></div>
            </div>
        {/if}

        {#if selectedMarker !== null && selectedMarker.id !== item.id}
            <div class="data-item" on:click={()=> handle_click(item.id)}>
                <div class="item-header">
                    <img src={getIcon(item.type)} alt={item.type} class = icon/>
                    <div><strong>Type:</strong> {item.type}</div>
                    <div> {item.posttime}</div>
                </div>
                <div class="item-header">Urgency:<strong>{item.urgency}</strong></div>
                {#if item.imgsrc !==""}
                <div class="item-image">
                    <img src={item.imgsrc} alt={item.type} />
                </div> 
                {/if}
                <div class="item-description">{item.description}</div>
                <div class="item-header"><strong>Source:</strong> <a href="{item.source}" target="_blank">{item.source}</a></div>
            </div>
        {/if}

        {#if selectedMarker === null}
            <div class="data-item" on:click={()=> handle_click(item.id )}>
                <div class="item-header">
                    <img src={getIcon(item.type)} alt={item.type} class = icon/>
                    <div><strong>Type:</strong> {item.type}</div>
                    <div> {item.posttime}</div>
                </div>
                <div class="item-header">Urgency:<strong>{item.urgency}</strong></div>
                {#if item.imgsrc !==""}
                <div class="item-image">
                    <img src={item.imgsrc} alt={item.type} />
                </div> 
                {/if}
                <div class="item-description">{item.description}</div>
                <div class="item-header"><strong>Source:</strong> <a href="{item.source}" target="_blank">{item.source}</a></div>
            </div>
        {/if}
    {/each}
    </div>
</main>

<style>
    .header-buttons {
        display: flex;
        justify-content: space-around;
        margin-bottom: 1rem;
    }

    .header-buttons button {
        padding: 0.5rem 1.5rem;
        cursor: pointer;
        border: 1px solid #ccc; /* Add a border to distinguish buttons */
        border-right: none; /* Remove the right border to avoid double borders */
        background-color: black; /* Light background color */
        transition: background-color 0.3s, box-shadow 0.3s; /* Smooth transition for hover effects */
    }

    .header-buttons button:last-child {
        border-right: 1px solid #ccc; /* Add the right border to the last button */
    }

    .header-buttons button:hover {
        background-color: #e0e0e0; /* Slightly darker background on hover */
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Add a subtle shadow on hover */
    }

    .data-item {
        margin-bottom: 1rem;
        padding: 1rem;
        border: 1px solid #ccc; /* Add a border to each item */
        border-radius: 4px; /* Add rounded corners */
        background-color: #fff; /* White background color */
        transition: box-shadow 0.3s; /* Smooth transition for hover effects */
        color: black; /* Adjust text color as needed */
    }
  
    .data-item:hover {
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Add a stronger shadow on hover */
    }

    .data-list {
        max-height: calc(100vh - 200px); /* Adjust this value based on your layout */
        overflow-y: auto;
        border: 1px solid #ccc;
        padding: 1rem;
        background-color: lightgray; /* Light background color */
    }

    .item-header {
        display: flex;
        justify-content: left;
        text-align: left;
    }

    .item-image {
        margin: 1rem 0;
        display: flex;
        justify-content: flex-start;
    }

    .item-image img {
        max-height: 150px; /* Adjust this value as needed */
        width: auto;
        height: auto;
        border-radius: 4px;
    }

    .item-header > div {
        margin-right: 1rem;
    }

    .item-description {
        text-align: left;
        margin-top: 0.5rem;
    }
    .icon {
      width: 24px; /* Adjust the width as needed */
      height: 24px; /* Adjust the height as needed */
      margin-right: 0.5rem; /* Optional: Add some space to the right of the icon */
      vertical-align: middle; /* Align the icon vertically with the text */
    }
    :global(.highlight) {
        
        border: 2px solid #000; /* Highlight border */
        box-shadow: 0 0 10px 5px rgba(255, 255, 0, 0.7); /* Add a glow effect */
    }
</style>