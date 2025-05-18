<script>
  import svelteLogo from './assets/svelte.svg'
  import viteLogo from '/vite.svg'
  import Counter from './lib/Counter.svelte'
  import { onMount } from 'svelte';

  let isLoading = true;
  let showModal = false;
  let referenceId = '';
  let withdrawalTime = '';
  let withdrawalAmount = '';

  onMount(() => {
    setTimeout(() => {
      isLoading = false;
      referenceId = `BDO-${Math.random().toString(36).substr(2, 9).toUpperCase()}`;
      withdrawalTime = new Date().toLocaleTimeString();
      withdrawalAmount = `$${(Math.random() * 10000).toFixed(2)}`; // Random amount for example
      showModal = true;
    }, 3000);
  });

  function closeModal() {
    showModal = false;
    // Optionally, reset for another "transaction" or navigate away
  }
</script>

<main>
  {#if isLoading}
    <div class="loading-container">
      <div class="spinner"></div>
      <p>Processing your withdrawal...</p>
    </div>
  {:else if showModal}
    <div class="modal-backdrop">
      <div class="modal">
        <h2>Withdrawal Successful!</h2>
        <p><strong>Reference ID:</strong> {referenceId}</p>
        <p><strong>Time:</strong> {withdrawalTime}</p>
        <p><strong>Amount:</strong> {withdrawalAmount}</p>
        <button on:click={closeModal}>Close</button>
      </div>
    </div>
  {/if}

  <!-- Your existing app content can go here or be conditionally rendered -->
  {#if !isLoading && !showModal}
    <h1>Welcome to BDO Online</h1>
    <p>Please insert your card...</p>
     <!-- Example: Add a button to trigger a new withdrawal for testing -->
    <button on:click={() => {
      isLoading = true;
      showModal = false;
      setTimeout(() => {
        isLoading = false;
        referenceId = `BDO-${Math.random().toString(36).substr(2, 9).toUpperCase()}`;
        withdrawalTime = new Date().toLocaleTimeString();
        withdrawalAmount = `$${(Math.random() * 10000).toFixed(2)}`;
        showModal = true;
      }, 3000);
    }}>
      Simulate Another Withdrawal
    </button>
  {/if}
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  .loading-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh; /* Full viewport height */
  }

  .spinner {
    border: 4px solid rgba(0, 0, 0, 0.1);
    width: 36px;
    height: 36px;
    border-radius: 50%;
    border-left-color: #09f;
    animation: spin 1s ease infinite;
  }

  @keyframes spin {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  .modal-backdrop {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .modal {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    text-align: left;
    min-width: 300px;
  }

  .modal h2 {
    margin-top: 0;
    color: #007bff; /* BDO Blue */
  }

  .modal p {
    margin: 10px 0;
  }

  .modal button {
    background-color: #007bff; /* BDO Blue */
    color: white;
    border: none;
    padding: 10px 15px;
    border-radius: 4px;
    cursor: pointer;
    float: right;
    margin-top: 10px;
  }

  .modal button:hover {
    background-color: #0056b3;
  }

  /* Responsive adjustments */
  @media (min-width: 600px) {
    main {
      max-width: none;
    }
  }

  .logo {
    height: 6em;
    padding: 1.5em;
    will-change: filter;
    transition: filter 300ms;
  }
  .logo:hover {
    filter: drop-shadow(0 0 2em #646cffaa);
  }
  .logo.svelte:hover {
    filter: drop-shadow(0 0 2em #ff3e00aa);
  }
  .read-the-docs {
    color: #888;
  }
</style>
