<template>
  <section id="bannersection1">
    <div class="background">
      <div class="image"></div>
      <div class="sprite-text">
        <h1>
          infinite <br />
          potential
        </h1>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from "vue";
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

onMounted(() => {
  gsap.from(".image", {
    x: "-100%", // start completely off-screen left
    opacity: 0,
    duration: 1.5,
    scrollTrigger: {
      trigger: ".background",
      start: "top bottom", // when the background enters the viewport
      end: "center center",
      scrub: true, // smooth scroll animation
    },
  });

  gsap.from(".sprite-text", {
    x: "100%", // off-screen right
    opacity: 0,
    duration: 1.5,
    scrollTrigger: {
      trigger: ".background",
      start: "top bottom",
      end: "center center",
      scrub: true,
    },
  });
});
</script>

<style scoped>
.background {
  display: flex;
  background-color: black;
}
.image {
  background-image: url("https://res.cloudinary.com/dxzt93qkk/image/upload/v1758761791/spritezero_dha4ad.jpg");
  min-height: 100vh;
  width: 60%;
  background-size: cover;
}

h1 {
  text-transform: uppercase;
  color: white;
  text-align: center;
  align-content: center;
  width: 100%;
  height: 100%;
  font-size: 5rem;
}

@media (max-width: 479px) {
  h1 {
    font-size: 1rem;
  }
  .image {
    min-height: 34vh;
  }
}

@media (min-width: 480px) and (max-width: 767px) {
  h1 {
    font-size: 2rem;
  }
  .image {
    min-height: 50vh;
  }
}

@media (min-width: 768px) and (max-width: 1023px) {
  h1 {
    font-size: 3rem;
  }
  .image {
    min-height: 60vh;
  }
}

@media (min-width: 1024px) and (max-width: 1439px) {
  h1 {
    font-size: 4rem;
  }
  .image {
    min-height: 70vh;
  }
}
</style>
