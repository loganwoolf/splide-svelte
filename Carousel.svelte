<script>
  import { Splide, SplideSlide } from "@splidejs/svelte-splide";
  import { onMount } from "svelte";
  import "@splidejs/svelte-splide/css";
  import "./splide-override.css";

  // set up placeholder images
  let images = [];
  const url = "https://picsum.photos/800/450?random=";
  for (let i = 1; i <= 10; i++) {
    images.push(url + i);
  }

  // set up carousel config
  const mainOptions = {
    pagination: true,
    type: "loop",
  };
  const thumbsOptions = {
    arrows: false,
    focus: "center",
    gap: 5,
    isNavigation: true,
    pagination: false,
    perMove: 1,
    perPage: 4,
    type: "loop",
    updateOnMove: true,
  };

  // sync carousels
  let main;
  let thumbs;
  onMount(() => {
    if (main && thumbs) {
      console.log({ main, thumbs });
      main.sync(thumbs.splide);
    }
  });
</script>

<div class="gallery">
  <div class="gallery--main">
    <Splide 
      bind:this={main} 
      options={ mainOptions }
    >
      {#each images as imageSrc}
        <SplideSlide>
          <img src={imageSrc} alt="desc" />
        </SplideSlide>
      {/each}
    </Splide>
  </div>

  <div class="gallery--thumbs">
    <Splide 
      id="gallery--thumbs"
      bind:this={thumbs} 
      options={ thumbsOptions }
    >
      {#each images as imageSrc}
        <SplideSlide>
          <img src={imageSrc} alt="desc" />
        </SplideSlide>
      {/each}
    </Splide>
  </div>
</div>

<style>
  .gallery {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    justify-content: center;
    margin: 0 auto;
    max-width: 960px;
    min-height: 100vh;
  }
</style>