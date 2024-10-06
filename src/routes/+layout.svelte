<script>
  import '../app.css';
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';

  onMount(() => {
    // Handle initial load and browser back/forward
    scrollToHash();

    // Listen for hash changes
    window.addEventListener('hashchange', scrollToHash);
  });

  function scrollToHash() {
    const hash = window.location.hash.slice(1);
    if (hash) {
      const element = document.getElementById(hash);
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
      }
    }
  }
</script>

<div class="app">
  <main>
    <div id="scroll-container">
      <slot />
    </div>
  </main>
</div>

<style>
  .app {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  main {
    flex: 1;
    display: flex;
    flex-direction: column;
    width: 100%;
    margin: 0 auto;
    box-sizing: border-box;
  }

  #scroll-container {
    height: 100vh;
    overflow-y: auto;
    scroll-behavior: smooth;
  }

  /* ... (keep other styles) ... */
</style>
