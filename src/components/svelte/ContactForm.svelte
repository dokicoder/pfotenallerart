<script>
  let name = '';
  let email = '';
  let message = '';
  let submitted = false;
  let error = '';

  function handleSubmit() {
    if (!name || !email || !message) {
      error = 'Bitte füllen Sie alle Felder aus.';
      return;
    }
    
    if (!email.includes('@')) {
      error = 'Bitte geben Sie eine gültige E-Mail-Adresse ein.';
      return;
    }
    
    // In a real app, you would send this data to a server
    console.log({ name, email, message });
    
    // Reset form and show success message
    name = '';
    email = '';
    message = '';
    error = '';
    submitted = true;
    
    // Hide success message after 5 seconds
    setTimeout(() => {
      submitted = false;
    }, 5000);
  }
</script>

<div class="contact-form">
  {#if submitted}
    <div class="success-message">
      <p>Vielen Dank für Ihre Nachricht! Ich werde mich so schnell wie möglich bei Ihnen melden.</p>
    </div>
  {:else}
    <form on:submit|preventDefault={handleSubmit}>
      {#if error}
        <div class="error-message">
          <p>{error}</p>
        </div>
      {/if}
      
      <div class="form-group">
        <label for="name">Name</label>
        <input type="text" id="name" bind:value={name} placeholder="Ihr Name">
      </div>
      
      <div class="form-group">
        <label for="email">E-Mail</label>
        <input type="email" id="email" bind:value={email} placeholder="Ihre E-Mail-Adresse">
      </div>
      
      <div class="form-group">
        <label for="message">Nachricht</label>
        <textarea id="message" bind:value={message} rows="5" placeholder="Ihre Nachricht"></textarea>
      </div>
      
      <button type="submit" class="btn">Nachricht senden</button>
    </form>
  {/if}
</div>

<style>
  .contact-form {
    max-width: 600px;
    margin: 0 auto;
  }
  
  .form-group {
    margin-bottom: 1.5rem;
  }
  
  label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: bold;
    color: var(--primary-dark);
  }
  
  input, textarea {
    width: 100%;
    padding: 0.8rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 1rem;
    transition: border-color 0.3s ease;
  }
  
  input:focus, textarea:focus {
    border-color: var(--primary);
    outline: none;
  }
  
  .success-message {
    background-color: #e8f5e9;
    color: #2e7d32;
    padding: 1rem;
    border-radius: 4px;
    text-align: center;
  }
  
  .error-message {
    background-color: #ffebee;
    color: #c62828;
    padding: 1rem;
    border-radius: 4px;
    margin-bottom: 1rem;
  }
  
  button {
    cursor: pointer;
  }
</style>