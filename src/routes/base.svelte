<script>
  import { onMount } from 'svelte';
  import { draw } from 'svelte/transition';

  let visible = false;
  let sectionRef;

  onMount(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        visible = entry.isIntersecting;
      });
    }, { threshold: 0.5 });

    observer.observe(sectionRef);

    return () => {
      observer.unobserve(sectionRef);
    };
  });

  function customFastEasing(t) {
    return 1 - Math.pow(1 - t, 8);
  }
</script>

<section id="experience" bind:this={sectionRef}>
  <div class="container">
    <div class="title-container">
      <h2>Experience</h2>
      <svg
        class="underline"
        width="200"
        viewBox="0 0 572 73"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        {#if visible}
          <path
            d="M1.77966 71.2773C20.7771 62.5928 40.1664 56.5709 60.4566 51.136C134.662 31.2597 210.429 18.9276 286.84 11.2645C380.95 1.82661 475.435 -0.709058 569.64 6.5375"
            stroke="var(--color-text-2)"
            stroke-width="4"
            stroke-linecap="round"
            transition:draw={{duration: 1500, easing: customFastEasing}}
          />
        {/if}
      </svg>
    </div>
  </div>
</section>

<style>
  section {
    height: 100vh;
    padding: 4rem;
    box-sizing: border-box;
    background-color: var(--color-bg-1);
    color: var(--color-text-1);
  }

  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    flex: 0.6;
    height: 100%;
    max-width: 64rem;
    margin: 0 auto;
  }
</style>
