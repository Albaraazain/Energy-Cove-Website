<template>
  <div class="ec-services">
    <div class="ec-title ec-title-desktop ec-fade-up" :style="titleStyle">
      <div class="ec-subtitle">{{ title }}</div>
      <span class="ec-line ec-line-center">{{ subtitle }}</span>
      <span class="ec-line">residential <span class="ec-highlight">and</span> commercial solar installations<span class="ec-highlight">,</span> maintenance</span>
      <span class="ec-line">and energy optimization. Our solar solutions are trusted by</span>
      homeowners and businesses alike
    </div>
    <div class="ec-title ec-title-mobile ec-fade-up" :style="titleStyle">
      <div class="ec-subtitle">{{ title }}</div>
      <span class="ec-line">{{ subtitle }}</span>
      <span class="ec-line">
        <a href="projects.html">residential</a> <span class="ec-highlight">and</span> <a href="projects.html">commercial</a> <a href="projects.html">solar installations</a><span class="ec-highlight">,</span>
      </span>
      <span class="ec-line">
        <a href="projects.html">maintenance</a> <span class="ec-highlight">and</span> <a href="projects.html">energy optimization</a><span class="ec-highlight">.</span>
      </span>
      <span class="ec-line">Our <a href="projects.html">solar solutions</a> are trusted by</span>
      <span class="ec-line">homeowners and businesses alike</span>
    </div>
    <div class="ec-circle-container">
      <div class="ec-circle ec-circle-outer"></div>
      <div class="ec-circle ec-circle-inner"></div>
      <div class="ec-video-container">
        <video ref="video" id="ec-video" class="ec-video" autoplay muted loop playsinline>
          <source :src="videoSrc" type="video/mp4">
        </video>
        <a href="#" class="ec-cta-button ec-fade-up" :style="linkStyle" @click="handleClick">
          <span>{{ linkText }}</span>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive, onMounted } from 'vue';

export default {
  name: 'EnergyCoveServices',
  props: {
    title: {
      type: String,
      default: 'Our services'
    },
    subtitle: {
      type: String,
      default: 'We install, maintain and optimize'
    },
    videoSrc: {
      type: String,
      default: './video/solar-panel-installation.mp4'
    },
    linkText: {
      type: String,
      default: "Get a quote"
    }
  },
  setup(props) {
    const video = ref(null);
    const titleStyle = reactive({
      opacity: 1,
      visibility: 'inherit',
      transform: 'translate(0px, 0px)'
    });
    const linkStyle = reactive({
      opacity: 1,
      visibility: 'inherit',
      transform: 'translate(0px, 0px)'
    });

    const handleClick = (event) => {
      event.preventDefault();
      console.log("Get a quote button clicked");
    };

    onMounted(() => {
      if (video.value) {
        video.value.play().catch(error => {
          console.log("Auto-play was prevented:", error);
        });
      }
    });

    return {
      video,
      titleStyle,
      linkStyle,
      handleClick
    };
  }
};
</script>

<style scoped>
@media (min-width: 320px) {
  *, ::after, ::before { outline: 0; margin: 0; padding: 0; box-sizing: border-box; }
  a { text-decoration: none; background-color: transparent; }
  a:focus, a:hover { text-decoration: none; outline: 0; }
  .ec-fade-up { opacity: 0; transform: translateY(30%); }
  .ec-services { background: #19191f; padding: 11.823vw 1.25vw 0; position: relative; }
  @media (max-width: 760px) { .ec-services { padding: 92px 15px 0; overflow: hidden; height: 900px; } }
  .ec-services .ec-title { margin: 0; color: #fff; font: normal 3.438vw/3.542vw SuisseIntl; letter-spacing: -.086vw; position: relative; z-index: 30; }
  @media (max-width: 760px) { .ec-services .ec-title { font: normal 16px/24px SuisseIntl; letter-spacing: -.4px; } }
  @media (max-width: 760px) { .ec-services .ec-title.ec-title-desktop { display: none; } }
  .ec-services .ec-title.ec-title-mobile { display: none; }
  @media (max-width: 760px) { .ec-services .ec-title.ec-title-mobile { display: block; } }
  .ec-services .ec-title .ec-subtitle { color: #8b8d92; font: normal 1.094vw/1.094vw SuisseIntl; letter-spacing: -.022vw; display: inline-block; position: absolute; top: .365vw; left: 0; }
  @media (max-width: 1024px) { .ec-services .ec-title .ec-subtitle { font: normal 1.172vw/1.172vw SuisseIntl; top: .391vw; } }
  @media (max-width: 760px) { .ec-services .ec-title .ec-subtitle { position: relative; display: block; top: 0; font: normal 16px/16px SuisseIntl; letter-spacing: -.32px; margin: 0 0 37px; } }
  .ec-services .ec-title a { color: #a5b3c5; transition: .35s; }
  .ec-services .ec-title a:hover { color: #fff; transition: .35s; }
  .ec-services .ec-title .ec-highlight { color: #a5b3c5; }
  @media (max-width: 760px) { .ec-services .ec-title .ec-highlight { color: #fff; } }
  .ec-services .ec-title .ec-line { display: block; }
  @media (max-width: 760px) { .ec-services .ec-title .ec-line { display: block; } }
  .ec-services .ec-title .ec-line.ec-line-center { text-align: center; }
  @media (max-width: 760px) { .ec-services .ec-title .ec-line.ec-line-center { text-align: left; } }
  .ec-services .ec-circle-container { width: 81.771vw; height: 81.771vw; margin: 0 auto; position: relative; display: flex; align-items: center; justify-content: center; margin: -13.802vw auto 0; }
  @media (max-width: 760px) { .ec-services .ec-circle-container { width: 656px; height: 656px; min-width: 656px; min-height: 656px; margin: 0 auto; position: absolute; top: 0; bottom: 0; left: -50%; right: -50%; margin: 228px auto 0; } }
  .ec-services .ec-circle-container .ec-video-container { width: 41.667vw; height: 41.667vw; position: relative; display: grid; justify-content: center; align-content: center; overflow: hidden; }
  @media (max-width: 760px) { .ec-services .ec-circle-container .ec-video-container { width: 330px; height: 330px; } }
  .ec-services .ec-circle-container .ec-video-container .ec-video { position: absolute; top: 0; left: 0; bottom: 0; right: 0; margin: auto; left: -3.646vw; width: 101%; height: 101%; }
  @media (max-width: 760px) { .ec-services .ec-circle-container .ec-video-container .ec-video { left: -2.632vw; width: 108%; height: 108%; } }
  .ec-services .ec-circle-container .ec-video-container .ec-cta-button { margin: -1.042vw 0 0; position: relative; color: #fff; font: normal 1.25vw/1.25vw SuisseIntl; display: inline-block; padding: 2.344vw 5.208vw; border-radius: 3.906vw; -webkit-backdrop-filter: blur(.417vw); backdrop-filter: blur(.417vw); background: rgba(255, 255, 255, .05); letter-spacing: -.033vw; text-transform: uppercase; z-index: 30; transition: .35s; }
  @media (max-width: 760px) { .ec-services .ec-circle-container .ec-video-container .ec-cta-button { font: normal 18px/18px SuisseIntl; padding: 31px 66px; border-radius: 50px; letter-spacing: -.468px; margin: 0; } }
  .ec-services .ec-circle-container .ec-video-container .ec-cta-button:hover { background: rgba(255, 255, 255, .25); -webkit-backdrop-filter: blur(1.979vw); backdrop-filter: blur(1.979vw); transition: .35s; }
  @media (max-width: 760px) { .ec-services .ec-circle-container .ec-video-container .ec-cta-button:hover { -webkit-backdrop-filter: blur(28px); backdrop-filter: blur(28px); } }
  .ec-services .ec-circle-container .ec-video-container .ec-cta-button span { position: relative; display: inline-block; }
  .ec-services .ec-circle-container .ec-video-container .ec-cta-button span:after { content: ""; position: absolute; top: .052vw; right: -1.198vw; width: .521vw; height: .521vw; background: url(https://www.liqium.com/img-2024/s6w.svg) no-repeat 0 0/cover; }
  @media (max-width: 1600px) { .ec-services .ec-circle-container .ec-video-container .ec-cta-button span:after { width: .625vw; height: .625vw; } }
  @media (max-width: 760px) { .ec-services .ec-circle-container .ec-video-container .ec-cta-button span:after { top: 0; right: -15px; width: 8px; height: 8px; } }
  .ec-services .ec-circle-container .ec-circle { position: absolute; top: 0; left: 0; bottom: 0; right: 0; margin: auto; border-radius: 100%; pointer-events: none; }
  .ec-services .ec-circle-container .ec-circle.ec-circle-outer { width: 81.771vw; height: 81.771vw; background: url(https://www.liqium.com/img-2024/cr01.svg) no-repeat 50% 50%/cover; z-index: 20; animation: ec-rotate 85s normal linear infinite; }
  @media (max-width: 760px) { .ec-services .ec-circle-container .ec-circle.ec-circle-outer { width: 656px; height: 656px; min-width: 656px; min-height: 656px; } }
  .ec-services .ec-circle-container .ec-circle.ec-circle-inner { width: 59.271vw; height: 59.271vw; background: url(https://www.liqium.com/img-2024/cr02.svg) no-repeat 50% 50%/cover; z-index: 20; animation: ec-rotate-rev 85s normal linear infinite; }
  @media (max-width: 760px) { .ec-services .ec-circle-container .ec-circle.ec-circle-inner { width: 475px; height: 475px; min-width: 475px; min-height: 475px; } }
}

@keyframes ec-rotate { 0% { transform: rotate3d(0, 0, 1, 0deg); } 100% { transform: rotate3d(0, 0, 1, 360deg); } }
@keyframes ec-rotate-rev { 0% { transform: rotate3d(0, 0, 1, 360deg); } 100% { transform: rotate3d(0, 0, 1, 0deg); } }
</style>