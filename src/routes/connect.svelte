<script>
  import { onMount } from 'svelte';
  import { draw } from 'svelte/transition';
  import GithubIcon from '../lib/icons/github.svelte';
  import LinkedinIcon from '../lib/icons/linkedin.svelte';

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

<section id="connect" bind:this={sectionRef}>
  <div class="container">
    <h2>Reach out if you want to create powerful, efficient, and beautifully designed software <i>together.</i></h2>
    <div class="solid-line" class:visible={visible}></div>
    <div class="social-icons">
      <a href="https://github.com/austinhardy" target="_blank">
        <GithubIcon class="social-icon" />
      </a>
      <a href="https://www.linkedin.com/in/austin-j-hardy/" target="_blank">
        <LinkedinIcon class="social-icon" />
      </a>
    </div>
  </div>
</section>

<style>
  section {
    min-height: 100vh;
    box-sizing: border-box;
    background-color: var(--color-bg-1);
    color: var(--color-text-2);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .container {
    max-width: 64rem;
    flex: 1 1 0;
    padding: 4rem;
  }

  h2 {
    font-family: var(--font-radley);
    font-size: 3rem;
    margin: 0;
    text-align: left;
    line-height: 1.5;
    max-width: 48rem;
  }

  .solid-line {
    height: 2px;
    max-width: 70%;
    background-color: #bd8f53;
    margin: 2rem 0 1rem;
    transform: scaleX(0);
    transition: transform 0.5s ease;
  }

  .solid-line.visible {
    transform: scaleX(1);
  }

  .social-icons {
    display: flex;
    gap: 0.75rem;
    margin: 1rem 0;
  }

  :global(.social-icon) {
    width: 2rem;
    height: 2rem;
    color: var(--color-text-2);
    transition: color 0.1s ease, transform 0.1s ease;

    &:hover {
      color: #ceccc4;
      transform: scale(1.1);
    }
  }

  @media (max-width: 768px) {
    .container {
      padding: 4rem 2rem;
      grid-template-columns: 1fr;
      text-align: center;
    }

    h2 {
      font-size: 2rem;
    }
  }
</style>
