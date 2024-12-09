<script>
    let title = '';
    let description = '';
    let sourceLink = '';
    let image = null;
  
    function handleSubmit() {
      const postData = {
        title,
        description,
        sourceLink,
        image
      };
      console.log('Submitted data:', postData);
      // You can add your form submission logic here
    }
  
    function handleImageChange(event) {
      const file = event.target.files[0];
      if (file) {
        image = URL.createObjectURL(file);
      }
    }
  </script>
  
  <style>
    .form-container {
      display: flex;
      flex-direction: column;
      width: 50vw;
      margin: 0 auto;
      padding: 2rem;
      background-color: gray;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(26, 25, 25, 0.1);
    }
  
    .form-group {
      margin-bottom: 1rem;
      color: black;
      background-color: lightgray;
    }
  
    .form-group label {
      display: block;
      margin-bottom: 0.5rem;
      font-weight: bold;
    }
  
    .form-group input,
    .form-group textarea {
      width: 100%;
      padding: 0.5rem;
      border: 1px solid #ccc;
      border-radius: 5px;
      background-color: white;
      color: black;
    }
  
    .form-group input[type="file"] {
      padding: 0;
    }
  
    .form-group img {
      max-width: 100%;
      margin-top: 1rem;
    }
  
    .submit-button {
      padding: 0.75rem;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
    }
  
    .submit-button:hover {
      background-color: #0056b3;
    }
  </style>
  
  <div class="form-container">
    <div class="form-group">
      <label for="title">Title</label>
      <input type="text" id="title" bind:value={title} />
    </div>
  
    <div class="form-group">
      <label for="description">Description</label>
      <textarea id="description" rows="4" bind:value={description}></textarea>
    </div>
  
    <div class="form-group">
      <label for="sourceLink">Source Link</label>
      <input type="url" id="sourceLink" bind:value={sourceLink} />
    </div>
  
    <div class="form-group">
      <label for="image">Image (optional)</label>
      <input type="file" id="image" accept="image/*" on:change={handleImageChange} />
      {#if image}
        <img src={image} alt="Selected image" />
      {/if}
    </div>
  
    <button class="submit-button" on:click={handleSubmit}>Submit</button>
</div>