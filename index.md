---
layout: post 
title: Soni Dhenuva
description: A highschooler in CS
author: Soni Dhenuva
image: /images/mario_animation.png
hide: true
menu: nav/home.html
---

<!-- Liquid:  statements-->

<!--- Concatenation of site URL to frontmatter image  --->
{% assign sprite_file = site.baseurl | append: page.image %}
<!--- Has is a list variable containing mario metadata for sprite --->
{% assign hash = site.data.mario_metadata %}  
<!--- Size width/height of Sprit images --->
{% assign pixels = 256 %}

<!--- HTML for page contains <p> tag named "Mario" and class properties for a "sprite"  -->

<p id="mario" class="sprite"></p>
  
<!--- Embedded Cascading Style Sheet (CSS) rules, 
        define how HTML elements look 
--->
<style>

  /*CSS style rules for the id and class of the sprite...
  */
  .sprite {
    height: {{pixels}}px;
    width: {{pixels}}px;
    background-image: url('{{sprite_file}}');
    background-repeat: no-repeat;
  }

  /*background position of sprite element
  */
  #mario {
    background-position: calc({{animations[0].col}} * {{pixels}} * -1px) calc({{animations[0].row}} * {{pixels}}* -1px);
  }
</style>

<!--- Embedded executable code--->
<script>
  ////////// convert YML hash to javascript key:value objects /////////

  var mario_metadata = {}; //key, value object
  {% for key in hash %}  
  
  var key = "{{key | first}}"  //key
  var values = {} //values object
  values["row"] = {{key.row}}
  values["col"] = {{key.col}}
  values["frames"] = {{key.frames}}
  mario_metadata[key] = values; //key with values added

  {% endfor %}

  ////////// game object for player /////////

  class Mario {
    constructor(meta_data) {
      this.tID = null;  //capture setInterval() task ID
      this.positionX = 0;  // current position of sprite in X direction
      this.currentSpeed = 0;
      this.marioElement = document.getElementById("mario"); //HTML element of sprite
      this.pixels = {{pixels}}; //pixel offset of images in the sprite, set by liquid constant
      this.interval = 100; //animation time interval
      this.obj = meta_data;
      this.marioElement.style.position = "absolute";
    }

    animate(obj, speed) {
      let frame = 0;
      const row = obj.row * this.pixels;
      this.currentSpeed = speed;

      this.tID = setInterval(() => {
        const col = (frame + obj.col) * this.pixels;
        this.marioElement.style.backgroundPosition = `-${col}px -${row}px`;
        this.marioElement.style.left = `${this.positionX}px`;

        this.positionX += speed;
        frame = (frame + 1) % obj.frames;

        const viewportWidth = window.innerWidth;
        if (this.positionX > viewportWidth - this.pixels) {
          document.documentElement.scrollLeft = this.positionX - viewportWidth + this.pixels;
        }
      }, this.interval);
    }

    startWalking() {
      this.stopAnimate();
      this.animate(this.obj["Walk"], 3);
    }

    startWalkingL() {
      this.stopAnimate();
      this.animate(this.obj["WalkL"], -3);
    }

    startRunning() {
      this.stopAnimate();
      this.animate(this.obj["Run1"], 6);
    }

    startRunningL() {
      this.stopAnimate();
      this.animate(this.obj["Run1L"], -6);
    }

    startPuffing() {
      this.stopAnimate();
      this.animate(this.obj["Puff"], 0);
    }

    startPuffingL() {
      this.stopAnimate();
      this.animate(this.obj["PuffL"], 0);
    }

    startCheering() {
      this.stopAnimate();
      this.animate(this.obj["Cheer"], 0);
    }

    startCheeringL() {
      this.stopAnimate();
      this.animate(this.obj["CheerL"], 0);
    }

    startFlipping() {
      this.stopAnimate();
      this.animate(this.obj["Flip"], 0);
    }

    startFlippingL() {
      this.stopAnimate();
      this.animate(this.obj["FlipL"], 0);
    }

    startResting() {
      this.stopAnimate();
      this.animate(this.obj["Rest"], 0);
    }

    startRestingL() {
      this.stopAnimate();
      this.animate(this.obj["RestL"], 0);
    }

    stopAnimate() {
      clearInterval(this.tID);
    }
  }

  const mario = new Mario(mario_metadata);

  ////////// event control /////////

// Add event listener for keydown events
  window.addEventListener("keydown", (event) => {
      if (event.key === "ArrowRight" || event.key === "d" || event.key === "D") {
          event.preventDefault();
          if (event.repeat) {
              mario.startCheering();
          } else {
              if (mario.currentSpeed === 0) {
                  mario.startWalking();
              } else if (mario.currentSpeed === 3) {
                  mario.startRunning();
              }
          }
      } else if (event.key === "ArrowLeft" || event.key === "a" || event.key === "A") {
          event.preventDefault();
          if (event.repeat) {
              mario.startCheeringL();
          } else {
              if (mario.currentSpeed === 0) {
                  mario.startWalkingL();
              } else if (mario.currentSpeed === 3) {
                  mario.startRunningL();
              }
          }
      } else if (event.key === "ArrowUp" || event.key === "w" || event.key === "W") {
          event.preventDefault();
          mario.startFlipping();
      } else if (event.key === "ArrowDown" || event.key === "s" || event.key === "S") {
          event.preventDefault();
          mario.startResting();
      }
  });
  
  // Add event listener for touchstart events
  window.addEventListener("touchstart", (event) => {
      event.preventDefault(); // prevent default browser action
      const touchX = event.touches[0].clientX;
      const screenWidth = window.innerWidth;
      const centerThreshold = screenWidth * 0.1; // 10% of the screen width on either side of the center

      if (touchX > screenWidth / 2 + centerThreshold) {
          // move right
          if (mario.currentSpeed === 0) {
              mario.startWalking();
          } else if (mario.currentSpeed === 3) {
              mario.startRunning();
          }
      } else if (touchX < screenWidth / 2 - centerThreshold) {
          // move left
          if (mario.currentSpeed === 0) {
              mario.startWalkingL();
          } else if (mario.currentSpeed === 3) {
              mario.startRunningL();
          }
      } else {
          // touch near the center, make Mario puff
          mario.startPuffing();
      }
  });

  //stop animation on window blur
  window.addEventListener("blur", () => {
    mario.stopAnimate();
  });

  //start animation on window focus
  window.addEventListener("focus", () => {
     mario.startFlipping();
  });

  //start animation on page load or page refresh
  document.addEventListener("DOMContentLoaded", () => {
    // adjust sprite size for high pixel density devices
    const scale = window.devicePixelRatio;
    const sprite = document.querySelector(".sprite");
    sprite.style.transform = `scale(${0.2 * scale})`;
    mario.startResting();
  });

</script>

## Intro
<p>Hi, My name is Sonika Dhenuva Konda, I go by Soni. I am in 10th grade and 15 years old.</p>
<p>I joined a few clubs at school like Robotics & Debate. I also own my own small buisness of selling jewlry</p>

## My Favorites
<p>My favorite food is icecream, i also love any type of chocolate</p>
<p>I also have several favorite movie such as all Ironman, Deadpool, Spiderman, Sherlock Homes, Transformers, Rush Hour, Jurrasic World, etc</p>
<img src="{{site.baseurl}}/images/jurassic.png">
<img src="{{site.baseurl}}/images/deadpool.png">
<img src="{{site.baseurl}}/images/spiderman.png">


## My Family
<p>Fun Fact! I was actually born in india. I moved here when I was 9 months old. My dad and mom are both from India, and I have a younger sister who is 9 years old.</p>
<p> A huge part of my family, including grandparents, aunts, uncles, and cousin are in Indian and I love to go and visit then once in a few years!</p>
<img src="{{site.baseurl}}/images/india.png">
<img src="{{site.baseurl}}/images/food.png">