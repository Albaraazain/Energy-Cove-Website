<template>
  <div id="app" class="">
    <Header />
    <TopTitle />
    <TopBest />
    <HeroImages />
    <AboutTextWrap />
    <CustomCursor />
    <ScrollingText/>
    <OurServices />
    <OurServicesTXT />
    <OurProjectsServices />
    <ScrollingText2 />

  </div>
</template>

<script>
import { onMounted, provide } from 'vue';
import TopTitle from "./components/TopTitle.vue";
import TopBest from "./components/TopBest.vue";
import HeroImages from "./components/HeroImages.vue";
import CustomCursor from "./components/CustomCursor.vue";
import ScrollingText from "./components/ScrollingText.vue";
import OurServices from "./components/OurServices.vue";
import OurServicesTXT from "./components/OurServicesTXT.vue";
import OurProjectsServices from "./components/OurProjectsServices.vue";
import { initScrollManager } from './ScrollManager.js';
import AboutTextWrap from "./components/AboutTextWrap.vue";
import ScrollingText2 from "./components/ScrollingText2.vue";
import OurClients from "./components/OurClients.vue";
import Header from "./components/Header.vue";

export default {
  components: {
    Header,
    ScrollingText2,
    AboutTextWrap,
    TopTitle,
    TopBest,
    HeroImages,
    CustomCursor,
    ScrollingText,
    OurServices,
    OurServicesTXT,
    OurProjectsServices,
  },
  setup() {
    const {lenis} = initScrollManager();
    provide('lenis', lenis);
    return {};
  }
}
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  overflow-x: hidden;
}

#app {
  width: 100%;
  max-width: 100vw;
  overflow-x: hidden;
}

html.lenis, html.lenis body {
  height: auto;
}

.lenis.lenis-smooth {
  scroll-behavior: auto !important;
}

.lenis.lenis-smooth [data-lenis-prevent] {
  overscroll-behavior: contain;
}

.lenis.lenis-stopped {
  overflow: hidden;
}

.lenis.lenis-smooth iframe {
  pointer-events: none;
}

/* Ensure all direct children of #app don't exceed viewport width */
#app > * {
  max-width: 100vw;
  box-sizing: border-box;
}

/* Media query for responsiveness */
@media screen and (max-width: 100vw) {
  #app > * {

  }
}
</style>