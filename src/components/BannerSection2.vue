<template>
  <section id="bannersection2">
    <div class="background2">
      <div class="image2"></div>
      <div class="sprite-text2">
        <h1>
          zero <br />
          limits
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
  gsap.from(".image2", {
    x: "-100%", // start completely off-screen left
    opacity: 0,
    duration: 1.5,
    scrollTrigger: {
      trigger: ".background2",
      start: "top bottom", // when the background enters the viewport
      end: "center center",
      scrub: true, // smooth scroll animation
    },
  });

  gsap.from(".sprite-text2", {
    x: "100%", // off-screen right
    opacity: 0,
    duration: 1.5,
    scrollTrigger: {
      trigger: ".background2",
      start: "top bottom",
      end: "center center",
      scrub: true,
    },
  });
});
</script>

<style scoped>
.background2 {
  display: flex;
  background-color: black;
}

.image2 {
  background-image: url("https://res.cloudinary.com/dxzt93qkk/image/upload/v1758761792/spritezero2_pmdmoy.jpg");
  min-height: 100vh;
  width: 60%;
  background-size: cover;
  background-position: center;
}

.sprite-text2 {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

h1 {
  text-transform: uppercase;
  color: white;
  text-align: center;
  font-size: 5rem;
  line-height: 1.2;
}
@media (max-width: 479px) {
  h1 {
    font-size: 2rem;
  }
  .image2 {
    min-height: 60vh;
  }
}

@media (min-width: 480px) and (max-width: 767px) {
  h1 {
    font-size: 2rem;
  }
  .image2 {
    min-height: 50vh;
  }
}

@media (min-width: 768px) and (max-width: 1023px) {
  h1 {
    font-size: 3rem;
  }
  .image2 {
    min-height: 60vh;
  }
}

@media (min-width: 1024px) and (max-width: 1439px) {
  h1 {
    font-size: 4rem;
  }
  .image2 {
    min-height: 70vh;
  }
}
</style>
