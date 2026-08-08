# AR-menu-whatsapp-<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>AR Restaurant Menu</title>

  <script type="module"
    src="https://ajax.googleapis.com/ajax/libs/model-viewer/4.0.0/model-viewer.min.js">
  </script>

  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f5f5f5;
    }

    header {
      background: #111;
      color: white;
      padding: 20px;
      text-align: center;
    }

    .menu {
      padding: 15px;
    }

    .item {
      background: white;
      margin-bottom: 20px;
      padding: 15px;
      border-radius: 15px;
      box-shadow: 0 3px 10px #ccc;
    }

    model-viewer {
      width: 100%;
      height: 280px;
      background: #eee;
      border-radius: 12px;
    }

    h2 {
      margin-bottom: 5px;
    }

    .price {
      font-size: 18px;
      font-weight: bold;
    }

    button {
      border: none;
      border-radius: 8px;
      padding: 12px 18px;
      margin: 5px;
      font-size: 15px;
      cursor: pointer;
    }

    .cart-btn {
      background: #ff9800;
      color: white;
    }

    .order-btn {
      background: #25D366;
      color: white;
      width: 100%;
      font-size: 18px;
    }

    #cart {
      background: white;
      margin: 15px;
      padding: 15px;
      border-radius: 15px;
    }

    input {
      width: 90%;
      padding: 12px;
      margin: 6px 0;
      border: 1px solid #ccc;
      border-radius: 8px;
    }
  </style>
</head>

<body>

<header>
  <h1>🍽️ AR Restaurant Menu</h1>
  <p>See your food in AR</p>
</header>

<div class="menu">

  <!-- BURGER -->
  <div class="item">
    <h2>🍔 Burger</h2>
    <p class="price">₹120</p>

    <model-viewer
      src="burger.glb"
      ar
      camera-controls
      auto-rotate>
    </model-viewer>

    <button class="cart-btn" onclick="addToCart('Burger',120)">
      Add to Cart
    </button>
  </div>

  <!-- PIZZA -->
  <div class="item">
    <h2>🍕 Pizza</h2>
    <p class="price">₹180</p>

    <model-viewer
      src="pizza.glb"
      ar
      camera-controls
      auto-rotate>
    </model-viewer>

    <button class="cart-btn" onclick="addToCart('Pizza',180)">
      Add to Cart
    </button>
  </div>

  <!-- BIRYANI -->
  <div class="item">
    <h2>🍗 Chicken Biryani</h2>
    <p class="price">₹200</p>

    <model-viewer
      src="biryani.glb"
      ar
      camera-controls
      auto-rotate>
    </model-viewer>

    <button class="cart-btn" onclick="addToCart('Chicken Biryani',200)">
      Add to Cart
    </button>
  </div>

</div>

<div id="cart">
  <h2>🛒 Your Cart</h2>

  <div id="cartItems">
    Cart is empty
  </div>

  <h3 id="total">Total: ₹0</h3>

  <input id="name" placeholder="Your Name">

  <input id="table" placeholder="Table Number">

  <button class="order-btn" onclick="orderWhatsApp()">
    🟢 Order on WhatsApp
  </button>
</div>

<script>

let cart = [];

function addToCart(name, price) {

  let existing = cart.find(item => item.name === name);

  if (existing) {
    existing.quantity++;
  } else {
    cart.push({
      name: name,
      price: price,
      quantity: 1
    });
  }

  updateCart();
}

function removeFromCart(name) {

  let item = cart.find(item => item.name === name);

  if (item) {
    item.quantity--;

    if (item.quantity <= 0) {
      cart = cart.filter(x => x.name !== name);
    }
  }

  updateCart();
}

function updateCart() {

  let html = "";
  let total = 0;

  if (cart.length === 0) {
    html = "Cart is empty";
  }

  cart.forEach(item => {

    let subtotal = item.price * item.quantity;

    total += subtotal;

    html += `
      <div style="margin-bottom:10px;">
        <b>${item.name}</b><br>
        ₹${item.price} × ${item.quantity}
        = ₹${subtotal}

        <br>

        <button onclick="removeFromCart('${item.name}')">
          ➖
        </button>

        <button onclick="addToCart('${item.name}',${item.price})">
          ➕
        </button>
      </div>
    `;
  });

  document.getElementById("cartItems").innerHTML = html;
  document.getElementById("total").innerText =
    "Total: ₹" + total;
}

function orderWhatsApp() {

  let name = document.getElementById("name").value;
  let table = document.getElementById("table").value;

  if (cart.length === 0) {
    alert("Please add something to your cart.");
    return;
  }

  if (name === "" || table === "") {
    alert("Please enter your name and table number.");
    return;
  }

  let message = "🍽️ *NEW ORDER*%0A%0A";

  message += "👤 Name: " + name + "%0A";
  message += "🪑 Table: " + table + "%0A%0A";

  let total = 0;

  cart.forEach(item => {

    let subtotal = item.price * item.quantity;

    total += subtotal;

    message +=
      item.quantity + " × " +
      item.name +
      " = ₹" +
      subtotal +
      "%0A";
  });

  message += "%0A💰 *Total: ₹" + total + "*";

  // REPLACE THIS WITH THE CAFE'S WHATSAPP NUMBER
  let phone = "91XXXXXXXXXX";

  let url =
    "https://wa.me/" +
    phone +
    "?text=" +
    message;

  window.open(url, "_blank");
}

</script>

</body>
</html>
