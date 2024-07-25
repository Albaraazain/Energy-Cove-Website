<template>
  <div id="energy-cove-cursor" ref="cursor">
    <div class="ec-cursor-outer">
      <div class="ec-cursor-inner">
        <div class="ec-cursor-icon"></div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue';

export default {
  name: 'EnergyCoveCursor',
  setup() {
    const cursor = ref(null);
    const mouse = {x: 0, y: 0};
    const pos = {x: 0, y: 0};
    const speed = 0.1;

    let animationFrameId = null;

    const updateCoordinates = (e) => {
      mouse.x = e.clientX;
      mouse.y = e.clientY;
    };

    const updateCursor = () => {
      const diffX = Math.round(mouse.x - pos.x);
      const diffY = Math.round(mouse.y - pos.y);

      pos.x += diffX * speed;
      pos.y += diffY * speed;

      const translate = `translate3d(${pos.x}px, ${pos.y}px, 0)`;
      if (cursor.value) {
        cursor.value.style.transform = translate;
      }

      animationFrameId = requestAnimationFrame(updateCursor);
    };

    onMounted(() => {
      window.addEventListener('mousemove', updateCoordinates);
      updateCursor();
    });

    onUnmounted(() => {
      window.removeEventListener('mousemove', updateCoordinates);
      if (animationFrameId) {
        cancelAnimationFrame(animationFrameId);
      }
    });

    return {
      cursor
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

  #energy-cove-cursor {
    position: absolute;
    z-index: 99999;
    left: -3.229vw;
    top: -3.229vw;
    width: 6.458vw;
    height: 6.458vw;
    pointer-events: none;
    will-change: transform;
    overflow: hidden;
    display: none;
  }

  @media (max-width: 760px) {
    #energy-cove-cursor {
      display: none;
    }
  }
  #energy-cove-cursor .ec-cursor-outer {
    position: relative;
    width: 100%;
    height: 100%;
    transform: scale(0);
    background: #494a4f;
    transition: .35s ease-in-out;
    border-radius: 100%;
    transform-origin: center;
    z-index: 10;
    overflow: hidden;
  }

  #energy-cove-cursor .ec-cursor-outer .ec-cursor-inner {
    position: relative;
    width: 100%;
    height: 100%;
  }

  #energy-cove-cursor .ec-cursor-outer .ec-cursor-inner .ec-cursor-icon {
    position: absolute;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    margin: auto;
    z-index: 30;
    background: url(https://www.liqium.com/img-2024/s6.svg) no-repeat 0 0/cover;
    width: 1.094vw;
    height: .365vw;
  }
}
</style>