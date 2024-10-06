<script>
  import { onMount } from 'svelte';
  import { draw } from 'svelte/transition';

  let drawLine = false;
  let subtitleVisible = false;

  onMount(() => {
    setTimeout(() => {
      drawLine = true;
    }, 500);
    setTimeout(() => {
      subtitleVisible = true;
    }, 1500);
  });

  function customFastEasing(t) {
    return 1 - Math.pow(1 - t, 5);
  }
</script>

<section id="hello">
  <div class="container">
    <h1>
      <i>Hello,</i>
      <span>I am</span>
      <span class="name">
        Austin!
        <div class="circle-container">
          <svg width="14rem" viewBox="-2 -2 506 288" fill="none" xmlns="http://www.w3.org/2000/svg">
            {#if drawLine}
              <path
                d="M217.751 2.34039C229.521 2.34039 241.292 2.34039 253.063 2.34039C308.768 2.34039 367.501 -1.80576 422.002 12.2386C441.583 17.2845 473.646 30.0511 487.544 47.4174C500.719 63.8805 500.193 86.8445 494.098 105.603C486.535 128.879 460.599 169.015 445.276 186.26C404.409 232.249 351.127 261.372 291.118 273.939C210.57 290.807 115.186 281.998 49.0798 228.595C9.75319 196.825 -11.5076 141.735 12.7641 94.1663C43.801 33.339 121.291 18.1683 182.706 13.6431C245.573 9.01077 308.669 19.364 370.638 28.8248"
                stroke="var(--color-text-0)"
                opacity="1"
                stroke-width="6"
                stroke-linecap="round"
                transition:draw={{duration: 1500, easing: customFastEasing}}
              />
            {/if}
          </svg>
        </div>
      </span>
    </h1>

    <h2 class:visible={subtitleVisible}>
      I build flexible, efficient solutions with a passion for modular code and thoughtful system design.
    </h2>
  </div>
</section>

<style>
  section {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    max-width: 64rem;
    padding: 4rem;
  }

  h1 {
    display: block;
    position: relative;
    width: 100%;
    font-family: var(--font-radley);
    font-size: 5.5rem;
    font-weight: 300;
    color: var(--color-text-0);
  }

  span {
    color: var(--color-text-1);
    font-weight: normal;
  }

  h2 {
    font-family: var(--font-carlito);
    font-size: 1.5rem;
    font-weight: 100;
    color: var(--color-text-0);
    max-width: 40rem;
    text-align: center;
    opacity: 0;
    transform: translateY(2rem);
    transition: opacity 1s, transform 1s;
  }

  h2.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .name {
    display: inline-block;
    position: relative;
  }

  .circle-container {
    position: absolute;
    top: 0;
    left: 7%;
    z-index: 100;
    transform: scaleX(1.3);
  }
</style>
