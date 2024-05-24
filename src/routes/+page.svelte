<script>
// @ts-nocheck

    import FormComponent from '../components/Form.svelte';
    import Navbar from '../components/Navbar.svelte';
  </script>
  
  <Navbar />
  <main>
    <FormComponent />
  </main>
  
  <style lang="postcss">
    :global(html) {
      background-color: #021325;
    }
  </style>