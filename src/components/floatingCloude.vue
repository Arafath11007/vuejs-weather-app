<template>
    <canvas class="clouds-canvas"></canvas>
</template>
  
<script>
export default {
    mounted() {
        const canvas = this.$el;
        const ctx = canvas.getContext('2d');
        const cloudCount = 5; // Number of clouds
        const clouds = [];

        // Set canvas dimensions for mobile-friendly size
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        // Create clouds
        for (let i = 0; i < cloudCount; i++) {
            clouds.push({
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height * 0.5,
                size: Math.random() * 30 + 50, // Adjusted cloud size for smaller clouds
                speed: Math.random() * 0.5 + 0.1, // Cloud speed
                opacity: Math.random() * 0.5 + 0.3 // Cloud opacity
            });
        }

        // Draw clouds
        function drawCloud(x, y, size, opacity) {
            ctx.beginPath();
            // ctx.arc(x, y, size, 0, Math.PI * 2);
            // ctx.arc(x + size * 0.2, y - size * 0.3, size * 0.6, 0, Math.PI * 2);
            ctx.arc(x + size * 0.6, y, size * 0.5, 0, Math.PI * 2);
            ctx.arc(x + size * 1.1, y - size * 0.2, size * 0.6, 0, Math.PI * 2);
            ctx.arc(x + size * 1.5, y, size * 0.4, 0, Math.PI * 2);
            ctx.arc(x + size * 1.8, y - size * 0.3, size * 0.7, 0, Math.PI * 2);
            ctx.arc(x + size * 2.2, y, size * 0.5, 0, Math.PI * 2);
            // ctx.arc(x + size * 2.7, y - size * 0.2, size * 0.6, 0, Math.PI * 2);
            ctx.fillStyle = `rgba(255, 255, 255, ${opacity})`;
            ctx.fill();
            ctx.closePath();
        }

        function draw() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            clouds.forEach(cloud => {
                cloud.x += cloud.speed;

                if (cloud.x > canvas.width + cloud.size) {
                    cloud.x = -cloud.size;
                }

                drawCloud(cloud.x, cloud.y, cloud.size, cloud.opacity);
            });

            requestAnimationFrame(draw);
        }

        draw();

        // Handle resizing
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    }
};
</script>
  
<style scoped>
.clouds-canvas {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    top: 80px;
}
</style>
  