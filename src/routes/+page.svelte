<script>
// @ts-nocheck

    import FormComponent from './components/Form.svelte';
    import Navbar from './components/Navbar.svelte';
  </script>
  
  <Navbar />
  <main>
    <FormComponent />
  </main>
  
  <style lang="postcss">
    :global(html) {
      background-color: #021325;
    }
  
    .font-bb-casual-pro-medium {
      font-family: "BB Casual Pro Medium", sans-serif;
    }
  
    .text-gradient {
      background: linear-gradient(0deg, #0683ff, rgba(0, 128, 255, 0.84)),
        linear-gradient(270deg, #0683ff 14.19%, #065aaf 100.84%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent !important;
    }
  </style>