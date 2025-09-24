<script>
import dora from "../assets/dora.jpg";
import shuri from "../assets/shuri.jpg";
import mbaku from "../assets/mbaku.jpg";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);

export default {
  data() {
    return {
      cards: [
        {
          img: dora,
          name: "dora milaje",
          bio: "“i am loyal to that throne, no matter who sits on it.”",
          description:
            "Much can be gleaned from these elites warriors who provide protection and intel to protect the crown and country. Though known for being physically skilled in battle, their minds are also among their greatest weapons-overcoming and embracing adversity and solving problems as quickly as they arise. Do the Dora's gifts reflect yours?",
        },
        {
          img: shuri,
          name: "shuri",
          bio: "“just because something works doesn't mean it can't be improved.”",
          description:
            "Both a problem solver and maker by nature, Shuri is a visionary, illuminator, decoder, exlplorer and avant-garde. She's unapologetically bold in her role as a leader across the board- as a master engineer, designer, tech inventor, mathematician, and scientist. Her innovations are of incredible importance to her community. Perhaps when you look at Shuri, you see glimpses of yourself there as well.",
        },
        {
          img: mbaku,
          name: "m'baku",
          bio: "“witness the strength of the jabari... first-hand!.”",
          description:
            "Behold the gifts of a great leader: determination, courage, and passion. M'Baku's superhuman physical agility and strength are particularly impressive when combined with his supererior mental agility-strategic, analytical, patient, and tenacious when met with obstacles. Do you think these characteristics would serve you well?",
        },
      ],
      modalOpen: false,
      selectedCard: {},
    };
  },
  methods: {
    openModal(idx) {
      this.selectedCard = this.cards[idx];
      this.modalOpen = true;
      document.body.style.overflow = "hidden";
    },
    closeModal() {
      this.modalOpen = false;
      this.selectedCard = {};
      document.body.style.overflow = "";
    },
  },
  mounted() {
    const lazyCards = this.$el.querySelectorAll(".lazy-bg");

    const observer = new IntersectionObserver(
      (entries, obs) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            const el = entry.target;
            const bg = el.dataset.bg;
            if (bg) {
              el.style.backgroundImage = `url(${bg})`;
              el.classList.remove("lazy-bg");
              obs.unobserve(el); // stop watching after load
            }
          }
        });
      },
      { threshold: 0.2 }
    );

    lazyCards.forEach((card) => observer.observe(card));
    gsap.utils.toArray(".statue-card").forEach((card, i) => {
      gsap.from(card, {
        skewX: 20,
        x: -100,
        opacity: 0,
        scale: 0.8, // start smaller
        duration: 2,
        ease: "power3.out",
        scrollTrigger: {
          trigger: card,
          start: "top 70%",
          end: "bottom 50%",
          toggleActions: "play none none reverse",
        },
      });
    });
  },
};
</script>

<template>
  <section id="inspirationgarden">
    <div class="cards-container">
      <div class="cards-grid">
        <div
          v-for="(card, idx) in cards"
          :key="idx"
          class="statue-card lazy-bg"
          :data-bg="card.img"
          @click="openModal(idx)"
        ></div>
      </div>
      <div v-if="modalOpen" class="bio-modal" @click.self="closeModal">
        <button class="close-btn" @click="closeModal">
          &times; clsoe quote
        </button>
        <div class="bio-content" :data-card="selectedCard.id">
          <div class="bio">
            <div class="glow-bar top"></div>
            <h1>{{ selectedCard.bio }}</h1>
            <div class="glow-bar bottom"></div>
          </div>

          <h2>{{ selectedCard.name }}</h2>
          <div class="container">
            <div class="glowing-ring"></div>
          </div>
          <p>{{ selectedCard.description }}</p>
        </div>
      </div>

      <div class="inspirationGarden">
        <div class="diamond-container">
          <div class="glowing-diamond left"></div>
          <h2>
            inspiration <br />
            <span>garden</span>
          </h2>
          <div class="glowing-diamond right"></div>
        </div>

        <h3>where ingenuity overflows</h3>
      </div>
    </div>
  </section>
</template>

<style scoped>
.cards-container {
  padding: 8rem 2rem 2rem;
  background: #000;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 2rem;
  max-width: 1200px;
  width: 100%;
}

.statue-card {
  position: relative;
  height: 650px;
  width: 400px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
  transition: all 0.3s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  background-size: cover;
  background-position: center;
  cursor: pointer;
}

.statue-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 30px 60px rgba(0, 0, 0, 0.7);
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
}

.bio-content .glow-bar {
  height: 1px;
  width: 30px;
  margin: 10px auto;
  background-color: #00ff88;
  box-shadow: 0 0 5px #00ff88, 0 0 10px #00ff88;
}

.bio-content .glow-bar.top {
  margin-left: 100px;
}
.bio-content .glow-bar.bottom {
  margin-right: 165px;
}

.bio-content h1 {
  text-shadow: 0 0 5px #2cc713, 0 0 10px #73996d, 0 0 20px #73996d;
  text-transform: uppercase;
  padding-right: 12px;
  padding-left: 12px;
}

.bio-content h2 {
  text-transform: uppercase;
  font-size: 15px;
  margin-top: 40px;
}

.bio-content .container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.bio-content .container .glowing-ring {
  width: 10px;
  height: 10px;
  border: 2px solid white;
  border-radius: 50%;
  animation: glow 1.5s ease-in-out infinite;
  box-shadow: 0 0 4px 0px white;
  margin-top: 30px;
  margin-bottom: 30px;
}

.bio-content p {
  margin-bottom: 30px;
  color: silver;
  padding-right: 20px;
  padding-left: 20px;
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

.inspirationGarden {
  margin-top: 5rem;
  color: white;
  text-align: center;
  text-transform: uppercase;
  display: grid;
  gap: 20px;
}

.inspirationGarden h2 {
  font-weight: bold;
  font-size: 34px;
  text-shadow: 0 0 25px #2cc713, 0 0 25px #73996d, 0 0 25px #73996d;
}

.inspirationGarden span {
  font-weight: 100;
}

.inspirationGarden h3 {
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

@media (max-width: 479px) {
  .cards-grid {
    width: 96%;
  }

  .bio-content {
    max-width: 400px;
  }
}

@media (min-width: 480px) and (max-width: 767px) {
  .cards-grid {
    width: 57%;
  }
}

@media (min-width: 768px) and (max-width: 1023px) {
  .cards-grid {
    width: 87%;
  }
}

@media (min-width: 1024px) and (max-width: 1439px) {
}
</style>
