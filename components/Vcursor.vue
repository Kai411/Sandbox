<template>
  <span>
    <span class="vueCursor"></span>
  </span>
</template>

<script>
export default {
  props: {
    scaleElement: {},

    circleSize: {
      default: 30,
    },
    cursorColor: {
      default: '#f00',
    },
  },

  mounted() {
    let vueCursor = document.querySelector('.vueCursor')

    document.addEventListener('mousemove', (e) => {
      let scaleElementHovered =
        e.target &&
        (e.target.classList.contains(this.scaleElement) ||
          e.target.closest(`.${this.scaleElement}`))

      vueCursor.style.cssText = `
      transform: translate3d(${e.clientX - this.circleSize - 1}px, ${
        e.clientY - this.circleSize - 1
      }px, 0) scale(${scaleElementHovered ? 1 : 0.5});
        width: ${this.circleSize * 2}px;
        height: ${this.circleSize * 2}px;
        background-color: ${this.cursorColor}
        `
    })
  },
}
</script>

<style>
* {
  cursor: none;
}
.vueCursor {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 100000;
  border-radius: 50%;
  pointer-events: none;
  box-sizing: border-box;
  backface-visibility: hidden;
  transition: transform 100ms;
  mix-blend-mode: difference;
}
</style>
