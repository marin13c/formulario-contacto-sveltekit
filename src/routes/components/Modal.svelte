<script>
    export let showModal;
    export let successMessage;
    export let registers;
    export let handleCloseModal;
    export let isServicesEmpty;
  </script>
  
  {#if showModal}
  <div class="fixed top-0 left-0 w-full h-full flex items-center justify-center z-50">
    <div class="bg-white p-8 rounded-xl shadow-lg w-96 z-50">
      <h2 class="text-lg font-bold mb-4">Message</h2>
      {#if successMessage}
        <p class="mb-4">The data has been sent correctly. We will be contacting you soon!</p>
      {:else if isServicesEmpty && registers.name && registers.last_name && registers.email && registers.phone && registers.message}
        <p class="mb-4">Please select at least one service!</p>
      {:else if !(registers.name && registers.last_name && registers.email && registers.phone && registers.message)}
        <p class="mb-4">Please complete all fields!</p>
      {/if}
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-3 px-8 rounded-lg focus:outline-none focus:shadow-outline" on:click={handleCloseModal}>OK</button>
    </div>
  </div>
{/if}