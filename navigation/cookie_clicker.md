---
layout: page
title: Cookie Clicker
permalink: /cookie/
---

<div id="cookie-game-container" style="text-align: center; margin-top: 20px;">

  <img id="cookie" src="{{site.baseurl}}/images/cookie.png" alt="Cookie" style="cursor: pointer;" width="400px" height="450px">

  <h2>Cookies clicked: <span id="counter">0</span></h2>

</div>

<script>
  // Load the sound file
  const clickSound = new Audio('{{site.baseurl}}/mouse-click-sound.mp3'); // Replace with your sound file path

  let counter = 0;

  // Add event listener for cookie click
  document.getElementById('cookie').addEventListener('click', function() {
    // Play sound
    clickSound.play();

    // Update counter
    counter++;
    document.getElementById('counter').textContent = counter;
  });
</script>
