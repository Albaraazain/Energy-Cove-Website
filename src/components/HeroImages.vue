<template>
  <div class="solarHeroSection" ref="solarHeroSection">
    <img src="./img-2024/Solar energy bubble left.png" width="991" height="1503" alt="Solar Energy Bubble Left" class="solarBubbleLeft" ref="solarBubbleLeft">
    <img src="./img-2024/solar%20energy%20bubble%20right.png" width="1197" height="1740" alt="Solar Energy Bubble Right" class="solarBubbleRight" ref="solarBubbleRight">
    <img src="./img-2024/Solar energy bubble left.png" width="477" height="529" alt="Solar Energy Bubble Left Mobile" class="solarBubbleLeftMobile" ref="solarBubbleLeftMobile">
    <img src="./img-2024/solar%20energy%20bubble%20right.png" width="576" height="837" alt="Solar Energy Bubble Right Mobile" class="solarBubbleRightMobile" ref="solarBubbleRightMobile">
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted, inject } from 'vue';
import { gsap } from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

export default {
  name: 'SolarHeroImages',
  setup() {
    const solarHeroSection = ref(null);
    const solarBubbleLeft = ref(null);
    const solarBubbleRight = ref(null);
    const solarBubbleLeftMobile = ref(null);
    const solarBubbleRightMobile = ref(null);
    const lenis = inject('lenis');

    let tlSolarHero, tlSolarHero2;

    onMounted(() => {
      if (!solarHeroSection.value || !solarBubbleLeft.value || !solarBubbleRight.value || !solarBubbleLeftMobile.value || !solarBubbleRightMobile.value) return;

      const solarHeroSectionTop = solarHeroSection.value.getBoundingClientRect().top;
      const trSolarHero = document.querySelector("#tr_solar_hero");
      if (!trSolarHero) {
        console.warn('Element #tr_solar_hero not found');
        return;
      }
      const trSolarHeroTop = parseFloat(window.getComputedStyle(trSolarHero).getPropertyValue("top"));

      const h = window.innerHeight;

      if (window.innerWidth > 760) {
        tlSolarHero = gsap.timeline({
          scrollTrigger: {
            id: "tlSolarHero",
            trigger: solarHeroSection.value,
            start: `top top+=${solarHeroSectionTop}`,
            end: `+=${trSolarHeroTop}`,
            pin: false,
            scrub: true,
            pinSpacing: false,
          }
        });
        tlSolarHero
            .add('d')
            .to(solarBubbleLeft.value, {x: -50, y: 0, ease: 'none'}, 'd')
            .to(solarBubbleRight.value, {x: -52, y: 0, ease: 'none'}, 'd');

        tlSolarHero2 = gsap.timeline({
          scrollTrigger: {
            id: "tlSolarHero2",
            trigger: "#tr_solar_hero",
            start: `top top`,
            end: `+=${h * 1.45}`,
            pin: false,
            scrub: true,
            pinSpacing: false,
          }
        });
        tlSolarHero2
            .add('dx')
            .to(solarBubbleLeft.value, {x: -278, y: -350, ease: 'none'}, 'dx')
            .to(solarBubbleRight.value, {x: -240, y: -250, ease: 'none'}, 'dx')
            .to('.solarAboutTextWrap', {marginTop: '-57.292vw', ease: 'none'}, 'dx');
      } else {
        tlSolarHero = gsap.timeline({
          scrollTrigger: {
            id: "tlSolarHero",
            trigger: solarHeroSection.value,
            start: `top top+=${solarHeroSectionTop}`,
            end: `+=${h * 2}`,
            pin: false,
            scrub: true,
            pinSpacing: false,
          }
        });
        tlSolarHero
            .add('d')
            .to(solarBubbleLeftMobile.value, {x: -250, ease: 'none'}, 'd')
            .to(solarBubbleRightMobile.value, {x: -250, ease: 'none'}, 'd');
      }

      // Update ScrollTrigger when Lenis scrolls
      if (lenis) {
        lenis.on('scroll', ScrollTrigger.update);
      }
    });

    onUnmounted(() => {
      // Clean up ScrollTrigger instances
      if (tlSolarHero && tlSolarHero.scrollTrigger) tlSolarHero.scrollTrigger.kill();
      if (tlSolarHero2 && tlSolarHero2.scrollTrigger) tlSolarHero2.scrollTrigger.kill();

      // Remove Lenis scroll listener
      if (lenis) {
        lenis.off('scroll', ScrollTrigger.update);
      }
    });

    return {
      solarHeroSection,
      solarBubbleLeft,
      solarBubbleRight,
      solarBubbleLeftMobile,
      solarBubbleRightMobile
    };
  }
}
</script>

<style scoped>
@media (min-width: 320px) {
  *, ::after, ::before {
    outline: 0;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  img {
    vertical-align: middle;
    border: 0;
    -ms-interpolation-mode: bicubic;
    height: auto;
    max-width: 100%;
    border-style: none;
  }

  .solarHeroSection {
    position: relative;
    height: 107.552vw;
    z-index: 20;
  }

  .solarHeroSection .solarBubbleLeft {
    position: absolute;
    top: 15vw;
    left: 0;
    display: block;
    width: 51.615vw;
  }

  .solarHeroSection .solarBubbleRight {
    position: absolute;
    top: 0;
    right: -10.938vw;
    display: block;
    width: 62.344vw;
  }

  .solarHeroSection .solarBubbleLeftMobile, .solarHeroSection .solarBubbleRightMobile {
    display: none;
  }

  @media (max-width: 760px) {
    .solarHeroSection {
      height: 100vh;
      height: 305.667vw;
    }

    .solarHeroSection .solarBubbleLeft {
      top: 573px;
      left: -37px;
      width: 80vw;
      height: 121vw;
      -o-object-fit: cover;
      object-fit: cover;
      display: none;
    }

    .solarHeroSection .solarBubbleRight {
      top: 30.395vw;
      right: -39.868vw;
      width: 75.789vw;
      height: 110.132vw;
      display: none;
    }

    .solarHeroSection .solarBubbleLeftMobile, .solarHeroSection .solarBubbleRightMobile {
      display: block;
      position: absolute;
    }

    .solarHeroSection .solarBubbleLeftMobile {
      top: 152.533vw;
      left: -10.933vw;
      width: 127.2vw;
      height: 151.733vw;
      -o-object-fit: cover;
      object-fit: cover;
    }

    .solarHeroSection .solarBubbleRightMobile {
      top: 87.733vw;
      right: -70.667vw;
      width: 153.6vw;
      height: 145.6vw;
      -o-object-fit: cover;
      object-fit: cover;
    }
  }
}
</style>