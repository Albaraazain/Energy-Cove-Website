<template>
  <div class="solarAboutWrapper">
    <div class="solarAboutContent">
      <div class="solarAboutRow" v-for="(text, index) in aboutTexts" :key="index">
        <h2 class="solarHeading">
          <span class="solarTextWrapper">
            <span class="solarText" :ref="el => textRefs[index] = el">{{ text }}</span>
            <span class="solarHighlight" :ref="el => highlightRefs[index] = el"></span>
          </span>
        </h2>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted, nextTick, inject } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

export default {
  name: 'SolarAboutSection',
  setup() {
    const aboutTexts = ref([
      "Powering sustainable futures",
      "Innovative solar solutions",
    ]);

    const textRefs = ref([]);
    const highlightRefs = ref([]);
    const lenis = inject('lenis');

    onMounted(async () => {
      await nextTick(); // Ensure all DOM elements are rendered

      textRefs.value.forEach((textEl, index) => {
        if (!textEl || !highlightRefs.value[index]) return;

        const highlightEl = highlightRefs.value[index];

        gsap.set(highlightEl, {
          width: "100%",
          height: "100%",
          scaleX: 0,
          transformOrigin: "left",
          position: "absolute",
          top: 0,
          left: 0,
          mixBlendMode: "multiply",
        });

        ScrollTrigger.create({
          trigger: textEl,
          start: "top center+=350",
          end: "bottom center-=350",
          scrub: true,
          onUpdate: (self) => {
            gsap.to(highlightEl, {
              scaleX: self.progress,
              duration: 0.1,
            });
            gsap.to(textEl, {
              color: gsap.utils.interpolate("#ffffff", "#000000", self.progress),
              duration: 0.1,
            });
          },
        });
      });

      // Header color change animation
      const solarAboutWrapper = document.querySelector('.solarAboutWrapper');
      const header = document.querySelector('.solarHeader');
      if (solarAboutWrapper && header) {
        const solarAboutWrapperHeight = solarAboutWrapper.getBoundingClientRect().height;
        const headerHeight = header.getBoundingClientRect().height;

        ScrollTrigger.create({
          trigger: '.solarAboutWrapper',
          start: `top top+=${headerHeight}`,
          end: `+=${solarAboutWrapperHeight}`,
          onUpdate: (self) => {
            const mainHeader = document.querySelector('.solarMainHeader');
            if (mainHeader) {
              mainHeader.classList.toggle('solarWhite', self.progress > 0);
            }
          },
        });
      }

      // Update ScrollTrigger when Lenis scrolls
      if (lenis) {
        lenis.on('scroll', ScrollTrigger.update);
      }
    });

    onUnmounted(() => {
      ScrollTrigger.getAll().forEach(trigger => trigger.kill());

      // Remove Lenis scroll listener
      if (lenis) {
        lenis.off('scroll', ScrollTrigger.update);
      }
    });

    return {
      aboutTexts,
      textRefs,
      highlightRefs,
    };
  }
}
</script>

<style scoped>
.solarAboutWrapper {
  margin: -40vw 0 0;
  position: relative;
  background: #000;
  padding: 34.896vw 0 9.583vw;
  z-index: 2;
}

.solarAboutContent {
  position: relative;
  padding: 0;
  text-align: left;
}

.solarAboutRow {
  position: relative;
  margin: 0 0 -1.563vw;
  overflow: hidden;
  padding: 0;
}

.solarHeading {
  color: #fff;
  font: normal 15.365vw/13.333vw Halvar;
  position: relative;
  text-transform: uppercase;
  z-index: 1;
  display: flex;
}

.solarTextWrapper {
  position: relative;
  display: inline-block;
}

.solarText {
  position: relative;
  z-index: 1;
}

.solarHighlight {
  z-index: 0;
}

@media (max-width: 760px) {
  .solarAboutWrapper {
    margin: -92vw 0 0;
    padding: 65vw 1.184vw 17px;
  }

  .solarHeading {
    font: normal 40px/40px Halvar;
    letter-spacing: -2.4px;
  }
}
</style>