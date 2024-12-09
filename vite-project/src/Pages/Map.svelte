<script lang="ts">
    import { onMount, setContext } from 'svelte';
    import { MapLibre, DefaultMarker, Marker, Popup } from 'svelte-maplibre';
    import 'maplibre-gl/dist/maplibre-gl.css';

    import Markers from '../assets/Markers.json';
    import List from '../Components/List.svelte';

    let selectedMarker = null;

    let headers = [
        'All',
        'Government',
        'Social',
        'News'
    ]

    let formattedMarkers = Markers.map(marker => ({
        lngLat: [marker.lng, marker.lat] as [number, number],
        label: String(marker.id),
        name: marker.name,
        urgency: marker.urgency,
        type: marker.type
    }));

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

    function setSelectedMarker(id){
        selectedMarker = Markers.find(marker => marker.id === Number(id));
        console.log(selectedMarker.id);
    }
    function getSelectedMarker(){
        return selectedMarker;
    }

    setContext('setSelectedMarker', setSelectedMarker);
    setContext('getSelectedMarker', getSelectedMarker);


</script>

<main>
    <MapLibre
        style="https://basemaps.cartocdn.com/gl/positron-gl-style/style.json"
        class="map"
        standardControls
        zoom={1}
        center={[-20, 0]}
    >
        {#each formattedMarkers as { lngLat, label, name, urgency, type }}
            <!-- {#if 1 === 1}
                <Marker
                    {lngLat}
                    draggable={false}
                    onclick={() => setSelectedMarker(label)}
                    class={`marker ${urgency} ${selectedMarker && selectedMarker.id === label ? 'highlight' : ''}`}
                >
                <span class="pin">
                    <img src={getIcon(type)} alt={type} class="icon" />
                </span>
            
                <Popup openOn="hover" offset={[0, -10]}>
                    <div class="text-lg font-bold">{name}</div>
                </Popup>
                </Marker>
            {/if} -->
            {#if selectedMarker !== null && Number(label) === Number(selectedMarker.id)}
                <Marker
                    {lngLat}
                    draggable={false}
                    onclick={() => setSelectedMarker(label)}
                    class={`marker ${urgency} highlight`}
                >
                <span class="pin">
                    <img src={getIcon(type)} alt={type} class="icon" />
                </span>
            
                <Popup openOn="hover" offset={[0, -10]}>
                    <div class="text-lg font-bold">{name}</div>
                </Popup>
                </Marker>
            {/if}
            {#if selectedMarker !== null && Number(label) !== Number(selectedMarker.id)}
                <Marker
                    {lngLat}
                    draggable={false}
                    onclick={() => setSelectedMarker(label)}
                    class={`marker ${urgency}`}
                >
                <span class="pin">
                    <img src={getIcon(type)} alt={type} class="icon" />
                </span>

                <Popup openOn="hover" offset={[0, -10]}>
                    <div class="text-lg font-bold">{name}</div>
                </Popup>
                </Marker>
            {/if}
            {#if selectedMarker === null}
                <Marker
                    {lngLat}
                    draggable={false}
                    onclick={() => setSelectedMarker(label)}
                    class={`marker ${urgency}`}
                >
                <span class="pin">
                    <img src={getIcon(type)} alt={type} class="icon" />
                </span>

                <Popup openOn="hover" offset={[0, -10]}>
                    <div class="text-lg font-bold">{name}</div>
                </Popup>
                </Marker>
            {/if}
            <!-- <Marker
                {lngLat}
                draggable={false}
                onclick={() => setSelectedMarker(label)}
                class={`marker ${urgency} ${selectedMarker && selectedMarker.id === label ? 'highlight' : ''}`}
            >
            <span class="pin">
                <img src={getIcon(type)} alt={type} class="icon" />
            </span>
        
            <Popup openOn="hover" offset={[0, -10]}>
                <div class="text-lg font-bold">{name}</div>
            </Popup>
            </Marker> -->
        {/each}
    </MapLibre>
    <div class="list-container">
        <List headers={headers} data={Markers} />
    </div>
</main>

<style>
    :global(.map) {
        position: absolute;
        top: 135px; /* Adjust this value based on the height of your NavBar */
        left: 0;
        height: calc(100vh - 125px); /* Adjust this value based on the height of your NavBar */
        width: 66.66%; /* 2/3 of the width */
    }
    .list-container {
        position: absolute;
        top: 135px; /* Adjust this value based on the height of your NavBar */
        right: 0;
        height: calc(100vh - 125px); /* Adjust this value based on the height of your NavBar */
        width: 33.33%; /* 1/3 of the width */
    }
    :global(.marker) {
        display: grid;
        height: 2rem; /* h-8 */
        width: 2rem; /* w-8 */
        place-items: center;
        border-radius: 9999px; /* rounded-full */
        border: 1px solid #e5e7eb; /* border-gray-200 */
        background-color: #fca5a5; /* bg-red-300 */
        color: #000000; /* text-black */
        box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05); /* shadow-2xl */
        outline: 2px solid transparent; /* focus:outline-2 */
        outline-offset: 2px; /* focus:outline-black */
    }
    .pin {
        position: relative;
        width: 2rem; /* h-8 */
        height: 2rem; /* w-8 */
        background-color: #fca5a5; /* bg-red-300 */
        border-radius: 50% 50% 50% 0; /* Pin shape */
        transform: rotate(-45deg);
        box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05); /* shadow-2xl */
    }
    .icon {
        position: absolute;
        width: 1rem; /* h-4 */
        height: 1rem; /* w-4 */
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        z-index: 1;
    }
    :global(.highlight) {
        
        border: 2px solid #000; /* Highlight border */
        box-shadow: 0 0 10px 5px rgba(255, 255, 0, 0.7); /* Add a glow effect */
    }
    :global(.low .pin) {
        background-color: #34d399; /* green-400 */
    }
    :global(.medium .pin) {
        background-color: #fbbf24; /* yellow-400 */
    }
    :global(.high .pin) {
        background-color: #f87171; /* red-400 */
    }
</style>