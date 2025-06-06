<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Responsive Carousel & API Example</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      text-align: center;
      background-color: #f0f0f0;
    }

    header {
      background-color: #333;
      color: white;
      padding: 1rem;
      font-size: 1.5rem;
    }

    .container {
      padding: 1rem;
    }

    /* Carousel */
    .carousel {
      position: relative;
      max-width: 600px;
      margin: 2rem auto;
    }

    .carousel img {
      width: 100%;
      border-radius: 10px;
      display: none;
    }

    .carousel img.active {
      display: block;
    }

    /* Joke Box */
    #joke-box {
      background: #fff;
      padding: 1.5rem;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      margin: 2rem auto;
      max-width: 500px;
    }

    button {
      padding: 0.5rem 1rem;
      font-size: 1rem;
      margin-top: 1rem;
      cursor: pointer;
    }

    /* Media Queries */
    @media (max-width: 768px) {
      header {
        font-size: 1.2rem;
      }

      button {
        font-size: 0.9rem;
      }

      #joke-box {
        margin: 1rem;
      }
    }

    @media (max-width: 480px) {
      .carousel {
        width: 90%;
      }

      button {
        padding: 0.4rem 0.8rem;
      }
    }
  </style>
</head>
<body>

  <header>Responsive Web App with Auto-Carousel and API</header>

  <div class="container">

    <!-- Image Carousel -->
    <div class="carousel">
      <img src="https://via.placeholder.com/600x300?text=Image+1" class="active" alt="Image 1">
      <img src="https://via.placeholder.com/600x300?text=Image+2" alt="Image 2">
      <img src="https://via.placeholder.com/600x300?text=Image+3" alt="Image 3">
    </div>

    <!-- Joke API Box -->
    <div id="joke-box">
      <h2>Random Joke</h2>
      <p id="setup">Loading...</p>
      <p id="punchline"></p>
      <button onclick="fetchJoke()">Get Another Joke</button>
    </div>

  </div>

  <script>
    // Auto Image Carousel Logic
    let index = 0;
    const images = document.querySelectorAll('.carousel img');

    function showImage(idx) {
      images.forEach((img, i) => {
        img.classList.remove('active');
        if (i === idx) img.classList.add('active');
      });
    }

    function autoSlide() {
      index = (index + 1) % images.length;
      showImage(index);
    }

    // Start carousel auto-slide
    setInterval(autoSlide, 3000); // change every 3 seconds

    // Joke API Logic
    async function fetchJoke() {
      try {
        const res = await fetch('https://official-joke-api.appspot.com/random_joke');
        const data = await res.json();
        document.getElementById('setup').textContent = data.setup;
        document.getElementById('punchline').textContent = data.punchline;
      } catch (error) {
        document.getElementById('setup').textContent = "Error fetching joke.";
        document.getElementById('punchline').textContent = "";
      }
    }

    // Load joke on page load
    window.onload = fetchJoke;
  </script>

</body>
</html>