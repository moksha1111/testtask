<script setup>
import { ref, onMounted, onBeforeUnmount } from "vue";
import * as THREE from "three";
const modalOpen = ref(false);

const container = ref(null);

let scene, camera, renderer, particleSphere, animationId;
const scrollY = ref(0);

onMounted(() => {
  scene = new THREE.Scene();
  camera = new THREE.PerspectiveCamera(
    75,
    window.innerWidth / window.innerHeight,
    0.1,
    1000
  );
  camera.position.z = 10;

  renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  renderer.setPixelRatio(window.devicePixelRatio);
  container.value.appendChild(renderer.domElement);

  const particleCount = 1000;
  const radius = 5;
  const geometry = new THREE.BufferGeometry();
  const positions = [];

  for (let i = 0; i < particleCount; i++) {
    const theta = Math.random() * 2 * Math.PI;
    const phi = Math.acos(2 * Math.random() - 1);
    const x = radius * Math.sin(phi) * Math.cos(theta);
    const y = radius * Math.sin(phi) * Math.sin(theta);
    const z = radius * Math.cos(phi);
    positions.push(x, y, z);
  }

  geometry.setAttribute(
    "position",
    new THREE.Float32BufferAttribute(positions, 3)
  );

  const material = new THREE.PointsMaterial({
    color: 0x00ffaa,
    size: 0.05,
    transparent: true,
    opacity: 1,
  });

  particleSphere = new THREE.Points(geometry, material);
  scene.add(particleSphere);

  const animate = () => {
    animationId = requestAnimationFrame(animate);

    const maxScroll = window.innerHeight * 1.2;
    const fadeFactor = 1 - Math.min(scrollY.value / maxScroll, 1);
    particleSphere.scale.setScalar(fadeFactor);
    particleSphere.rotation.y += 0.002;
    particleSphere.rotation.x += 0.001;

    renderer.render(scene, camera);
  };

  animate();
});
const biography = {
  description:
    "Let's put the insight, learning, and inspiration you've found here in the Hall of Zero Limits to work. To see what purpose may be calling, answer the following questions about your passions and preference. Each has only two answers, so simply choose the answer that best applies to you. Go forth; the key to discovering your gift awaits.",
};

function openModal() {
  modalOpen.value = true;
  document.body.style.overflow = "hidden";
}

function closeModal() {
  modalOpen.value = false;
  document.body.style.overflow = "";
}
</script>

<template>
  <section id="findyourgift">
    <div class="container">
      <div class="content">
        <div class="particle-bg" ref="container"></div>
        <h1 class="centered-text" @click="openModal">find <br />your gift</h1>
      </div>
      <div v-if="modalOpen" class="bio-modal" @click.self="closeModal">
        <div class="modal">
          <button class="close-btn" @click="closeModal">
            &times; close quiz
          </button>
          <div class="bio-content">
            <div class="bio">
              <div class="glow-bar top"></div>
              <h1>
                find <br />
                your gift
              </h1>
              <div class="glow-bar bottom"></div>
            </div>
            <p>{{ biography.description }}</p>
            <div>
              <div
                :class="['glow-bar-button', 'top', { hovered: quizHover }]"
              ></div>
              <button
                class="quiz"
                @mouseenter="quizHover = true"
                @mouseleave="quizHover = false"
              >
                begin quiz
              </button>
              <div
                :class="['glow-bar-button', 'bottom', { hovered: quizHover }]"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.particle-bg {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  background-color: black;
  position: absolute;
  inset: 0;
  z-index: 1;
  align-content: center;
}

canvas {
  position: fixed;
  top: 0;
  left: 0;
  z-index: -2;
}

.container {
  background-color: black;
  color: white;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  justify-content: center;
  position: relative;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}

.centered-text {
  cursor: pointer;
  position: relative;
  z-index: 2;
  color: #fff;
  font-size: 4rem;
  text-transform: uppercase;
  text-align: center;
  text-shadow: 0 0 5px #2cc713, 0 0 10px #73996d, 0 0 20px #73996d;
  cursor: pointer;
  line-height: 1.1;
  padding: 0 2rem;
  user-select: none;
}

.find-your-gift {
  margin-top: 5rem;
  color: white;
  text-align: center;
  text-transform: uppercase;
  display: grid;
  gap: 20px;
  transform: translateY(225%);
}

.find-your-gift h2 {
  font-weight: bold;
  font-size: 34px;
  text-shadow: 0 0 25px #2cc713, 0 0 25px #73996d, 0 0 25px #73996d;
}

.find-your-gift span {
  font-weight: 100;
}

.find-your-gift h3 {
  text-shadow: 0 0 5px #2cc713, 0 0 10px #73996d, 0 0 20px #73996d;
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
  max-width: 500px;
  text-align: center;
  clip-path: polygon(
    50px 0%,
    100% 0%,
    100% calc(100% - 50px),
    calc(100% - 50px) 100%,
    0% 100%,
    0% 50px
  );
}

.bio-content .bio {
  margin-top: 30px;
  margin-bottom: 30px;
}

.bio-content .glow-bar,
.glow-bar-button {
  height: 1px;
  width: 30px;
  margin: 10px auto;
  background-color: #00ff88;
  box-shadow: 0 0 5px #00ff88, 0 0 10px #00ff88;
}

.bio-content .glow-bar.top,
.glow-bar-button.top {
  margin-left: 15rem;
  transition: transform 0.3s, background-color 0.3s;
}
.bio-content .glow-bar.bottom,
.glow-bar-button.bottom {
  margin-right: 13rem;
  transition: transform 0.3s, background-color 0.3s;
}

.bio-content h1 {
  font-size: 4rem;
  text-shadow: 0 0 5px #2cc713, 0 0 10px #73996d, 0 0 20px #73996d;
  text-transform: uppercase;
  padding-right: 12px;
  padding-left: 12px;
}

.bio-content p {
  margin-bottom: 30px;
  color: silver;
}
.close-btn {
  position: absolute;
  text-transform: uppercase;
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

.quiz {
  cursor: pointer;
  text-transform: uppercase;
  border: 1px solid;
  padding: 13px 50px;
  border-radius: 5px;
  background: #3fb13f;
  transition: transform 0.5s, background-color 0.5s;
  clip-path: polygon(
    0% 0%,
    calc(118% - 50px) 0%,
    118% 50px,
    100% 100%,
    50px 175%,
    0% calc(175% - 50px)
  );
}

.quiz:hover {
  background: #c8e9c8;
}
.glow-bar-button.top.hovered {
  transform: translateX(-100px);
}
.glow-bar-button.bottom.hovered {
  transform: translateX(70px);
}
</style>
