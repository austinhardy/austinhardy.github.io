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

    <div class="experience-grid" class:visible={visible}>
      <div class="experience-column">
        <h3>Vidyard</h3>
        <h4>Staff Developer</h4>
        <div class="solid-line"></div>
        <p>Apr 2020 - Present</p>
      </div>
      <div class="experience-column">
        <h3>PerkinElmer</h3>
        <h4>Software Developer Co-op</h4>
        <div class="solid-line"></div>
        <p>Sept 2017 - Dec 2017</p>
      </div>
      <div class="experience-column">
        <h3>Rave Inc.</h3>
        <h4>Software Developer Co-op</h4>
        <div class="solid-line"></div>
        <p>Jun 2016 - Jun 2017</p>
      </div>
    </div>
  </div>
</section>

<style>
  section {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    box-sizing: border-box;
    background-color: var(--color-bg-2);
    color: var(--color-text-2);
  }

  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    flex: 0.6;
    height: 100%;
    max-width: 64rem;
    padding: 4rem;
  }

  h2 {
    font-family: var(--font-radley);
    font-size: 3rem;
    text-align: center;
    margin-bottom: 2rem;
  }

  .title-container {
    position: relative;
  }

  .underline {
    position: absolute;
    bottom: 8%;
    left: 30%;
    transform: rotate(3deg);
  }

  .experience-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2rem;
    opacity: 0;
    transform: translateY(4rem);
    transition: opacity 0.5s ease, transform 0.5s ease;
  }

  .experience-grid.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .experience-column {
    padding: 1.5rem;
  }

  h3 {
    font-family: var(--font-radley);
    font-size: 1.5rem;
    margin: 0.5rem 0;
  }

  h4 {
    font-family: var(--font-carlito);
    font-size: 1rem;
    font-weight: 100;
    letter-spacing: 0.1rem;
    margin: 0.5rem 0;
  }

  p {
    font-family: var(--font-carlito);
    font-size: 0.9rem;
    line-height: 1.6;
    font-weight: 100;
  }

  .solid-line {
    height: 2px;
    width: 100%;
    background-color: #bd8f53;
    margin: 1rem 0;
  }

  @media (max-width: 768px) {
    .container {
      padding: 4rem 2rem;
    }

    .experience-grid {
      grid-template-columns: 1fr;
    }
  }
</style>
