---
layout: page
title: About Me
permalink: /about/
---

<h3 style="font-family: Courier New"> <strong> My name is Avika Prasad and I am a sophomore at Del Norte High School. I want to pursue computer science in the future! Some things I like to do in my free time are dance and listen to music. I'm excited to continue learning computer science principles. </strong> </h3>

<div>
<center>
<img src="{{site.baseurl}}/images/avika.png" width="300" height ="350"/>
<div>
<a href="https://www.linkedin.com/in/avika-prasad-157b332a6/" target="_blank">
<button style="background-color: #017371; color: white; padding: 10px">My LinkedIn</button>
</a>
<br>

<h2> <strong> Ancestry: I am Indian and I come from a family of generational hindi-speakers. </strong> </h2>
<span>
<img src="{{site.baseurl}}/images/indian flag.gif" width="200" height="150"> 
<img src="{{site.baseurl}}/images/avika_in_hindi.png" alt="my name in hindi script!">
<h3 style="font-family: Courier New"> <strong> My name in Hindi!  👆🏻 😃 </strong> </h3>
</span>

<h3 style="font-family: Courier New"> <strong>  I was born in India and I moved to the US the summer before first grade.</strong> </h3>
<h3 style="font-family: Courier New"> <strong> Since then I have lived in 3 states, and 4 different places. St. Louis, Missouri, Edison, New Jersey, Cupertino, CA and finally San Diego, CA</strong> </h3>

<h3 style="font-family: Courier New"> <strong>I went to Oak Valley Middle School and now I will graduate Del Norte in 2027.</strong> </h3>

<br>

<comment>
Programming languages are made using Wikipedia images
</comment>

<br>

<style>
    /* Style looks pretty compact, 
       - grid-container and grid-item are referenced the code 
    */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
        align-items: center;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }

    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
        }

    .image-gallery img {
        max-height: 150px;
        object-fit: cover;
        border-radius: 5px;
    }
</style>

<!-- This grid_container class is used by CSS styling and the id is used by JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container"); // This container connects to the HTML div

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
    {"flag": "c/c3/Python-logo-notext.svg", "greeting": "Python", "description": "I've learned"},
    {"flag": "3/38/HTML5_Badge.svg", "greeting": "HTML", "description": "I'm learning"},
    {"flag": "6/62/CSS3_logo.svg", "greeting": "CSS", "description": "I'm learning"},
    {"flag": "9/99/Unofficial_JavaScript_logo_2.svg", "greeting": "JavaScript", "description": "I want to learn"}
];

    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";  // This class name connects the gridItem to the CSS style elements
        // Add "img" HTML tag for the flag
        var img = document.createElement("img");
        img.src = http_source + location.flag; // concatenate the source and flag
        img.alt = location.flag + " Flag"; // add alt text for accessibility

        // Add "p" HTML tag for the description
        var description = document.createElement("p");
        description.textContent = location.description; // extract the description

        // Add "p" HTML tag for the greeting
        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;  // extract the greeting

        // Append img and p HTML tags to the grid item DIV
        gridItem.appendChild(img);
        gridItem.appendChild(description);
        gridItem.appendChild(greeting);

        // Append the grid item DIV to the container DIV
        container.appendChild(gridItem);
    }
</script>

<div>
<a href="http://127.0.0.1:4100/avika_2025/">
<button style="background-color: #F88379; color: white; padding: 10px"> Back To Homepage </button> </a>
</div>

<script src="https://utteranc.es/client.js"
        repo="nighthawkcoders/portfolio_2025"
        issue-term="title"
        label="blogpost-comment"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script> 

<!-- Adding Changing Background Color -->
<script>
  let colors = ["#FFFAF0", "#FFFACD", "#E6E6FA", "#F5FFFA"];
  let currentColor = 0;
  setInterval(function() {
    document.body.style.backgroundColor = colors[currentColor];
    currentColor = (currentColor + 1) % colors.length;
  }, 5000); // Change color every 5 seconds
</script>