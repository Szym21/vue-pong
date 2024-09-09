<template>
    <div class="PongGame">        
        <canvas ref="canvas" @click.up="moveUp" @click.down="moveDown" ></canvas>
    </div>
</template>

<script>
let canvas, ctx;
let player;

export default {
    name: "PongGame",
    props: {
        msg: String
    },
    mounted() {
        canvas = this.$refs.canvas;
        ctx = canvas.getContext("2d");

        canvas.width = 1200;
        canvas.height = 550;
        this.initGame();
        requestAnimationFrame(this.runGame);
        canvas.addEventListener("mousemove", this.updatePlayerMove);
    },
    beforeUnmount() {
        canvas.removeEventListener("mousemove", this.updatePlayerMove);
    },
    methods: {
        initGame(){
            this.clearBoard();
        },
        clearBoard() {
            ctx.fillStyle = "#222";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
        },
        drawMiddle() {
            ctx.beginPath();
            ctx.lineWidth = 2;
            ctx.strokeStyle = "#FFF";
            ctx.setLineDash([10, 10]);
            ctx.moveTo(canvas.width / 2, 0);
            ctx.lineTo(canvas.width / 2, canvas.height);
            ctx.stroke();
            ctx.closePath();
        },
        runGame() {
            this.clearBoard();
            this.drawMiddle();
        },
        moveUp(){
            player.y += 10;
        },
        moveDown(){
            player.y -= 10;
        },
        draw() {
            ctx.fillStyle = "#FFF";
            ctx.fillRect(this.width, this.y - (this.height / 2), -this.width, this.height);
            ctx.fill();
        }
    }
}
</script>

<style>

</style>