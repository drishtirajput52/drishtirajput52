<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Winter Cloth Sale</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-image: url('https://images.unsplash.com/photo-1457269449834-928af64c684d?ixlib=rb-4.0.3'); 
      background-size: cover;
      background-position: center;
      text-align: center;
      height: 100vh;
      overflow: hidden;
    }

    header {
      margin-top: 20px;
      color: white;
    }

    /* Blinking Light Effect on Heading */
    header h1 {
      font-size: 5em;
      font-weight: bold;
      color: #ff6347;
      text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.6);
      animation: blinkEffect 1.5s infinite alternate;
    }

    @keyframes blinkEffect {
      0% {
        color: #ff6347;
        text-shadow: 2px 2px 5px rgba(255, 255, 255, 0.8);
      }
      50% {
        color: #ffff00;
        text-shadow: 2px 2px 10px rgba(255, 255, 0, 0.8);
      }
      100% {
        color: #ff6347;
        text-shadow: 2px 2px 5px rgba(255, 255, 255, 0.8);
      }
    }

    nav {
      background-color: rgba(0, 0, 0, 0.6);
      padding: 10px;
    }

    nav a {
      color: white;
      text-decoration: none;
      margin: 0 20px;
      font-size: 1.2em;
    }

    nav a:hover {
      color: #ff6347;
    }

    .collection, .expanded-view {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 50px;
      margin-top: 50px;
      z-index: 2;
    }

    .item, .expanded-item {
      position: relative;
      width: 200px;
      height: 300px;
      cursor: pointer;
      transform: perspective(800px) rotateY(0deg);
      transition: transform 0.5s ease-in-out, box-shadow 0.3s ease-in-out;
    }

    .item:hover, .expanded-item:hover {
      transform: perspective(800px) rotateY(20deg);
      /* Glowing effect on hover */
      box-shadow: 0 0 20px 10px rgba(255, 255, 255, 0.8);
    }

    .item img, .expanded-item img {
      width: 100%;
      height: 100%;
      border-radius: 10px;
      object-fit: cover;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
    }

    .item p, .expanded-item p {
      display: none;
    }

    .bottom-text {
      position: fixed;
      bottom: 10px;
      left: 0;
      right: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 10px;
      color: white;
      font-size: 1.5em;
      text-align: center;
    }

    .back-arrow {
      position: fixed;
      top: 20px;
      left: 20px;
      font-size: 3em;
      color: #ffffff;
      cursor: pointer;
      display: none;
      z-index: 10;
      text-shadow: 0px 0px 8px rgba(0, 0, 0, 0.7);
      background: rgba(0, 0, 0, 0.6);
      padding: 10px;
      border-radius: 50%;
      box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.5);
    }

    .back-arrow.visible {
      display: block;
    }

    .hidden {
      display: none;
    }

    .price-container {
      position: absolute;
      bottom: 10px;
      left: 50%;
      transform: translateX(-50%);
      background-color: rgba(0, 0, 0, 0.6);
      padding: 10px;
      border-radius: 10px;
      color: white;
      font-size: 1.2em;
      display: flex;
      flex-direction: column;
      align-items: center;
      text-shadow: 0px 0px 10px rgba(255, 255, 255, 0.7);
    }

    .price-container .original-price {
      font-size: 1.5em;
      text-decoration: line-through;
      color: #d3d3d3;
    }

    .price-container .discounted-price {
      font-size: 1.8em;
      font-weight: bold;
      color: #ff6347;
    }

    .label {
      font-size: 1.5em;
      font-weight: bold;
      color: white;
      position: absolute;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      background-color: rgba(0, 0, 0, 0.6);
      padding: 5px 15px;
      border-radius: 5px;
    }
  </style>
</head>
<body>
  <nav>
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </nav>

  <header>
    <h1>WINTER CLOTH SALE!!</h1>
  </header>

  <div class="back-arrow" id="back-arrow" onclick="goBack()">&#8592;</div>

  <main>
    <div class="collection" id="initial-collection">
      <div class="item" onclick="showMorePictures('men')">
        <img src="https://d118ps6mg0w7om.cloudfront.net/media/catalog/product/a/w/fit-in/1000x1333/aw-23_4000x5000-10-10-24_msw-4521-r-57-maroon_1_msw-4521-r-57-maroon.jpg" alt="Men's Clothing">
        <div class="label">Men's Cloth</div>
      </div>
      <div class="item" onclick="showMorePictures('women')">
        <img src="https://images.bestsellerclothing.in/data/only/23-aug-2023/113263301_g0.jpg?width=380&height=500&mode=fill&fill=blur&format=auto" alt="Women's Clothing">
        <div class="label">Women's Cloth</div>
      </div>
    </div>

    <div class="expanded-view hidden" id="expanded-view"></div>

    <div class="bottom-text" id="bottom-text"></div>
  </main>

  <script>
    const picturesData = {
      men: [
        { src: "https://cdn.shopify.com/s/files/1/0088/7013/3865/files/cn56059908_360x.jpg?v=1725330074", label: "Men's Sweater - 4000 INR", originalPrice: 4000, discountedPrice: 2500 },
        { src: "https://rukminim2.flixcart.com/image/850/1000/xif0q/sweater/r/q/b/l-3-fold-men-sweater-sky-blue-myles-original-imagtc3f2z8udgbf.jpeg?q=20&crop=false", label: "Men's Jacket - 3000 INR", originalPrice: 2000, discountedPrice: 1000 },
        { src: "https://www.jiomart.com/images/product/original/rvru8eqxfx/kvetoo-men-high-neck-zip-full-sleeve-woolen-winter-sweater-product-images-rvru8eqxfx-0-202409201841.jpg", label: "Men's Coat - 5000 INR", originalPrice: 1000, discountedPrice: 800 },
      ],
      women: [
        { src: "https://img.tatacliq.com/images/i13/437Wx649H/MP000000018470145_437Wx649H_202308261400241.jpeg", label: "Women's Sweater - 4000 INR", originalPrice: 1000, discountedPrice: 800 },
        { src: "https://images.bestsellerclothing.in/data/only/20-aug-2024/112430901_g0.jpg?width=488&height=650&mode=fill&fill=blur&format=auto", label: "Women's Cardigan - 2500 INR", originalPrice: 3500, discountedPrice: 3000 },
        { src: "https://cdn.dsmcdn.com/ty906/product/media/images/20230525/17/360527360/853273349/1/1_org_zoom.jpg", label: "Women's Coat - 3000 INR", originalPrice: 5000, discountedPrice: 4500 },
      ]
    };
    function showMorePictures(gender) {
      const expandedView = document.getElementById("expanded-view");
      const collection = document.getElementById("initial-collection");
      const backArrow = document.getElementById("back-arrow");
      const bottomText = document.getElementById("bottom-text");
      expandedView.innerHTML = ''; // Clear existing content

      picturesData[gender].forEach(picture => {
        const item = document.createElement("div");
        item.classList.add("expanded-item");
        item.innerHTML = `
          <img src="${picture.src}" alt="${picture.label}">
          <div class="price-container">
            <div class="original-price">${picture.originalPrice} INR</div>
            <div class="discounted-price">${picture.discountedPrice} INR</div>
          </div>
          <p>${picture.label}</p>
        `;
        expandedView.appendChild(item);
      });

      collection.classList.add("hidden");
      expandedView.classList.remove("hidden");
      backArrow.classList.add("visible");
      bottomText.textContent = gender.charAt(0).toUpperCase() + gender.slice(1) + " Collection";
    }

    function goBack() {
      const expandedView = document.getElementById("expanded-view");
      const collection = document.getElementById("initial-collection");
      const backArrow = document.getElementById("back-arrow");
      const bottomText = document.getElementById("bottom-text");

      expandedView.classList.add("hidden");
      collection.classList.remove("hidden");
      backArrow.classList.remove("visible");
      bottomText.textContent = '';
    }
  </script>
</body>
</html>
