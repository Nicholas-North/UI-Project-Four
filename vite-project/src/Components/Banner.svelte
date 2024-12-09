<script>
    import bannerImage from '../assets/Weather_Logo.png';
</script>

<main>
    <div class="banner">
        <img src={bannerImage} alt="Weather Logo" class="logo"/>
        <div class="text-section">
            <h1>National Weather Service</h1>
            <p>Emergency Weather Application</p>
        </div>
    </div>

</main>

<style>
    :global(body) {
        margin: 0;
    }

    .banner {
        display: flex;
        align-items: center;
        width: 100%;
        background-color: white;
        padding: 10px; /* Adjust padding as needed */
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Optional: adds a subtle shadow */
        position: fixed;
        top: 0;
        left: 0;
        z-index: 1000; /* Ensure it stays on top */
        height: 60px; /* Fixed height */
    }

    .logo {
        width: 100px; /* Adjust size as needed */
        height: auto;
    }

    .text-section {
        margin-left: 20px; /* Adjust spacing as needed */
    }

    h1 {
        margin: 0;
        font-size: 24px; /* Adjust size as needed */
        color: black; /* Adjust color as needed */
    }

    p {
        margin: 0;
        font-size: 16px; /* Adjust size as needed */
        color: gray; /* Adjust color as needed */
    }
</style>