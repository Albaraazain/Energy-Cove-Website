<template>
  <div ref="solarTopFeature" class="solarTopFeature solarFadeUp">
    <div class="solar-pin-spacer solar-pin-spacer-topTitle">
      <div ref="solarFeatureBox" class="solarFeatureBox solarFadeUpMobile">
        <div class="solarFeatureIcon">
          <img src="./img-2024/s5.svg" width="32" height="18" alt="Solar Feature Icon">
        </div>
        <div class="solarFeatureText">
          <span class="solarFeatureBreak">Create world-class advanced</span>
          solar energy solutions
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, inject } from 'vue'
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

export default {
  name: 'SolarTopFeature',
  setup() {
    const solarTopFeature = ref(null)
    const solarFeatureBox = ref(null)
    const lenis = inject('lenis')

    onMounted(() => {
      if (!solarTopFeature.value || !solarFeatureBox.value) return;

      // Animation for the solarFadeUp class
      gsap.fromTo(solarTopFeature.value,
          {y: "30%", autoAlpha: 0},
          {
            y: 0,
            autoAlpha: 1,
            duration: .9,
            ease: 'power1.inOut',
            scrollTrigger: {
              trigger: solarTopFeature.value,
              start: 'top bottom-=5.208vw',
            }
          }
      )

      // Animation for the solarFadeUpMobile class
      gsap.fromTo(solarFeatureBox.value,
          {y: "30%", autoAlpha: 0},
          {
            y: 0,
            autoAlpha: 1,
            duration: .9,
            ease: 'power1.inOut',
            scrollTrigger: {
              trigger: solarFeatureBox.value,
              start: 'top bottom-=5.208vw',
            }
          }
      )

      // Pin animation
      const featureBoxElement = document.querySelector('.solarTopFeature .solarFeatureBox')
      if (featureBoxElement) {
        const abtScr = featureBoxElement.getBoundingClientRect().top

        const pinAnimation = ScrollTrigger.create({
          trigger: ".solarTopFeature .solarFeatureBox",
          start: `top top+=${abtScr}`,
          end: `+=${window.innerHeight / 2}`,
          pin: true,
          scrub: true,
          pinSpacing: false,
        })

        // Clean up function
        return () => {
          pinAnimation.kill()
        }
      }
    })

    return {
      solarTopFeature,
      solarFeatureBox
    }
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
  }

  img {
    border-style: none;
  }

  .solarFadeUp {
    opacity: 0;
    transform: translateY(30%);
  }

  @media (max-width: 760px) {
    .solarFadeUp {
      opacity: 1;
      transform: translateY(0);
    }
  }
  @media (max-width: 760px) {
    .solarFadeUpMobile {
      opacity: 0;
      transform: translateY(30%);
    }
  }
  .solarTopFeature {
    position: absolute;
    padding: 16.354vw 0 0;
    left: 1.302vw;
  }

  @media (max-width: 760px) {
    .solarTopFeature {
      padding: 0;
      left: 5px;
      top: 111.2vw;
    }
  }
  @media (max-width: 760px) {
    .solarTopFeature .solarFeatureBox {
      padding-left: 5px;
    }
  }
  .solarTopFeature .solarFeatureBox .solarFeatureIcon {
    height: .938vw;
    margin: 0 0 1.094vw .365vw;
  }

  @media (max-width: 760px) {
    .solarTopFeature .solarFeatureBox .solarFeatureIcon {
      margin: 55vw 0 1.974vw 1.974vw;
      margin: 0 0 15px 5px;
      height: auto;
    }
  }
  .solarTopFeature .solarFeatureBox .solarFeatureIcon img {
    width: 1.667vw;
  }

  @media (max-width: 760px) {
    .solarTopFeature .solarFeatureBox .solarFeatureIcon img {
      width: 32px;
    }
  }
  .solarTopFeature .solarFeatureBox .solarFeatureText {
    color: #000;
    font: normal 1.25vw/1.51vw SuisseIntl;
    letter-spacing: -.033vw;
  }

  @media (max-width: 1024px) {
    .solarTopFeature .solarFeatureBox .solarFeatureText {
      font: normal 1.27vw/1.563vw SuisseIntl;
    }
  }
  @media (max-width: 760px) {
    .solarTopFeature .solarFeatureBox .solarFeatureText {
      font: normal 21px/21px SuisseIntl;
      letter-spacing: -.42px;
      margin: 0 0 0 6px;
    }
  }
  .solarTopFeature .solarFeatureBox .solarFeatureText .solarFeatureBreak {
    display: block;
    margin: 0 0 .156vw;
  }

  @media (max-width: 760px) {
    .solarTopFeature .solarFeatureBox .solarFeatureText .solarFeatureBreak {
      margin: 0 0 3px;
    }
  }
}
</style>