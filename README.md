<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>AR Restaurant Menu</title>

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
      padding: 22px 15px;
    }

    header h1 {
      margin: 0 0 8px;
    }

    header p {
      margin: 0;
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

    .item h2 {
      margin: 0 0 5px;
    }

    .price {
      font-size: 18px;
      font-weight: bold;
      margin: 8px 0 12px;
    }

    model-viewer {
      width: 100%;
      height: 280px;
      background: #eee;
      border-radius: 12px;
    }

    button {
      border: none;
      border-radius: 8px;
      padding: 12px 18px;
      margin-top: 10px;
      font-size: 16px;
      cursor: pointer;
    }

    .cart-btn {
      background: #ff9800;
      color: white;
      width: 100%;
    }

    #cart {
      background: white;
      margin: 15px;
      padding: 18px;
      border-radius: 15px;
      box-shadow: 0 3px 10px #ccc;
    }

    #cartItems {
      margin-bottom: 10px;
    }

    .cart-item {
      padding: 10px 0;
      border-bottom: 1px solid #ddd;
    }

    .quantity button {
      padding: 6px 12px;
      margin: 5px 3px 0 0;
      background: #eee;
      color: #222;
    }

    input {
      width: 100%;
      padding: 13px;
      margin: 7px 0;
      border: 1px solid #ccc;
      border-radius: 8px;
      font-size: 16px;
    }

    .order-btn {
      background: #25D366;
      color: white;
      width: 100%;
      font-size: 18px;
      font-weight: bold;
    }
  </style>
</head>

<body>

<header>
  <h1>🍽
