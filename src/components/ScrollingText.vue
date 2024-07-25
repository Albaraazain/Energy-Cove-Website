<template>
  <div class="ec-scrolling-text">
    <div class="ec-scrolling-text-wrapper up" :style="wrapperStyle">
      <div data-cursor-class="ec-cursor" ref="textContainer">
        <div
            v-for="(wrapper, index) in wrappers"
            :key="index"
            class="ec-text-wrapper"
            :style="getWrapperStyle(index)"
        >
          <div class="ec-moving-text">{{ text }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive, onMounted, onUnmounted } from 'vue';

export default {
  name: 'EnergyCoveScrollingText',
  props: {
    text: {
      type: String,
      default: 'SOLAR POWER—ENERGY SAVINGS—SUSTAINABILITY—GREEN FUTURE—'
    }
  },
  setup(props) {
    const textContainer = ref(null);
    const wrappers = reactive([{}, {}]);
    const wrapperStyle = reactive({
      opacity: 1,
      visibility: 'inherit',
      transform: 'translate(0px, 0px)'
    });

    const animationFrame = ref(null);
    const scrollPosition = ref(0);

    const animate = () => {
      scrollPosition.value -= 0.1; // Adjust speed as needed
      if (scrollPosition.value <= -100) {
        scrollPosition.value = 0;
      }
      animationFrame.value = requestAnimationFrame(animate);
    };

    const getWrapperStyle = (index) => {
      const baseTransform = `translate(${scrollPosition.value}%, 0%) translate3d(0px, 0px, 0px)`;
      if (index === 1) {
        const containerWidth = textContainer.value ? textContainer.value.offsetWidth : 0;
        const startPosition = 100 * containerWidth / window.innerWidth;
        const adjustedLeft = Math.max(startPosition, 100 + startPosition + scrollPosition.value);
        return {
          position: 'absolute',
          left: `${adjustedLeft}%`,
          top: '0px',
          transform: baseTransform
        };
      }
      return {transform: baseTransform};
    };

    onMounted(() => {
      animate();
    });

    onUnmounted(() => {
      if (animationFrame.value) {
        cancelAnimationFrame(animationFrame.value);
      }
    });

    return {
      textContainer,
      wrappers,
      wrapperStyle,
      getWrapperStyle,
      text: props.text
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

  .up {
    opacity: 0;
    transform: translateY(30%);
  }

  .ec-scrolling-text {
    position: relative;
    overflow: hidden;
    padding: 0 0 4.063vw;
    background: #000;
    border-top: rgba(255, 255, 255, .18) 1px solid;
    border-bottom: rgba(255, 255, 255, .18) 1px solid;
  }

  @media (max-width: 760px) {
    .ec-scrolling-text {
      padding: 15px 0 14px;
    }
  }
  .ec-scrolling-text:hover .ec-scrolling-text-wrapper .ec-text-wrapper .ec-moving-text {
    color: #ffffff;
    transition: .55s;
  }

  .ec-scrolling-text .ec-scrolling-text-wrapper {
    display: flex;
    width: 100%;
    position: relative;
  }

  .ec-scrolling-text .ec-scrolling-text-wrapper .ec-text-wrapper {
    margin: 0;
  }

  .ec-scrolling-text .ec-scrolling-text-wrapper .ec-text-wrapper .ec-moving-text {
    color: #808080;
    font: normal 15.365vw/13.333vw Halvar;
    letter-spacing: -1.152vw;
    white-space: nowrap;
    text-transform: uppercase;
    transition: .55s;
  }

  @media (max-width: 760px) {
    .ec-scrolling-text .ec-scrolling-text-wrapper .ec-text-wrapper .ec-moving-text {
      font: normal 64px/64px Halvar;
      letter-spacing: -4.8px;
    }
  }
}
</style>