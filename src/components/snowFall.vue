<template>
    <div class="snowfall">
        <!-- Add snowflake elements dynamically -->
        <div v-for="(flake, index) in flakes" :key="index" class="snowflake"></div>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            flakes: [], // Array to hold snowflake data
        };
    },
    mounted() {
        this.createSnowflakes();
    },
    methods: {
        createSnowflakes() {
            const numberOfFlakes = 50; // Number of snowflakes

            for (let i = 0; i < numberOfFlakes; i++) {
                // Generate random positions for each snowflake
                const positionX = Math.random() * window.innerWidth;
                const positionY = Math.random() * window.innerHeight;

                // Generate random animation duration for each snowflake
                const duration = Math.random() * 5 + 3; // Adjust duration as needed

                // Push snowflake data into the array
                this.flakes.push({
                    x: positionX,
                    y: positionY,
                    d: duration,
                });
            }
        },
    },
};
</script>
  
<style>
/* Basic styles for the snowfall container */
.snowfall {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 9999;
}

.snowflake {
  position: absolute;
  width: 8px;
  height: 8px;
  background-color: #fff;
  border-radius: 50%;
  animation: fall linear infinite;
  opacity: 0; /* Start with zero opacity */
}

@keyframes fall {
  0% {
    transform: translateY(-10vh);
    opacity: 1; /* Show the snowflake */
  }
  100% {
    transform: translateY(100vh);
    opacity: 0; /* Hide the snowflake */
  }
}
</style>
  