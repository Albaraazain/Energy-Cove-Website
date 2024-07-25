<template>
  <div class="ec-services-text">
    <div class="ec-title-container">
      <div class="ec-title ec-title-desktop ec-fade-up" :style="animationStyle">
        <span class="ec-title-line ec-line-1">We focus on providing innovative solar</span>
        <span class="ec-title-line ec-line-2">and renewable energy solutions that effectively meet</span>
        <span class="ec-title-line ec-line-3">our clients' energy needs</span>
      </div>
      <div class="ec-title ec-title-mobile ec-fade-up" :style="animationStyle">
        <span class="ec-title-line ec-line-1">We focus on providing innovative</span>
        <span class="ec-title-line ec-line-2">solar and renewable energy</span>
        <span class="ec-title-line ec-line-3">solutions that effectively meet our</span>
        <span class="ec-title-line ec-line-4">clients' energy needs</span>
      </div>
    </div>
    <div class="ec-services-list ec-move-top" :style="{ left: moveLeft + 'px' }">
      <h2 class="ec-services-heading ec-fade-up" :style="animationStyle">Our Services</h2>
      <div class="ec-services-grid ec-fade-up" :style="animationStyle">
        <div class="ec-services-column ec-column-1">
          <p><a href="#" class="ec-service-link ec-form-trigger" @click="openForm">Solar Panel Installation</a></p>
          <p><a href="projects.html">System Maintenance</a></p>
          <p><a href="projects.html">Energy Efficiency Consulting</a></p>
          <p><a href="#" class="ec-service-link ec-form-trigger" @click="openForm">Battery Storage Solutions</a></p>
        </div>
        <div class="ec-services-column ec-column-2">
          <p><a href="projects.html" class="ec-service-link">Commercial Solar Projects</a></p>
          <p><a href="#" class="ec-service-link ec-form-trigger" @click="openForm">Residential Solar Design</a></p>
          <p><a href="#" class="ec-service-link ec-form-trigger" @click="openForm">Solar Monitoring Systems</a></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {ref, onMounted, onUnmounted, inject} from 'vue';
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

export default {
  name: 'EnergyCoveServicesText',
  setup() {
    const lenis = inject('lenis');
    const moveLeft = ref(0);
    const animationStyle = ref({
      opacity: 0,
      visibility: 'hidden',
      transform: 'translate(0px, 30%)'
    });

    const updateMoveLeft = () => {
      const titleElement = document.querySelector('.ec-services-text .ec-title');
      if (titleElement) {
        moveLeft.value = titleElement.offsetLeft;
      }
    };

    const initAnimations = () => {
      gsap.utils.toArray('.ec-fade-up').forEach((elem) => {
        gsap.fromTo(elem,
            {y: '30%', autoAlpha: 1},
            {
              y: 50,
              autoAlpha: 1,
              duration: 0.9,
              ease: 'power1.inOut',
              scrollTrigger: {
                trigger: elem,
                start: 'top bottom-=5.208vw',
              }
            }
        );
      });
    };

    onMounted(() => {
      if (lenis) {
        ScrollTrigger.scrollerProxy(window, {
          scrollTop(value) {
            if (arguments.length) {
              lenis.scrollTo(value);
            }
            return lenis.scroll;
          },
          getBoundingClientRect() {
            return {top: 0, left: 0, width: window.innerWidth, height: window.innerHeight};
          }
        });

        lenis.on('scroll', ScrollTrigger.update);

        gsap.ticker.add((time) => {
          lenis.raf(time * 1000);
        });

        gsap.ticker.lagSmoothing(0);
      }
      updateMoveLeft();
      window.addEventListener('resize', updateMoveLeft);
      initAnimations();
    });

    onUnmounted(() => {
      window.removeEventListener('resize', updateMoveLeft);
    });

    const openForm = (event) => {
      event.preventDefault();
      // Add logic to open the form
    };

    return {
      moveLeft,
      animationStyle,
      openForm
    };
  }
};
</script>

<style scoped>
@media (min-width: 320px) {
  *, ::after, ::before {
    outline: 0;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  h2, p {
    margin: 0;
    padding: 0;
  }

  a {
    text-decoration: none;
    background-color: transparent;
  }

  a:focus, a:hover {
    text-decoration: none;
    outline: 0;
  }

  .ec-fade-up {
    opacity: 0;
    transform: translateY(30%);
  }

  .ec-services-text {
    margin: -10.156vw 0 0;
    background: #19191f;
    padding: 0 1.302vw 9.01vw;
    position: relative;
  }

  @media (max-width: 760px) {
    .ec-services-text {
      margin: 0;
      padding: 22px 15px 92px;
    }
  }
  .ec-services-text .ec-title-container {
    text-align: right;
    position: relative;
    z-index: 20;
  }

  @media (max-width: 760px) {
    .ec-services-text .ec-title-container {
      text-align: left;
    }
  }
  .ec-services-text .ec-title {
    margin: 0;
    color: #fff;
    font: normal 3.438vw/3.542vw SuisseIntl;
    letter-spacing: -.086vw;
    text-align: right;
    display: inline-block;
  }

  @media (max-width: 760px) {
    .ec-services-text .ec-title {
      font: normal 16px/24px SuisseIntl;
      letter-spacing: -.4px;
      text-align: left;
    }
  }
  @media (max-width: 760px) {
    .ec-services-text .ec-title.ec-title-desktop {
      display: none;
    }
  }
  .ec-services-text .ec-title.ec-title-mobile {
    display: none;
  }

  @media (max-width: 760px) {
    .ec-services-text .ec-title.ec-title-mobile {
      display: block;
    }
  }
  .ec-services-text .ec-title .ec-title-line {
    display: block;
  }

  .ec-services-text .ec-title .ec-title-line.ec-line-2 {
    margin-right: 4.427vw;
  }

  @media (max-width: 760px) {
    .ec-services-text .ec-title .ec-title-line.ec-line-2 {
      margin-right: 0;
    }
  }
  .ec-services-text .ec-title .ec-title-line.ec-line-3, .ec-services-text .ec-title .ec-title-line.ec-line-4 {
    text-align: left;
  }

  .ec-services-text .ec-services-list {
    margin: 5.417vw 0 0 -1.146vw;
    position: relative;
  }

  @media (max-width: 760px) {
    .ec-services-text .ec-services-list {
      position: static;
      margin: 50px 0 0;
    }
  }
  .ec-services-text .ec-services-list .ec-services-heading {
    color: #74747d;
    font: 300 .833vw/.833vw SuisseIntl;
    letter-spacing: -.013vw;
    margin: 0 0 2.188vw;
  }

  @media (max-width: 1600px) {
    .ec-services-text .ec-services-list .ec-services-heading {
      font: 300 .813vw/.813vw SuisseIntl;
    }
  }
  @media (max-width: 1440px) {
    .ec-services-text .ec-services-list .ec-services-heading {
      font: 300 .903vw/.903vw SuisseIntl;
    }
  }
  @media (max-width: 1280px) {
    .ec-services-text .ec-services-list .ec-services-heading {
      font: 300 .938vw/.938vw SuisseIntl;
    }
  }
  @media (max-width: 1024px) {
    .ec-services-text .ec-services-list .ec-services-heading {
      font: 300 1.172vw/1.172vw SuisseIntl;
    }
  }
  @media (max-width: 760px) {
    .ec-services-text .ec-services-list .ec-services-heading {
      font: 300 14px/14px SuisseIntl;
      letter-spacing: -.21px;
      margin: 0 0 36px;
    }
  }
  .ec-services-text .ec-services-list .ec-services-grid {
    display: flex;
  }

  @media (max-width: 760px) {
    .ec-services-text .ec-services-list .ec-services-grid {
      flex-wrap: wrap;
    }
  }
  @media (max-width: 760px) {
    .ec-services-text .ec-services-list .ec-services-grid .ec-services-column {
      width: 100%;
    }
  }
  .ec-services-text .ec-services-list .ec-services-grid .ec-services-column.ec-column-2 {
    padding-left: 16.719vw;
  }

  @media (max-width: 760px) {
    .ec-services-text .ec-services-list .ec-services-grid .ec-services-column.ec-column-2 {
      padding-left: 0;
    }
  }
  .ec-services-text .ec-services-list .ec-services-grid .ec-services-column p {
    margin: 0 0 .521vw;
  }

  @media (max-width: 760px) {
    .ec-services-text .ec-services-list .ec-services-grid .ec-services-column p {
      margin: 0;
    }
  }
  .ec-services-text .ec-services-list .ec-services-grid .ec-services-column p:last-child {
    margin-bottom: 0;
  }

  .ec-services-text .ec-services-list .ec-services-grid .ec-services-column p a {
    color: #c0c0c9;
    letter-spacing: -.014vw;
    font: normal .938vw/.938vw SuisseIntl;
    transition: .35s;
  }

  @media (max-width: 1280px) {
    .ec-services-text .ec-services-list .ec-services-grid .ec-services-column p a {
      font: normal 1.016vw/1.016vw SuisseIntl;
    }
  }
  @media (max-width: 1024px) {
    .ec-services-text .ec-services-list .ec-services-grid .ec-services-column p a {
      font: normal 1.27vw/1.27vw SuisseIntl;
    }
  }
  @media (max-width: 760px) {
    .ec-services-text .ec-services-list .ec-services-grid .ec-services-column p a {
      font: normal 16px/24px SuisseIntl;
      letter-spacing: -.24px;
    }
  }
  .ec-services-text .ec-services-list .ec-services-grid .ec-services-column p a:hover {
    color: #fff;
    transition: .35s;
  }
}
</style>