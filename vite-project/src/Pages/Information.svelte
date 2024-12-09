<script>
    let tornadoOpen = false;
    let hurricaneOpen = false;
    let earthquakeOpen = false;
    let snowstormOpen = false;
  
    let tornadoFaqs = { whatToDo: false, howToPrepare: false, during: false, after: false };
    let hurricaneFaqs = { whatToDo: false, howToPrepare: false, during: false, after: false };
    let earthquakeFaqs = { whatToDo: false, howToPrepare: false, during: false, after: false };
    let snowstormFaqs = { whatToDo: false, howToPrepare: false, during: false, after: false };
  
    function toggle(section) {
      if (section === 'tornado') tornadoOpen = !tornadoOpen;
      if (section === 'hurricane') hurricaneOpen = !hurricaneOpen;
      if (section === 'earthquake') earthquakeOpen = !earthquakeOpen;
      if (section === 'snowstorm') snowstormOpen = !snowstormOpen;
    }
  
    function toggleFaq(section, faq) {
      if (section === 'tornado') tornadoFaqs[faq] = !tornadoFaqs[faq];
      if (section === 'hurricane') hurricaneFaqs[faq] = !hurricaneFaqs[faq];
      if (section === 'earthquake') earthquakeFaqs[faq] = !earthquakeFaqs[faq];
      if (section === 'snowstorm') snowstormFaqs[faq] = !snowstormFaqs[faq];
    }
  </script>
  
  <style>
    body {
      background-color: #f5f5f5;
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
    }
  
    .container {
      width: 50vw;
    }
  
    .title {
      font-size: 2rem;
      text-align: left;
      margin: 2rem 0;
    }
  
    .header {
      font-size: 1.5rem;
      cursor: pointer;
      margin: 1rem 0;
      padding: 1rem;
      background-color: lightgray;
      border-radius: 10px;
      width: 100%;
      box-sizing: border-box;
      color: black;
      text-align: left;
    }
  
    .sub-header {
      margin-left: 1rem;
      font-size: 1rem;
      cursor: pointer;
      padding: 0.5rem;
      background-color: white;
      border-radius: 5px;
      width: calc(100% - 1rem);
      box-sizing: border-box;
      color: black;
      text-align: left;
    }
  
    .faq {
      margin-left: 2rem;
      font-size: 0.9rem;
      padding: 0.5rem;
      background-color: white;
      border-radius: 5px;
      width: calc(100% - 2rem);
      box-sizing: border-box;
      color: black;
      text-align: left;
    }
  </style>
  
  <div class="container">
    <div class="title">Frequently Asked Questions</div>
  
    <div class="header" on:click={() => toggle('tornado')}>Tornado's</div>
    {#if tornadoOpen}
      <div class="sub-header" on:click={() => toggleFaq('tornado', 'whatToDo')}>FAQ: What to do during a tornado?</div>
      {#if tornadoFaqs.whatToDo}
        <div class="faq">Seek shelter immediately, preferably in a basement or an interior room without windows.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('tornado', 'howToPrepare')}>FAQ: How to prepare for a tornado?</div>
      {#if tornadoFaqs.howToPrepare}
        <div class="faq">Have a plan, create an emergency kit, and stay informed about weather conditions.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('tornado', 'during')}>FAQ: What to do during a tornado warning?</div>
      {#if tornadoFaqs.during}
        <div class="faq">Stay indoors, away from windows, and follow local weather updates.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('tornado', 'after')}>FAQ: What to do after a tornado?</div>
      {#if tornadoFaqs.after}
        <div class="faq">Check for injuries, avoid damaged areas, and listen for emergency information.</div>
      {/if}
    {/if}
  
    <div class="header" on:click={() => toggle('hurricane')}>Hurricane's</div>
    {#if hurricaneOpen}
      <div class="sub-header" on:click={() => toggleFaq('hurricane', 'whatToDo')}>FAQ: What to do during a hurricane?</div>
      {#if hurricaneFaqs.whatToDo}
        <div class="faq">Evacuate if instructed, stay indoors, and avoid flood-prone areas.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('hurricane', 'howToPrepare')}>FAQ: How to prepare for a hurricane?</div>
      {#if hurricaneFaqs.howToPrepare}
        <div class="faq">Create an emergency kit, secure your home, and stay informed about weather updates.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('hurricane', 'during')}>FAQ: What to do during a hurricane warning?</div>
      {#if hurricaneFaqs.during}
        <div class="faq">Stay indoors, away from windows, and follow local weather updates.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('hurricane', 'after')}>FAQ: What to do after a hurricane?</div>
      {#if hurricaneFaqs.after}
        <div class="faq">Check for injuries, avoid floodwaters, and listen for emergency information.</div>
      {/if}
    {/if}
  
    <div class="header" on:click={() => toggle('earthquake')}>Earthquakes</div>
    {#if earthquakeOpen}
      <div class="sub-header" on:click={() => toggleFaq('earthquake', 'whatToDo')}>FAQ: What to do during an earthquake?</div>
      {#if earthquakeFaqs.whatToDo}
        <div class="faq">Drop, cover, and hold on. Stay indoors until the shaking stops.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('earthquake', 'howToPrepare')}>FAQ: How to prepare for an earthquake?</div>
      {#if earthquakeFaqs.howToPrepare}
        <div class="faq">Secure heavy items, create an emergency plan, and have a disaster kit ready.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('earthquake', 'during')}>FAQ: What to do during an earthquake warning?</div>
      {#if earthquakeFaqs.during}
        <div class="faq">Stay indoors, away from windows, and follow local updates.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('earthquake', 'after')}>FAQ: What to do after an earthquake?</div>
      {#if earthquakeFaqs.after}
        <div class="faq">Check for injuries, avoid damaged areas, and listen for emergency information.</div>
      {/if}
    {/if}
  
    <div class="header" on:click={() => toggle('snowstorm')}>Snow Storms</div>
    {#if snowstormOpen}
      <div class="sub-header" on:click={() => toggleFaq('snowstorm', 'whatToDo')}>FAQ: What to do during a snowstorm?</div>
      {#if snowstormFaqs.whatToDo}
        <div class="faq">Stay indoors, keep warm, and avoid travel if possible.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('snowstorm', 'howToPrepare')}>FAQ: How to prepare for a snowstorm?</div>
      {#if snowstormFaqs.howToPrepare}
        <div class="faq">Stock up on supplies, have a backup heat source, and stay informed about weather conditions.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('snowstorm', 'during')}>FAQ: What to do during a snowstorm warning?</div>
      {#if snowstormFaqs.during}
        <div class="faq">Stay indoors, keep warm, and follow local updates.</div>
      {/if}
      <div class="sub-header" on:click={() => toggleFaq('snowstorm', 'after')}>FAQ: What to do after a snowstorm?</div>
      {#if snowstormFaqs.after}
        <div class="faq">Check for injuries, clear snow safely, and listen for emergency information.</div>
      {/if}
    {/if}
  </div>