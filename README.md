<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>AR Food Menu</title>

  <script type="module"
    src="https://ajax.googleapis.com/ajax/libs/model-viewer/4.0.0/model-viewer.min.js">
  </script>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      color: #222;
    }

    header {
      background: #111;
      color: white;
      text-align: center;
      padding: 25px 15px;
    }

    header h1 {
      margin: 0;
      font-size: 28px;
    }

    header p {
      margin: 8px 0 0;
    }

    .menu {
      max-width: 600px;
      margin: auto;
      padding: 15px;
    }

    .food-card {
      background: white;
      margin-bottom: 20px;
      padding: 15px;
      border-radius: 18px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.12);
    }

    .food-card h2 {
      margin: 5px 0;
    }

    .price {
      font-size: 19px;
      font-weight: bold;
      margin: 8px 0 12px;
    }

    model-viewer {
      width: 100%;
      height: 300px;
      background: #eee;
      border-radius: 14px;
    }

    .add-button {
      width: 100%;
      padding: 14px;
      margin-top: 12px;
      border: none;
      border-radius: 10px;
      background: #ff9800;
      color: white;
      font-size: 17px;
      font-weight: bold;
    }

    .cart {
      max-width: 600px;
      margin: 15px auto 30px;
      background: white;
      padding: 18px;
      border-radius: 18px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.12);
    }

    .cart-item {
      border-bottom: 1px solid #ddd;
      padding: 12px 0;
    }

    .qty-button {
      border: none;
      background: #eee;
      padding: 7px 12px;
      border-radius: 7px;
      font-size: 16px;
      margin-top: 7px;
    }

    .total {
      font-size: 20px;
      font-weight: bold;
      margin: 18px 0;
    }

    input {
      width: 100%;
      padding: 13px;
      margin: 6px 0;
      border: 1px solid #ccc;
      border-radius: 9px;
      font-size: 16px;
    }

    .whatsapp {
      width: 100%;
      padding: 15px;
      margin-top: 12px;
      border: none;
      border-radius: 10px;
      background: #25D366;
      color: white;
      font-size: 18px;
      font-weight: bold;
    }
  </style>
</head>

<body>

<header>
  <h1>🍽️ AR Food Menu</h1>
  <p>View your food in AR before ordering</p>
</header>

<div class="menu">

  <!-- BURGER -->
  <div class="food-card">

    <h2>🍔 Burger</h2>

    <div class="price">₹120</div>

    <model-viewer
      src="burger_compressed_25mb.glb"
      alt="3D Burger"
      ar
      camera-controls
      auto-rotate
      shadow-intensity="1">
    </model-viewer>

    <button
      class="add-button"
      onclick="addItem('Burger',120)">
      🛒 Add Burger
    </button>

  </div>


  <!-- JUICE -->
  <div class="food-card">

    <h2>🥤 Fresh Juice</h2>

    <div class="price">₹80</div>

    <model-viewer
      src="7d8ad3b7-7254-474f-aefc-1ab51638e10f_dbcc9b7f7a131391594e130269ab4acd.glb"
      alt="3D Fresh Juice"
      ar
      camera-controls
      auto-rotate
      shadow-intensity="1">
    </model-viewer>

    <button
      class="add-button"
      onclick="addItem('Fresh Juice',80)">
      🛒 Add Juice
    </button>

  </div>

</div>


<!-- CART -->
<div class="cart">

  <h2>🛒 Your Order</h2>

  <div id="cartItems">
    Your cart is empty.
  </div>

  <div class="total" id="total">
    Total: ₹0
  </div>

  <input
    id="customerName"
    type="text"
    placeholder="Enter your name">

  <input
    id="tableNumber"
    type="text"
    placeholder="Enter table number">

  <button
    class="whatsapp"
    onclick="sendWhatsApp()">
    🟢 Order on WhatsApp
  </button>

</div>


<script>

let cart = [];


/* ADD ITEM */
function addItem(name, price) {

  const item = cart.find(
    product => product.name === name
  );

  if (item) {
    item.quantity++;
  } else {
    cart.push({
      name: name,
      price: price,
      quantity: 1
    });
  }

  updateCart();
}


/* REMOVE ITEM */
function removeItem(name) {

  const item = cart.find(
    product => product.name === name
  );

  if (!item) return;

  item.quantity--;

  if (item.quantity <= 0) {
    cart = cart.filter(
      product => product.name !== name
    );
  }

  updateCart();
}


/* UPDATE CART */
function updateCart() {

  const cartBox =
    document.getElementById("cartItems");

  const totalBox =
    document.getElementById("total");

  if (cart.length === 0) {

    cartBox.innerHTML =
      "Your cart is empty.";

    totalBox.innerHTML =
      "Total: ₹0";

    return;
  }

  let html = "";
  let total = 0;

  cart.forEach(item => {

    const subtotal =
      item.price * item.quantity;

    total += subtotal;

    html += `
      <div class="cart-item">

        <strong>${item.name}</strong>

        <br>

        ₹${item.price} × ${item.quantity}
        = ₹${subtotal}

        <br>

        <button
          class="qty-button"
          onclick="removeItem('${item.name}')">
          ➖
        </button>

        <button
          class="qty-button"
          onclick="addItem('${item.name}',${item.price})">
          ➕
        </button>

      </div>
    `;
  });

  cartBox.innerHTML = html;

  totalBox.innerHTML =
    "Total: ₹" + total;
}


/* WHATSAPP ORDER */
function sendWhatsApp() {

  if (cart.length === 0) {
    alert("Please add an item first.");
    return;
  }

  const customerName =
    document
      .getElementById("customerName")
      .value
      .trim();

  const tableNumber =
    document
      .getElementById("tableNumber")
      .value
      .trim();

  if (!customerName) {
    alert("Please enter your name.");
    return;
  }

  if (!tableNumber) {
    alert("Please enter your table number.");
    return;
  }

  let total = 0;

  let message =
    "🍽️ NEW RESTAURANT ORDER\n\n";

  message +=
    "👤 Name: " +
    customerName +
    "\n";

  message +=
    "🪑 Table: " +
    tableNumber +
    "\n\n";

  message +=
    "📋 ORDER DETAILS\n";

  cart.forEach(item => {

    const subtotal =
      item.price * item.quantity;

    total += subtotal;

    message +=
      item.quantity +
      " × " +
      item.name +
      " = ₹" +
      subtotal +
      "\n";
  });

  message +=
    "\n💰 TOTAL: ₹" +
    total;


  /* RESTAURANT WHATSAPP NUMBER */
  const restaurantNumber =
    "918446348928";


  const whatsappLink =
    "https://wa.me/918446348928?text=Hello%20I%20want%20to%20place%20an%20order" +
    restaurantNumber +
    "?text=" +
    encodeURIComponent(message);


  window.open(
    whatsappLink,
    "_blank"
  );
}

</script>

</body>
</html>
