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
      background: #f4f4f4;
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
      color: #ddd;
    }

    .menu {
      padding: 15px;
      max-width: 600px;
      margin: auto;
    }

    .food-card {
      background: white;
      border-radius: 18px;
      margin-bottom: 20px;
      padding: 15px;
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
      background: #eeeeee;
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

    .cart h2 {
      margin-top: 0;
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
