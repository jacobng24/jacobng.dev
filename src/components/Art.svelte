<script lang="ts">
  import { fly } from "svelte/transition";
  import { quintOut } from "svelte/easing";
  import FlyIn from "./FlyIn.svelte";
  import Button from "./Button.svelte";
  import { images } from "./images";
  import Photo1 from "../images/Photo1.webp";
  import Photo2 from "../images/Photo2.webp";
  import Photo3 from "../images/Photo3.webp";
  import { galleryOpen } from "./gallery";

  let selectedIndex = 0;
</script>

<FlyIn>
  <div class="" id="art">
    <div
      id="artContent"
      in:fly={{ easing: quintOut, duration: 1000, delay: 200 }}
    >
      <div class="artTextSide">
        <div class="blurbcontainer">
          <section class="blurb" style="font-size: 18px">
            <span class=" text-l hubot" style="color: var(--jpurple)"
              >Photography :D</span
            >
            <br />Here are the photos and creations that I have produced over
            the past four years! <br /><br />Shot with a Canon Rebel XT, Nikon
            D750, and through many other mediums! Edited with Photoshop.<br
            /><br /> P.S. there is also a Google Drive link if you want to see more!
          </section>
        </div>
        <a
          href="https://drive.google.com/drive/folders/1UBavS5fYbSiJJTOMsAZxW_llEihR1c6T?usp=drive_link"
        >
          <button id="seeMoreButton" class="seeMoreButton"> See More</button>
        </a>
      </div>
      <div class="artContainer">
        <div class="image-stack">
          <div class="image-stack__item artImage-top">
            <img src={Photo2.src} alt="sad" class="artImage" />
          </div>
          <div class="image-stack__item artImage-bottom">
            <img src={Photo1.src} alt="happy" class="artImage" />
          </div>
          <div class="image-stack__item artImage-side">
            <img src={Photo3.src} alt="hi" class="artImage" />
          </div>
        </div>
      </div>
    </div>
  </div>
  <div id="imageGallery" class:none={!$galleryOpen}>
    <div class="popup">
      <button id="closeButton" on:click={() => ($galleryOpen = false)}>
        Close
      </button>
      <ul>
        {#each images as image, i}
          <!-- Add more images as needed -->
          <li>
            <img
              src={image.url}
              alt={image.alt}
              class="artimage"
              class:none={selectedIndex % images.length !== i}
            />
          </li>
        {/each}
      </ul>
      <div class="navigation">
        <button on:click={() => (selectedIndex -= 1)}>Previous</button>
        <button on:click={() => (selectedIndex += 1)}>Next</button>
      </div>
    </div>
  </div>

  <div in:fly={{ easing: quintOut, duration: 1000, delay: 200 }}>
    <Button number={4} className={"margin"} />
  </div>
</FlyIn>

<style>
  .none {
    display: none;
  }
</style>
