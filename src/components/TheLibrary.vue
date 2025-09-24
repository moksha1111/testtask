<script>
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import talking4 from "../assets/talking4.mp4";
import talking5 from "../assets/talking5.mp4";
import talking6 from "../assets/talking6.mp4";
gsap.registerPlugin(ScrollTrigger);

export default {
  data() {
    return {
      modalOpen: false,
      modalData: null,
      cardsInfo: [
        {
          video: talking4,
          fname: "naya",
          lname: null,
          role: "Software Engineer",
        },
        {
          video: talking5,
          fname: "reyna",
          lname: "noriega",
          role: "visual artist & author",
        },
        {
          video: talking6,
          fname: "joan ",
          lname: "marie",
          role: "space engineer",
        },
      ],
    };
  },
  mounted() {
    const cards = this.$refs.cardsGrid.querySelectorAll(".card");
    const videos = Array.isArray(this.$refs.lazyVideo)
      ? this.$refs.lazyVideo
      : [this.$refs.lazyVideo];

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          const video = entry.target;
          if (entry.isIntersecting) {
            video.play();
          } else {
            video.pause();
          }
        });
      },
      { threshold: 0.5 }
    );

    videos.forEach((video) => {
      observer.observe(video);
    });
    cards.forEach((card, index) => {
      gsap.fromTo(
        card,
        { scale: 0.8, opacity: 0, y: 50 },
        {
          scale: 1,
          opacity: 1,
          y: 0,
          duration: 2,
          delay: index * 0.1,
          ease: "power2.out",
          scrollTrigger: {
            trigger: card,
            start: "top 70%",
            end: "bottom 20%",
            toggleActions: "play none none reverse",
          },
        }
      );
    });
  },
  methods: {
    openModal(index) {
      this.modalData = this.cardsInfo[index];
      this.modalOpen = true;
      document.body.style.overflow = "hidden";
    },
    closeModal() {
      this.modalOpen = false;
      this.modalData = null;
      document.body.style.overflow = "";
    },
  },
};
</script>

<template>
  <section id="thelibrary">
    <div class="cards-container">
      <div class="cards-grid" ref="cardsGrid">
        <div
          class="card"
          v-for="(card, idx) in cardsInfo"
          :key="idx"
          :ref="'card' + idx"
          @click="openModal(idx)"
        >
          <video
            :src="card.video"
            muted
            loop
            autoplay
            preload="none"
            ref="lazyVideo"
          ></video>
          <div class="overlay">
            <h2>{{ card.fname }} <br />{{ card.lname }}</h2>
            <p>{{ card.role }}</p>
          </div>
        </div>
      </div>
      <div v-if="modalOpen" class="video-modal" @click.self="closeModal">
        <button class="close-btn" @click="closeModal">&times; close</button>
        <video
          v-if="modalData"
          :src="modalData.video"
          controls
          autoplay
          class="modal-video"
        ></video>
        <div class="modal-info" v-if="modalData">
          <h2>
            <span>{{ modalData.fname }}</span> <br />
            {{ modalData.lname }}
          </h2>
          <h3>{{ modalData.role }}</h3>
          <p>{{ modalData.phrase }}</p>
        </div>
      </div>

      <div class="the-library">
        <div class="diamond-container">
          <div class="glowing-diamond left"></div>
          <h2>
            the <br />
            <span>library</span>
          </h2>
          <div class="glowing-diamond right"></div>
        </div>

        <h3>more help finding your gift</h3>
      </div>
    </div>
  </section>
</template>

<style scoped>
.cards-container {
  padding: 2rem 2rem;
  background: #000;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  max-width: 1200px;
  width: 100%;
}

.card {
  position: relative;
  height: 650px;
  width: 400px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 30px 60px rgba(0, 0, 0, 0.7);
}

.card video {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(0.8);
  transition: filter 0.3s ease;
}

.card:hover video {
  filter: brightness(1);
}

.overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: linear-gradient(transparent, rgba(0, 0, 0, 0.9));
  padding: 2rem;
  color: white;
  transform: translateY(20px);
  transition: all 0.3s ease;
  text-align: center;
}

.card:hover .overlay {
  transform: translateY(0);
  opacity: 1;
}

.overlay h2 {
  font-size: 2.8rem;
  font-weight: 300;
  letter-spacing: 0.1em;
  margin-bottom: 0.5rem;
  text-transform: uppercase;
}

.overlay p {
  font-size: 1.1rem;
  opacity: 0.8;
  font-weight: 200;
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

.the-library {
  margin-top: 5rem;
  color: white;
  text-align: center;
  text-transform: uppercase;
  display: grid;
  gap: 20px;
}

.the-library h2 {
  font-weight: bold;
  font-size: 34px;
  text-shadow: 0 0 25px #2cc713, 0 0 25px #73996d, 0 0 25px #73996d;
}

.the-library span {
  font-weight: 100;
}

.the-library h3 {
  text-shadow: 0 0 5px #2cc713, 0 0 10px #73996d, 0 0 20px #73996d;
}

.diamond-container {
  display: flex;
  flex-wrap: wrap;
  align-content: center;
  align-items: center;
  justify-content: center;
}

.glowing-diamond {
  border: 2px solid #7ed77e;
  width: 8px;
  height: 8px;
  transform: rotate(45deg);
  animation: glow 1.5s ease-in-out infinite;
  box-shadow: 0 0 15px 3px #336033;
}

.glowing-diamond.left {
  margin-right: 60px;
}

.glowing-diamond.right {
  margin-left: 60px;
}

.video-modal {
  position: fixed;
  z-index: 9999;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
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

.modal-video {
  width: 90vw;
  max-width: 900px;
  max-height: 60vh;
  border-radius: 16px;
  background: #000;
  margin-bottom: 2rem;
}

.modal-info {
  color: #fff;
  text-align: center;
  line-height: 2rem;
}

.modal-info h2 {
  text-transform: uppercase;
  font-weight: 100;
}

.modal-info h2 span {
  font-weight: 900;
}

.modal-info h3 {
  text-transform: uppercase;
  font-weight: 300;
  font-size: 14px;
}

.modal-info p {
  color: #2df872;
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
</style>
