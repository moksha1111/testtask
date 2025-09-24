<script setup>
import { ref } from "vue";
const quizHover = ref(false);

const modalOpen = ref(false);

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
      <div class="content" @click="openModal">
        <h1>find <br />your gift</h1>
      </div>
      <div class="find-your-gift">
        <div class="diamond-container">
          <div class="glowing-diamond left"></div>
          <h2>
            find your <br />
            <span>gift</span>
          </h2>
          <div class="glowing-diamond right"></div>
        </div>

        <h3>quiz experience</h3>
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
.container {
  background-color: black;
  color: white;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  justify-content: center;
}

.content h1 {
  text-transform: uppercase;
  cursor: pointer;
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
    /* Top-left inward cut */ 100% 0%,
    /* Top-right */ 100% calc(100% - 50px),
    /* Before bottom-right cut */ calc(100% - 50px) 100%,
    /* Bottom-right inward cut */ 0% 100%,
    /* Bottom-left */ 0% 50px /* Back to top-left vertical */
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
    /* Top-left */ calc(118% - 50px) 0%,
    /* Top-right inward cut */ 118% 50px,
    /* Down to complete top-right cut */ 100% 100%,
    /* Bottom-right */ 50px 175%,
    /* Bottom-left inward cut */ 0% calc(175% - 50px)
      /* Up to complete bottom-left cut */
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
