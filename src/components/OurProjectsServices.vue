<template>
  <div class="ec-projects-services">
    <div class="ec-grid">
      <div class="ec-column ec-column-projects">
        <div class="ec-content">
          <a href="projects.html" class="ec-link" @mouseover="handleMouseOver" @mouseout="handleMouseOut">
            <span class="ec-fade-up ec-title" :style="animationStyle">
              Solar Projects<span class="ec-count">150+</span>
            </span>
            <span class="ec-arrow"></span>
          </a>
        </div>
      </div>
      <div class="ec-column ec-column-services">
        <div class="ec-content">
          <a href="services.html" class="ec-link" @mouseover="handleMouseOver" @mouseout="handleMouseOut">
            <span class="ec-fade-up ec-title" :style="animationStyle">
              Energy Services<span class="ec-count">07</span>
            </span>
            <span class="ec-arrow"></span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import gsap from 'gsap';
import ScrollTrigger from 'gsap/ScrollTrigger';

gsap.registerPlugin(ScrollTrigger);

export default {
  name: 'EnergyCoveProjectsServices',
  setup() {
    const animationStyle = ref({
      opacity: 0,
      visibility: 'hidden',
      transform: 'translate(0px, 30%)'
    });

    const initAnimations = () => {
      gsap.utils.toArray(".ec-fade-up").forEach((elem) => {
        gsap.fromTo(elem,
            { y: "30%", autoAlpha: 0 },
            {
              y: 0,
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

    const handleMouseOver = (event) => {
      const parentBlock = event.target.closest('.ec-grid');
      const allLinks = parentBlock.querySelectorAll('.ec-link');
      allLinks.forEach(link => link.classList.remove('ec-dimmed'));

      const currentIndex = Array.from(allLinks).indexOf(event.target);
      if (currentIndex < allLinks.length - 1) {
        allLinks[currentIndex + 1].classList.add('ec-dimmed');
      } else {
        allLinks[0].classList.add('ec-dimmed');
      }
    };

    const handleMouseOut = () => {
      document.querySelectorAll('.ec-link').forEach(link => {
        link.classList.remove('ec-dimmed');
      });
    };

    onMounted(() => {
      initAnimations();
    });

    return {
      animationStyle,
      handleMouseOver,
      handleMouseOut
    };
  }
};
</script>

<style scoped>
.ec-link.ec-dimmed {
  opacity: 0.5;
  transition: opacity 0.3s ease;
}
@media (min-width: 320px){
  *,::after,::before{outline:0;margin:0;padding:0;box-sizing:border-box;}
  a{text-decoration:none;}
  a:focus,a:hover{text-decoration:none;outline:0;}
  a{background-color:transparent;}
  a:focus,a:hover{text-decoration:none;outline:0;}
  .ec-fade-up{opacity:0;transform:translateY(30%);}
  .ec-projects-services{margin:0 0 0;position:relative;background:#19191f;}
  .ec-projects-services .ec-grid{display:grid;grid-template-columns:repeat(2,1fr);border-top:#424347 1px solid;}
  @media (max-width:760px){
    .ec-projects-services .ec-grid{grid-template-columns:repeat(1,1fr);border-top:rgba(66,67,71,.3) 1px solid;}
  }
  .ec-projects-services .ec-grid .ec-column-projects{border-right:#424347 1px solid;}
  @media (max-width:760px){
    .ec-projects-services .ec-grid .ec-column-projects{border-right:#424347 0 solid;border-bottom:rgba(66,67,71,.3) 1px solid;}
  }
  .ec-projects-services .ec-grid .ec-column-projects .ec-title .ec-count{right:-2.969vw;}
  @media (max-width:760px){
    .ec-projects-services .ec-grid .ec-column-projects .ec-title .ec-count{right:-33px;}
  }
  .ec-projects-services .ec-grid .ec-column-services .ec-title .ec-count{right:-2.188vw;}
  @media (max-width:760px){
    .ec-projects-services .ec-grid .ec-column-services .ec-title .ec-count{right:-23px;}
  }
  .ec-projects-services .ec-grid .ec-link{display:grid;align-content:center;justify-content:center;width:100%;height:100%;position:relative;height:46.042vw;transition:.6s;}
  @media (max-width:760px){
    .ec-projects-services .ec-grid .ec-link{height:270px;}
  }
  .ec-projects-services .ec-grid .ec-link:hover .ec-arrow{opacity:1;transition:.6s;}
  .ec-projects-services .ec-grid .ec-title{color:#fff;font:normal 3.438vw/3.438vw SuisseIntl;letter-spacing:-.086vw;position:relative;display:inline-block;}
  @media (max-width:760px){
    .ec-projects-services .ec-grid .ec-title{font:normal 40px/40px SuisseIntl;letter-spacing:-1px;}
  }
  .ec-projects-services .ec-grid .ec-title .ec-count{position:absolute;top:.365vw;right:-2.969vw;font:normal 1.094vw/1.094vw SuisseIntl;letter-spacing:-.022vw;}
  @media (max-width:760px){
    .ec-projects-services .ec-grid .ec-title .ec-count{top:1px;font:normal 12px/12px SuisseIntl;letter-spacing:-.24px;}
  }
  .ec-projects-services .ec-grid .ec-arrow{display:block;background:url(https://www.liqium.com/img-2024/arw_w.svg) no-repeat 0 0/cover;width:2.5vw;height:1.927vw;position:absolute;bottom:5.365vw;left:0;right:0;margin:0 auto;opacity:0;transition:.6s;}
  @media (max-width:760px){
    .ec-projects-services .ec-grid .ec-arrow{display:none;}
  }
}
</style>