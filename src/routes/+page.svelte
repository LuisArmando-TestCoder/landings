<script lang="ts">
  // .

  let loadingScreen: HTMLElement;

  import playVideo from "./scripts/play-video";
  import { setScrollingEffects } from "./scripts/scrolling-effects";

  // .

  let heroBannerVideo: HTMLVideoElement;
  let gridVideos: HTMLVideoElement[] = [];

  import { onMount } from "svelte";
  import {
    changeHeightOnScroll,
    changeOpacityOnScroll,
    changePositionOnScroll,
    changeSkewOnScroll,
  } from "./scripts/scrolling-effects/effects";

  const SA: HTMLElement[] = [];
  const SB: HTMLElement[] = [];
  const SC: HTMLElement[] = [];

  onMount(() => {
    setEffects();
  });

  function setEffects() {
    setScrollingEffects(SA, [changeOpacityOnScroll, changePositionOnScroll]);
    setScrollingEffects(SB, [changeOpacityOnScroll]);
    setScrollingEffects(SC, [
      changeOpacityOnScroll,
      changeSkewOnScroll,
      changePositionOnScroll,
    ]);
    setScrollingEffects(gridVideos, [changeHeightOnScroll]);
  }

  // .

  // onMount(() => {
  //   // Add this function to your code
  //   function addScrollAcceleration() {
  //     let lastScrollPosition = 0;
  //     let peakAcceleration = 20;
  //     let accelerationFactor = peakAcceleration; // Adjust this value to control the acceleration

  //     // Calculate the scroll direction
  //     let scrollDirection = 0;

  //     function handleScroll() {
  //       // Apply acceleration

  //       accelerationFactor = Math.round((accelerationFactor / 2) * 1000) / 1000;

  //       if (accelerationFactor)
  //         window.scrollY =
  //           window.scrollY + scrollDirection * accelerationFactor;
  //     }

  //     // Attach the scroll event listener
  //     window.addEventListener("scroll", handleScroll);
  //     window.addEventListener("scrollend", () => {
  //       accelerationFactor = peakAcceleration;
  //       scrollDirection = Math.sign(lastScrollPosition - window.scrollY);
  //       lastScrollPosition = window.scrollY;
  //       console.log("scrollDirection", scrollDirection);
  //     });
  //   }

  //   // Call the function to enable scroll acceleration
  //   addScrollAcceleration();
  // });

  let isMenuOpen: boolean;

  let progressValueElement: HTMLElement;
  let progressBarElement: HTMLElement;
  let progressValue = 1;
  let hasLoadingHadInteraction: boolean;

  onMount(() => {
    hasLoadingHadInteraction = false;

    (function frame() {
      progressBarElement.style.width = `${progressValue}%`;
      console.log(progressValue);

      if ((progressValue += 1.5) > 100) return;

      requestAnimationFrame(frame);
    })();
  });
</script>

<svelte:window
  on:mouseover={() => {
    [...gridVideos, heroBannerVideo].forEach((video) => {
      playVideo(video)();
    });
  }}
/>

<!-- svelte-ignore a11y-no-static-element-interactions -->
<div
  bind:this={loadingScreen}
  on:click={() => {
    console.log("click!");
    hasLoadingHadInteraction = true;
  }}
  on:keydown={() => {
    console.log("key down!");
    hasLoadingHadInteraction = true;
  }}
  aria-pressed={hasLoadingHadInteraction}
  class="loading-screen {progressValue >= 100 && hasLoadingHadInteraction
    ? 'open'
    : 'closed'}"
>
  <p>loading</p>
  <br />
  <div
    bind:this={progressBarElement}
    class="loading-screen__progress-bar-wrapper"
  >
    <hr
      class="loading-screen__progress-bar {progressValue >= 100 && 'pulse'}"
    />
  </div>
  <br />
  <h2 bind:this={progressValueElement} class="loading-screen__progress">
    {Math.floor(progressValue - 1)}%
  </h2>
</div>

<input bind:checked={isMenuOpen} class="ham-trigger" type="checkbox" />

<nav class="menu {isMenuOpen ? '' : 'hide-on-menu-open'}">
  <ul class="menu__list">
    <li class="menu__list-item">
      <a class="menu__anchor" href="/"><p>Home</p></a>
    </li>
    <li class="menu__list-item">
      <a class="menu__anchor" href="#about"><p>About</p></a>
    </li>
    <li class="menu__list-item">
      <a class="menu__anchor" href="#contact"><p>Services</p></a>
    </li>
    <!-- Add more menu items as needed -->
  </ul>
</nav>

<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
<main
  class="visible-when-ready squishable {progressValue >= 100 &&
    hasLoadingHadInteraction &&
    'show'} {isMenuOpen && 'squish-on-open-menu'}"
>
  <!-- svelte-ignore a11y-media-has-caption -->
  <video
    loop
    bind:this={heroBannerVideo}
    class="hero-banner-video {isMenuOpen ? 'squish-on-open-menu' : ''}"
    src="/videos/7946009-uhd_1440_2732_30fps.mp4"
  ></video>

  <div class="hero-container">
    <h1>
      <div bind:this={SA[SA.length]}>soft</div>
      <div bind:this={SA[SA.length]}>smooth</div>
      <div bind:this={SA[SA.length]}>& tasty</div>
    </h1>

    <h2 bind:this={SB[SB.length]}>Libre Baskervile</h2>
  </div>

  <div class="body-container bg" id="about">
    <div class="container grid-2">
      <div class="info">
        <h3 bind:this={SA[SA.length]}>
          Nihil ullam id explicabo aperiam voluptas
        </h3>
        <p bind:this={SB[SB.length]}>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Nulla nostrum
          eveniet similique nihil ullam id explicabo aperiam voluptas. A,
          dolorum itaque minus deleniti facilis rerum suscipit fugiat distinctio
          ipsam recusandae.
        </p>
      </div>
      <!-- svelte-ignore a11y-media-has-caption -->
      <div bind:this={SA[SA.length]} class="video-container">
        <video
          loop
          bind:this={gridVideos[0]}
          class="grid-video"
          src="/videos/5353260-hd_1080_1920_25fps.mp4"
        ></video>
      </div>
    </div>
    <div class="container grid-2">
      <!-- svelte-ignore a11y-media-has-caption -->
      <div bind:this={SA[SA.length]} class="video-container">
        <video
          loop
          bind:this={gridVideos[1]}
          class="grid-video"
          src="/videos/5353381-hd_1080_1920_25fps.mp4"
        ></video>
      </div>
      <div class="info">
        <h3 bind:this={SA[SA.length]}>Adipisicing elit earum!</h3>
        <p bind:this={SB[SB.length]}>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Laboriosam
          corrupti nam placeat excepturi molestiae minus, autem cumque amet
          repellendus quia, sint deleniti nostrum eligendi dolores,
          necessitatibus soluta eum dicta aliquid.
          <br /><br />
          Soluta doloribus, numquam perspiciatis unde debitis vel eveniet reiciendis
          autem reprehenderit quia est cumque? Sed veritatis velit impedit dolorem
          aliquid unde ducimus atque tempore amet voluptas, modi labore magnam. Aut.
        </p>
      </div>
    </div>
    <div class="container grid-2">
      <div class="info">
        <h3 bind:this={SA[SA.length]}>Distinctio ipsam recusandae</h3>
        <p bind:this={SB[SB.length]}>
          Lorem, ipsum dolor sit amet consectetur adipisicing elit. Praesentium
          possimus perspiciatis totam, laudantium officia doloremque eligendi
          voluptate beatae deserunt dicta enim autem cum hic quod delectus
          recusandae excepturi laborum nam?
          <br /><br />
          Sapiente totam porro architecto assumenda. Facere ducimus enim eum eaque
          ipsa cupiditate, molestias quia qui praesentium dolorum iusto pariatur
          vitae molestiae at quos, totam id ad nobis magnam. Similique, et!
          <br /><br />
          Quod temporibus reprehenderit sapiente eum ex, ut harum quia distinctio
          similique sunt omnis, unde eius. Tempore debitis laborum natus alias, quo
          laboriosam vero libero praesentium beatae rem reiciendis, repellat blanditiis.
          <br /><br />
          Lorem ipsum dolor, sit amet consectetur adipisicing elit. Vero soluta in,
          dolores quam fugit temporibus! Quaerat fuga inventore dolore laudantium
          nostrum, consequatur, explicabo consectetur veritatis alias optio nemo
          animi tempora?
          <br /><br />
          Culpa voluptatem ea quae doloribus, temporibus a fuga quo! Nisi neque numquam
          nulla suscipit architecto quod aliquam praesentium culpa minima tempora,
          odio qui eveniet delectus aperiam magnam quisquam! Accusantium, nemo.
        </p>
      </div>
      <!-- svelte-ignore a11y-media-has-caption -->
      <div bind:this={SA[SA.length]} class="video-container">
        <video
          loop
          bind:this={gridVideos[2]}
          class="grid-video"
          src="/videos/5353382-hd_1080_1920_25fps.mp4"
        ></video>
      </div>
    </div>
  </div>

  <footer id="contact">
    <h3 bind:this={SC[SC.length]}>Contact us:</h3>
    <hr />
    <div class="contact-info">
      <div class="contact-info__info">
        <p bind:this={SC[SC.length]}>
          <b>Email:</b> <a href="mailto:info@example.com">info@example.com</a>
        </p>
        <p bind:this={SC[SC.length]}><b>Phone:</b> +1 (123) 456-7890</p>
      </div>
      <div class="contact-info__info">
        <p bind:this={SC[SC.length]}>
          &copy; 2024 My Website. All rights reserved.
        </p>
      </div>
    </div>
  </footer>
</main>

<style type="scss">
  @import "./styles/reset.scss";
  @import "./styles/global.scss";
  @import "./styles/menu.scss";
  @import "./styles/loading-screen.scss";
</style>
