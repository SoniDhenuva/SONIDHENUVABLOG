---
layout: post
title: Cookie
description: This is my cookie clicker game
type: ccc
courses: {'csp': {'week': 7}}
comments: True
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie Clicker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f5f5f5;
        }
        .game-container {
            text-align: center;
        }
        .cookie-button {
            cursor: pointer;
            background: none;
            border: none;
            outline: none;
            font-size: 150px; /* Size of the cookie */
            transition: transform 0.2s;
        }
        .cookie-button:hover {
            transform: scale(1.1);
        }
        .cookie-count {
            font-size: 36px;
            margin: 20px 0;
            color: white; /* Set text color to white */
        }
        .buy-button {
            padding: 10px 20px;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            background-color: #4caf50;
            color: white; /* Set button text color to white */
            cursor: pointer;
            margin: 10px;
            transition: background-color 0.3s;
        }
        .buy-button:hover {
            background-color: #45a049;
        }
        .info {
            font-size: 16px;
            margin: 10px 0;
            color: white; /* Set info text color to white */
        }
    </style>
</head>
<body>

<div class="game-container">
    <!-- Preload the audio and set its volume -->
    <audio id="clickSound" src="{{site.baseurl}}/coin.mp3" preload="auto"></audio>
    <button id="cookieButton" class="cookie-button" onclick="cookieClick()">
        🍪
    </button>
    <div id="cookieCount" class="cookie-count">Cookies: 0</div>
    <div id="productionRate" class="info">Cookies per second: 0</div>
    <div id="upgradeSection">
        <div class="info">
            <button id="buyGrandma" class="buy-button">Buy Grandma: +1 Cookie/Second (Cost: 50 Cookies)</button>
            <button id="buyFactory" class="buy-button">Buy Factory: +5 Cookies/Second (Cost: 500 Cookies)</button>
        </div>
    </div>
</div>

<script>
    let cookieCount = 0;
    let cookiesPerClick = 1;
    let cookiesPerSecond = 0;
    let grandmaCost = 50;
    let factoryCost = 500;

    // Function to play the click sound
    function playClickSound() {
        const sound = document.getElementById('clickSound');
        sound.currentTime = 0;  // Reset sound to the beginning
        sound.play();
    }

    function updateDisplay() {
        document.getElementById('cookieCount').textContent = `Cookies: ${cookieCount}`;
        document.getElementById('productionRate').textContent = `Cookies per second: ${cookiesPerSecond}`;
        document.getElementById('buyGrandma').textContent = `Buy Grandma: +1 Cookie/Second (Cost: ${grandmaCost} Cookies)👵`;
        document.getElementById('buyFactory').textContent = `Buy Factory: +5 Cookies/Second (Cost: ${factoryCost} Cookies) 🏭`;
    }

    function cookieClick() {
        cookieCount += cookiesPerClick;
        updateDisplay();
        playClickSound(); // Play the sound when the cookie is clicked
    }

    document.getElementById('buyGrandma').onclick = function() {
        if (cookieCount >= grandmaCost) {
            cookieCount -= grandmaCost;
            cookiesPerSecond += 1;
            grandmaCost = Math.floor(grandmaCost * 1.15); // Increase cost for next Grandma
            updateDisplay();
        } else {
            alert('Not enough cookies for Grandma!');
        }
    };

    document.getElementById('buyFactory').onclick = function() {
        if (cookieCount >= factoryCost) {
            cookieCount -= factoryCost;
            cookiesPerSecond += 5;
            factoryCost = Math.floor(factoryCost * 1.15); // Increase cost for next Factory
            updateDisplay();
        } else {
            alert('Not enough cookies for Factory!');
        }
    };

    function increaseCookies() {
        cookieCount += cookiesPerSecond;
        updateDisplay();
    }

    setInterval(increaseCookies, 1000);
</script>

</body>
</html>
