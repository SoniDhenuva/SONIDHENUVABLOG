---
title: Sprite testing
layout: post
type: hacks
comments: true
courses: {csa: {week: 10}}
type: ccc
---

<!DOCTYPE html>
<html lang="en">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Demon Animation</title>
    <style>
        body {
            background: black;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            font-family: Arial, sans-serif;
        }
        canvas {
            background: black;
            margin: 20px 0;
            border: 1px solid #333;
        }
        .controls {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }
        button {
            padding: 10px 15px;
            background: white;
            border: 1px solid gray;
            cursor: pointer;
        }
        button.active {
            background: gray;
            color: white;
        }
    </style>
    <canvas id="spriteContainer"></canvas>
    <div class="controls">
        <button class="active" onclick="setAnimation(0)">Idle</button>
        <button onclick="setAnimation(1)">Walk</button>
        <button onclick="setAnimation(2)">Fly</button>
        <button onclick="setAnimation(3)">Jump</button>
        <button onclick="setAnimation(4)">Attack</button>
        <button onclick="setAnimation(5)">Hurt</button>
        <button onclick="setAnimation(6)">Die</button>
    </div>
    <script>
        const canvas = document.getElementById('spriteContainer');
        const ctx = canvas.getContext('2d');
        // Sprite dimensions based on your sprite sheet
        const SPRITE_WIDTH = 100;
        const SPRITE_HEIGHT = 100;
        const SCALE_FACTOR = 2;
        const FRAMES_PER_ROW = 5; // 5 frames per animation
        const TOTAL_ROWS = 7; // 7 animations (idle, walk, fly, jump, attack, hurt, die)
        const FRAME_INTERVAL = 100;
        // Canvas size
        canvas.width = SPRITE_WIDTH * SCALE_FACTOR + 20;
        canvas.height = SPRITE_HEIGHT * SCALE_FACTOR + 40;
        class Demon {
            constructor() {
                this.image = new Image();
                this.image.src = "demon.webp";
                this.frameX = 0;
                this.frameY = 0;
                this.maxFrame = FRAMES_PER_ROW - 1; // 0-4 (5 frames)
                // Center the sprite in canvas
                this.x = (canvas.width - SPRITE_WIDTH * SCALE_FACTOR) / 2;
                this.y = (canvas.height - SPRITE_HEIGHT * SCALE_FACTOR) / 2;
            }
            draw() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                if (this.image.complete) {
                    ctx.drawImage(
                        this.image,
                        this.frameX * SPRITE_WIDTH,
                        this.frameY * SPRITE_HEIGHT,
                        SPRITE_WIDTH,
                        SPRITE_HEIGHT,
                        this.x,
                        this.y,
                        SPRITE_WIDTH * SCALE_FACTOR,
                        SPRITE_HEIGHT * SCALE_FACTOR
                    );
                }
            }
            update() {
                this.frameX = this.frameX < this.maxFrame ? this.frameX + 1 : 0;
            }
            setRow(row) {
                this.frameY = row;
                this.frameX = 0;
            }
        }
        const demon = new Demon();
        let lastTime = 0;
        function animate(time) {
            if (time - lastTime >= FRAME_INTERVAL) {
                demon.draw();
                demon.update();
                lastTime = time;
            }
            requestAnimationFrame(animate);
        }
        window.setAnimation = function(row) {
            demon.setRow(row);
            document.querySelectorAll('button').forEach((btn, index) => {
                btn.classList.toggle('active', index === row);
            });
        }
        // Start animation
        demon.image.onload = () => {
            animate(0);
        };
        // Start immediately if image is cached
        if (demon.image.complete) {
            animate(0);
        }
    </script>
</html>