<script setup>
import { onMounted, onBeforeUnmount } from "vue";
import { ref } from "vue";
const modalOpen = ref(false);
function closeModal() {
  modalOpen.value = false;
  document.body.style.overflow = "";
}
function scrollToSection(sectionId) {
  const el = document.getElementById(sectionId);
  if (el) {
    el.scrollIntoView({ behavior: "smooth" });
    modalOpen.value = false;
    document.body.style.overflow = "";
  }
}
let text, leaf, hill1, hill4, hill5;
let handleScroll;

onMounted(() => {
  text = document.getElementById("text");
  leaf = document.getElementById("leaf");
  hill1 = document.getElementById("hill1");
  hill4 = document.getElementById("hill4");
  hill5 = document.getElementById("hill5");

  handleScroll = () => {
    var value = window.scrollY;
    text.style.marginTop = value * 2.5 + "px";
    leaf.style.top = value * -1 + "px";
    leaf.style.left = value * 1 + "px";
    hill5.style.left = value * 1 + "px";
    hill4.style.left = value * -1 + "px";
    hill1.style.top = value * 1 + "px";
  };

  window.addEventListener("scroll", handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener("scroll", handleScroll);
});
</script>

<template>
  <div class="text">
    <img src="../assets/spritelogo.png" alt="" />
    <img src="../assets/wakandalogo.png" alt="" />
    <h2>Sprite Zero Sugar<span class="small"> Ⓡ </span>| ⓒ MARVEL</h2>
  </div>
  <section id="welcome">
    <div class="particle-bg" ref="container">
      <nav class="navbar">
        <div class="title">
          <span>the</span> hall <span>of</span> <br />
          zero limits
        </div>
        <button
          class="hamburger"
          @click="modalOpen = true"
          aria-label="Open menu"
        >
          <span></span>
          <span></span>
          <span></span>
        </button>
      </nav>

      <div v-if="modalOpen" class="bio-modal" @click.self="closeModal">
        <button class="close-btn" @click="closeModal">
          &times; close menu
        </button>
        <div class="bio-content">
          <h2 class="menu">Menu</h2>
          <ul class="menu-links">
            <li>
              <a @click="scrollToSection('welcome')"> Welcome </a>
            </li>
            <li>
              <a @click="scrollToSection('originstories')"> Origin Stories </a>
            </li>
            <li>
              <a @click="scrollToSection('bannersection1')"> Banner </a>
            </li>
            <li>
              <a @click="scrollToSection('inspirationgarden')">
                Inspiration Garden
              </a>
            </li>
            <li>
              <a @click="scrollToSection('spritezerosugar')">
                Sprite Zero Sugar<span class="small">Ⓡ</span>
              </a>
            </li>
            <li>
              <a @click="scrollToSection('bannersection2')"> Banner </a>
            </li>
            <li>
              <a @click="scrollToSection('thelibrary')"> The Library </a>
            </li>
            <li>
              <a @click="scrollToSection('findyourgift')"> Find Your Gift </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>

  <div class="parralax">
    <img src="../assets/hill1.png" id="hill1" />
    <img src="../assets/hill2.png" id="hill2" />
    <img src="../assets/hill3.png" id="hill3" />
    <img src="../assets/hill4.png" id="hill4" />
    <img src="../assets/hill5.png" id="hill5" />
    <img src="../assets/tree.png" id="tree" />
    <h2 class="welcomemsg" id="text">
      exlpore new paths <br />
      find your gift
    </h2>
    <img src="../assets/leaf.png" id="leaf" />
    <img src="../assets/plant.png" id="plant" />
  </div>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  padding: 20px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  z-index: 10;
  background: transparent;
  color: white;
  font-family: sans-serif;
}
.title {
  text-transform: uppercase;
  font-size: 2em;
  color: #fff;
  letter-spacing: 4px;
  text-align: center;
  line-height: 1.2;
  text-shadow: 0 0 5px #2cc713, 0 0 10px #73996d, 0 0 20px #73996d;
}
.title span:nth-child(1) {
  font-size: 15px;
  vertical-align: super;
}

.title span:nth-child(2) {
  font-size: 15px;
  vertical-align: baseline;
}
.bio-modal {
  position: fixed;
  z-index: 9999;
  inset: 0;
  background: rgb(0 0 0 / 52%);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  animation: fadeIn 0.3s;
}
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
.bio-content {
  background: #222222d1;
  color: #fff;
  padding: 2rem 3rem;
  border-radius: 16px;
  width: 20%;
  clip-path: polygon(
    50px 0%,
    100% 0%,
    100% calc(100% - 50px),
    calc(100% - 50px) 100%,
    0% 100%,
    0% 50px
  );
}

.bio-content .menu {
  text-align: center;
}
.close-btn {
  text-transform: uppercase;
  position: absolute;
  top: 2rem;
  right: 2rem;
  font-size: 1rem;
  background: none;
  border: none;
  color: #fff;
  cursor: pointer;
  z-index: 10001;
  transition: color 0.2s;
}
.close-btn:hover {
  color: rgb(123, 255, 123);
}
.menu-links {
  line-height: 2rem;
  list-style: none;
  padding: 0;
  margin: 2rem 0 0 0;
}
.menu-links li {
  margin: 1rem 0;
}
.menu-links a {
  cursor: pointer;
  color: #00ff88;
  text-decoration: none;
  font-size: 1.2rem;
  transition: color 0.2s;
}
.menu-links a:hover {
  color: #fff;
}
.hamburger {
  width: 40px;
  height: 40px;
  background: none;
  border: 2px solid white;
  border-radius: 5px;
  z-index: 20;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  gap: 6px;
  transition: background-color 0.3s;
}

.hamburger:hover {
  background-color: #00ff88;
}
.hamburger span {
  display: block;
  width: 30px;
  height: 2px;
  background: #fff;
  border-radius: 2px;
  transition: all 0.3s;
}
span.small {
  font-size: 10px;
  vertical-align: super;
}

.text {
  display: flex;
  align-items: center;
  position: fixed;
  right: 30px;
  bottom: 30px;
  color: white;
  font-size: 0.5rem;
  font-weight: bold;
  letter-spacing: 2px;
  z-index: 10000;
  pointer-events: none;
  user-select: none;
}

.text img {
  width: 55px;
}

.parralax {
  overflow: hidden;
  position: relative;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.parralax h2 {
  position: absolute;
  font-size: 7rem;
  color: white;
  z-index: 99;
  text-transform: uppercase;
  text-align: center;
  text-shadow: 0 0 5px #1a564b, 0 0 10px #1a564b, 0 0 20px #1a564b;
}

.parralax img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  pointer-events: none;
}

@media (max-width: 479px) {
  .parralax {
    min-height: 32vh;
  }

  .parralax h2 {
    font-size: 2rem;
  }

  .title {
    font-size: 1rem;
  }

  .title span:nth-child(1),
  .title span:nth-child(2) {
    font-size: 8px;
  }

  .bio-content {
    width: 70%;
  }
}

@media (min-width: 480px) and (max-width: 767px) {
  .parralax {
    min-height: 52vh;
  }

  .parralax h2 {
    font-size: 3rem;
  }

  .bio-content {
    width: 45%;
  }
}

@media (min-width: 768px) and (max-width: 1023px) {
  .parralax {
    min-height: 70vh;
  }

  .parralax h2 {
    font-size: 4rem;
  }

  .bio-content {
    width: 35%;
  }
}

@media (min-width: 1024px) and (max-width: 1439px) {
  .parralax {
    min-height: 70vh;
  }

  .parralax h2 {
    font-size: 5rem;
  }

  .bio-content {
    width: 30%;
  }
}
</style>
