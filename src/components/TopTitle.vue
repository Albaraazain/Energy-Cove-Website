<template>
  <div class="solar-pin-spacer solar-pin-spacer-topTitle">
    <div ref="solarTopTitle" class="solarTopTitle">
      <div class="solarContainer">
        <div class="solarMainTitle">
          <div class="solarMainTitle_masks">
            <div class="solarMainTitle_mask solarMainTitle_mask01">
              <div class="solarHeading_overflow">
                <div class="solarHeading_overflow">
                  <h1 ref="solarHeadingInner" class="solarHeading_inner solarH1">Energy Cove</h1>
                </div>
              </div>
            </div>
          </div>
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
  name: 'SolarTopTitle',
  setup() {
    const solarTopTitle = ref(null)
    const solarHeadingInner = ref(null)
    const lenis = inject('lenis')

    onMounted(() => {
      if (!solarTopTitle.value || !solarHeadingInner.value) return;

      const tlLoaderOut = gsap.timeline({
        id: 'tlLoaderOut',
        defaults: {
          duration: 1.1,
          ease: 'power2.inOut'
        },
      })

      tlLoaderOut
          .add('h')
          .fromTo(solarHeadingInner.value,
              {autoAlpha: 0, rotation: 7, yPercent: 100},
              {autoAlpha: 1, rotation: 0, yPercent: 0, stagger: .42, duration: 1.5}
          )

      const solarTopTitleRect = solarTopTitle.value.getBoundingClientRect()
      const solarAboutTextWrap = document.querySelector('.solarAboutTextWrap')

      if (!solarAboutTextWrap) {
        console.warn('Element .solarAboutTextWrap not found')
        return
      }

      const solarAboutTextWrapRect = solarAboutTextWrap.getBoundingClientRect()

      const scrollTrigger = ScrollTrigger.create({
        trigger: solarTopTitle.value,
        start: `top top+=${solarTopTitleRect.top}`,
        end: `+=${solarAboutTextWrapRect.top - solarTopTitleRect.height}`,
        pin: true,
        scrub: true,
        pinSpacing: false,
        id: 'tlSolarTopTitle',
        animation: gsap.timeline()
      })

      // Clean up function
      return () => {
        scrollTrigger.kill()
      }
    })

    return {
      solarTopTitle,
      solarHeadingInner
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

  h1 {
    margin: 0;
    padding: 0;
    font-size: 2rem;
  }

  .solarContainer {
    max-width: 100%;
    width: 100%;
    margin-left: auto;
    margin-right: auto;
    padding-left: 2.5rem;
    padding-right: 2.5rem;
  }

  @media (max-width: 760px) {
    .solarContainer {
      padding-left: 1.6rem;
      padding-right: 1.6rem;
    }
  }

  .solarTopTitle {
    margin: 0;
    position: relative;
    z-index: 10;
    width: 100%;
    padding-top: 2.344vw;
    top: 0;
  }

  @media (max-width: 760px) {
    .solarTopTitle {
      display: block;
    }
  }

  .solarTopTitle .solarContainer {
    position: relative;
    height: 100%;
  }

  .solarTopTitle .solarMainTitle {
    position: relative;
    height: auto;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    overflow: visible;
  }

  .solarTopTitle .solarMainTitle_masks {
    margin: 0;
    position: relative;
  }

  @media (max-width: 1600px) {
    .solarTopTitle .solarMainTitle_masks {
      margin-top: .5vw;
    }
  }

  @media (max-width: 760px) {
    .solarTopTitle .solarMainTitle_masks {
      display: block;
    }
  }

  .solarTopTitle .solarMainTitle_mask {
    overflow: visible;
  }

  .solarTopTitle .solarMainTitle_mask.solarMainTitle_mask01 {
    position: relative;
  }

  .solarTopTitle .solarMainTitle_mask.solarMainTitle_mask01 .solarHeading_overflow {
    height: auto; /* Changed from fixed height to auto */
  }

  .solarTopTitle .solarHeading_overflow {
    overflow: visible;
    height: auto;
  }

  .solarTopTitle .solarH1 {
    color: #181a1e;
    font: normal 15.365vw/0.8 Halvar;
    text-transform: uppercase;
    margin: 0;
    overflow: visible;
    opacity: 0;
    letter-spacing: -0.05em;
    word-wrap: break-word;
    hyphens: auto;
  }

  .solarTopTitle {
    position: relative;
    z-index: 1;
  }

  .solarTopTitle .solarH1 {
    margin: 0;
    padding: 0 0.5rem;
  }
}
</style>