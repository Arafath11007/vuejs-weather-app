<template>
  <canvas class="rain-canvas"></canvas>
</template>

<script>
export default {
  props: {
    amount: {
      type: Number,
      default: 100
    },
    size: {
      type: Number,
      default: 5
    },
    speed: {
      type: Number,
      default: 5
    },
    color: {
      type: String,
      default: '#BBDEFB'
    },
    zIndex: {
      type: Number,
      default: null
    },
    resize: {
      type: Boolean,
      default: true
    }
  },

  mounted() {
    const self = this;
    const CANVAS = self.$el;
    const CONTEXT = CANVAS.getContext('2d');
    let canvasHeight = CANVAS.offsetHeight;
    let canvasWidth = CANVAS.offsetWidth;
    const drops = [];

    CANVAS.height = canvasHeight;
    CANVAS.width = canvasWidth;
    CANVAS.style.zIndex = self.zIndex ? self.zIndex : 'auto';

    function init() {
      for (let i = 0; i < self.amount; i++) {
        drops.push({
          x: Math.random() * canvasWidth,
          y: Math.random() * canvasHeight,
          size: Math.random() * self.size + 2.5,
          speed: Math.random() * self.speed + 2,
          opacity: Math.random() * 0.5 + 0.3
        });
      }
      rain();
    }

    function rain() {
      CONTEXT.clearRect(0, 0, canvasWidth, canvasHeight);
      CONTEXT.fillStyle = self.color;

      drops.forEach((drop) => {
        CONTEXT.globalAlpha = drop.opacity;
        CONTEXT.beginPath();
        CONTEXT.arc(drop.x, drop.y, drop.size, 0, Math.PI * 2);
        CONTEXT.fill();
        drop.y += drop.speed;

        if (drop.y - drop.size > canvasHeight) {
          drop.x = Math.random() * canvasWidth;
          drop.y = -drop.size;
        }
      });

      requestAnimationFrame(rain);
    }

    init();

    if (self.resize) {
      window.addEventListener('resize', function () {
        const H0 = CANVAS.height;
        const W0 = CANVAS.width;
        const H1 = CANVAS.offsetHeight;
        const W1 = CANVAS.offsetWidth;

        CANVAS.height = canvasHeight = H1;
        CANVAS.width = canvasWidth = W1;

        drops.forEach((drop) => {
          drop.x = drop.x / W0 * W1;
          drop.y = drop.y / H0 * H1;
        });
      });
    }
  }
};
</script>

<style scoped>
.rain-canvas {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  top: 80px;
}
</style>
