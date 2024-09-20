---
layout: base
title: ✨ Avika's Homepage ✨
description: 😃🔥💃🏻✨‼️
image: /images/mario_animation.png
hide: true
---
<center>
<h3 style="font-family: Courier New"> <strong> Hi I'm Avika, and my journey in computer science princples journey starts here. </strong> </h3>
<span class="container">
<img src="{{site.baseurl}}/images/comp.gif" width="300" height="300"/>
<img src="{{site.baseurl}}/images/duck.gif" width="250" height="250"/>
<div>

<h3 style="font-family: Courier New"> <strong> Press right-arrow to make Mario move! </strong></h3>

<h3 style="font-family: Courier New"> <strong>Press left-arrow to make him stop and rest!</strong></h3>

<h3 style="font-family: Courier New"> <strong>Press the up-arrow and right-arrow together to make him jog!</strong></h3>

<h3 style="font-family: Courier New"> <strong>Switch tabs and come back for a surprise!</strong></h3>

<table>
  <tr>
    <th>Github Pages Hacks</th>
    <th>Games</th>
  </tr>
  <tr>
    <td> <a href="{{site.baseurl}}/emoji/"> <button style="background-color: #F88379; color: white; padding: 10px"> Emoji Notebook </button> </a> </td> 
    <td> <a href="{{site.baseurl}}/snake/"> <button style="background-color: #F88379; color: white; padding: 10px"> Snake Game </button> </a> </td>
  </tr>
  <tr>
    <td> <a href="{{site.baseurl}}/frontend/"> <button style="background-color: #F88379; color: white; padding: 10px"> Frontend </button> </a> </td> 
    <td> <a href="{{site.baseurl}}/cookie/"> <button style="background-color: #F88379; color: white; padding: 10px"> Cookie Clicker </button> </a> </td>
  </tr>
  <tr>
    <td> <a href="{{site.baseurl}}/music/"> <button style="background-color: #F88379; color: white; padding: 10px"> Music Blog </button> </a> </td> 
    <td>
    <a href="{{site.baseurl}}/calculator/"> <button style="background-color: #F88379; color: white; padding: 10px"> Calculator </button> </a> </td>
  </tr>
</table>

<!-- Liquid:  statements -->

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

    startRunning() {
      this.stopAnimate();
      this.animate(this.obj["Run1"], 6);
    }

    startPuffing() {
      this.stopAnimate();
      this.animate(this.obj["Puff"], 0);
    }

    startCheering() {
      this.stopAnimate();
      this.animate(this.obj["Cheer"], 0);
    }

    startFlipping() {
      this.stopAnimate();
      this.animate(this.obj["Flip"], 0);
    }

    startResting() {
      this.stopAnimate();
      this.animate(this.obj["Rest"], 0);
    }

    stopAnimate() {
      clearInterval(this.tID);
    }
  }

  const mario = new Mario(mario_metadata);

  ////////// event control /////////

  window.addEventListener("keydown", (event) => {
    if (event.key === "ArrowRight") {
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
    } else if (event.key === "ArrowLeft") {
      event.preventDefault();
      if (event.repeat) {
        mario.stopAnimate();
      } else {
        mario.startPuffing();
      }
    }
  });

  //touch events that enable animations
  window.addEventListener("touchstart", (event) => {
    event.preventDefault(); // prevent default browser action
    if (event.touches[0].clientX > window.innerWidth / 2) {
      // move right
      if (currentSpeed === 0) { // if at rest, go to walking
        mario.startWalking();
      } else if (currentSpeed === 3) { // if walking, go to running
        mario.startRunning();
      }
    } else {
      // move left
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


