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
    <div class="content-container">
      <div class="title-container">
        <h2>About Austin</h2>
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
              stroke="var(--color-text-1)"
              stroke-width="5"
              stroke-linecap="round"
              transition:draw={{duration: 1500, easing: customFastEasing}}
            />
          {/if}
        </svg>
      </div>
      <p>
        I'm a software developer with a passion for building scalable, efficient solutions. I'm a quick learner and a team player. I'm a graduate of the University of Waterloo with a degree in Computer Science. I'm currently a software developer at Vidyard.
      </p>
    </div>
    <img 
      src="src/lib/images/IMG_5857.JPEG"
      alt="Austin Hardy"
      class:visible={visible}
    />
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
    background-color: var(--color-bg-0);
    color: var(--color-text-0);
  }

  .container {
    display: grid;
    grid-template-columns: 3fr 2fr;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 2rem;
    height: 100%;
    max-width: 64rem;
    padding: 4rem;
  }

  h2 {
    font-family: var(--font-radley);
    font-size: 3rem;
    text-align: center;
    margin: 0;
    color: var(--color-text-1);
  }

  .title-container {
    position: relative;
    width: fit-content;
    margin-bottom: 2rem;
  }

  .underline {
    position: absolute;
    bottom: -25%;
    left: 40%;
    transform: rotate(6deg) scaleY(0.8);
  }

  img {
    width: 100%;
    max-width: 22rem;
    border-radius: 1rem;
    opacity: 0;
    transform: translateY(4rem);
    transition: opacity 0.5s ease, transform 0.5s ease;
  }

  img.visible {
    opacity: 1;
    transform: translateY(0);
  }

  @media (max-width: 768px) {
    .container {
      grid-template-columns: 1fr;
      text-align: center;
    }

    .content-container {
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    img {
      margin: 0 auto;
    }
  }
</style>
