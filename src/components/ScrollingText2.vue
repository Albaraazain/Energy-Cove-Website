<template>
  <div class="ec-scrolling-text" ref="textContainer">
    <div class="ec-text-wrapper ec-fade-up" :style="wrapperStyle">
      <div class="ec-text-content" :style="textWrapStyle">
        <div class="ec-moving-text">{{ scrollingText }}</div>
      </div>
      <div class="ec-text-content" :style="clonedTextWrapStyle">
        <div class="ec-moving-text">{{ scrollingText }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import {ref, computed, onMounted, onUnmounted} from 'vue'

export default {
  name: 'EnergyCoveScrollingText',
  setup() {
    const scrollingText = 'Sustainable Energy Solutions for a Brighter Future - Solar Power - Clean Energy - Renewable Resources'
    const scrollPosition = ref(0)
    const scrollSpeed = 0.5 // Adjust this value to change scroll speed
    const textContainer = ref(null)

    const wrapperStyle = computed(() => ({
      opacity: 1,
      visibility: 'inherit',
      transform: 'translate(0px, 0px)'
    }))

    const textWrapStyle = computed(() => ({
      transform: `translateX(${-scrollPosition.value}%)`,
      display: 'inline-block',
      whiteSpace: 'nowrap'
    }))

    const clonedTextWrapStyle = computed(() => ({
      transform: `translateX(${100 - scrollPosition.value}%)`,
      display: 'inline-block',
      whiteSpace: 'nowrap'
    }))

    const animateScroll = () => {
      scrollPosition.value += scrollSpeed
      if (scrollPosition.value >= 100) {
        scrollPosition.value = 0
      }
      requestAnimationFrame(animateScroll)
    }

    let animationFrame

    onMounted(() => {
      animationFrame = requestAnimationFrame(animateScroll)
    })

    onUnmounted(() => {
      cancelAnimationFrame(animationFrame)
    })

    return {
      scrollingText,
      wrapperStyle,
      textWrapStyle,
      clonedTextWrapStyle,
      textContainer
    }
  }
}
</script>

<style scoped>
.ec-scrolling-text {
  position: relative;
  overflow: hidden;
  padding: 15.365vw 0 4.271vw;
  background: #fff;
  border-bottom: #d1d1d1 1px solid;
}

.ec-text-wrapper {
  display: flex;
  width: 200%; /* Double the width to accommodate both text elements */
  position: relative;
}

.ec-text-content {
  width: 50%; /* Each text wrap takes half of the doubled width */
}

.ec-moving-text {
  color: #000;
  font: 300 9.583vw/9.583vw SuisseIntl;
  letter-spacing: -0.479vw;
  white-space: nowrap;
}

@media (max-width: 760px) {
  .ec-scrolling-text {
    padding: 146px 0 51px;
  }

  .ec-moving-text {
    font: 300 70px/70px SuisseIntl;
    letter-spacing: -1.4px;
  }
}
</style>