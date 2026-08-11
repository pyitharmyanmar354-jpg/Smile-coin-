<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Smile Coin - Game Top Up</title>

<style>
*{box-sizing:border-box}
body{
  margin:0;
  font-family:Arial,sans-serif;
  background:#111;
  color:white;
}
header{
  background:#171717;
  padding:18px;
  text-align:center;
  border-bottom:1px solid #333;
}
.logo{
  font-size:28px;
  font-weight:bold;
  color:#ff9d00;
}
.hero{
  padding:45px 20px;
  text-align:center;
  background:linear-gradient(135deg,#251400,#111);
}
.hero h1{
  font-size:40px;
  margin:10px 0;
}
.hero p{
  color:#ccc;
  font-size:18px;
}
button{
  background:#ff9d00;
  color:#111;
  border:0;
  border-radius:10px;
  padding:13px 22px;
  font-weight:bold;
  font-size:15px;
  cursor:pointer;
}
button:hover{
  background:#ffb52e;
}
.cards{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:15px;
  padding:20px;
}
.card{
  background:#202020;
  border-radius:16px;
  padding:25px 10px;
  text-align:center;
  border:1px solid #292929;
}
.card h2{
  font-size:19px;
}
.card p{
  color:#ccc;
}
.price{
  color:#ffb52e;
  font-weight:bold;
  margin:12px 0;
}
.section{
  padding:20px;
}
.form-box{
  display:none;
  background:#202020;
  margin:10px 20px 25px;
  padding:22px;
  border-radius:16px;
}
.form-box h2{
  color:#ff9d00;
  margin-top:0;
}
input,select{
  width:100%;
  padding:14px;
  margin:8px 0;
  border-radius:9px;
  border:1px solid #444;
  background:#111;
  color:white;
  font-size:16px;
}
label{
  display:block;
  margin-top:10px;
  color:#ddd;
}
.total{
  font-size:20px;
  color:#ffb52e;
  font-weight:bold;
  margin:18px 0;
}
.order{
  display:none;
  background:#171717;
  border:1px solid #ff9d00;
  margin:20px;
  padding:20px;
  border-radius:15px;
}
footer{
  text-align:center;
  padding:30px;
  color:#888;
}
@media(max-width:600px){
  .cards{
    grid-template-columns:1fr 1fr;
  }
}
</style>
</head>

<body>

<header>
  <div class="logo">🪙 SMILE COIN</div>
</header>

<section class="hero">
  <h1>Smile Coin</h1>
  <p>Fast & Easy Game Top-up Service</p>
  <button onclick="openGame('PUBG')">TOP UP NOW</button>
</section>

<div class="cards">

  <div class="card">
    <h2>🎮 PUBG Mobile</h2>
    <p>UC Top-up</p>
    <div class="price">From 50 THB</div>
    <button onclick="openGame('PUBG')">TOP UP</button>
  </div>

  <div class="card">
    <h2>💎 Mobile Legends</h2>
    <p>Diamonds Top-up</p>
    <div class="price">From 20 THB</div>
    <button onclick="openGame('MLBB')">TOP UP</button>
  </div>

  <div class="card">
    <h2>🇹🇭 THB</h2>
    <p>Thai Baht</p>
    <button onclick="setCurrency('THB')">SELECT</button>
  </div>

  <div class="card">
    <h2>🇲🇲 MMK</h2>
    <p>Myanmar Kyat</p>
    <button onclick="setCurrency('MMK')">SELECT</button>
  </div>

</div>

<div class="form-box" id="formBox">

  <h2 id="gameTitle">🎮 PUBG Mobile</h2>

  <label>Player ID / User ID</label>
  <input type="text" id="playerId" placeholder="Enter Player ID">

  <label>Server ID (MLBB only)</label>
  <input type="text" id="serverId" placeholder="Enter Server ID">

  <label>Package</label>
  <select id="package" onchange="calculate()">
    <option value="50">50 Coins / UC - 50 THB</option>
    <option value="100">100 Coins / UC - 100 THB</option>
    <option value="300">300 Coins / UC - 250 THB</option>
    <option value="500">500 Coins / UC - 400 THB</option>
    <option value="1000">1000 Coins / UC - 750 THB</option>
  </select>

  <label>Currency</label>
  <select id="currency" onchange="calculate()">
    <option value="THB">🇹🇭 THB</option>
    <option value="MMK">🇲🇲 MMK</option>
  </select>

  <div class="total" id="total">
    Total: 50 THB
  </div>

  <button onclick="placeOrder()">🛒 PLACE ORDER</button>

</div>

<div class="order" id="orderBox">
  <h2>✅ Order Created</h2>
  <p id="orderText"></p>
  <p>📌 Please contact Smile Coin Admin to complete payment.</p>
</div>

<footer>
  © 2026 Smile Coin<br>
  Game Top-up Service
</footer>

<script>

let currentGame = "PUBG";

function openGame(game){

  currentGame = game;

  document.getElementById("formBox").style.display = "block";

  if(game === "PUBG"){
    document.getElementById("gameTitle").innerHTML =
      "🎮 PUBG Mobile - UC Top-up";
    document.getElementById("serverId").style.display = "none";
  }

  if(game === "MLBB"){
    document.getElementById("gameTitle").innerHTML =
      "💎 Mobile Legends - Diamonds";
    document.getElementById("serverId").style.display = "block";
  }

  document.getElementById("formBox").scrollIntoView({
    behavior:"smooth"
  });

  calculate();
}

function setCurrency(currency){

  document.getElementById("currency").value = currency;

  document.getElementById("formBox").style.display = "block";

  document.getElementById("formBox").scrollIntoView({
    behavior:"smooth"
  });

  calculate();
}

function calculate(){

  let price = Number(
    document.getElementById("package").value
  );

  let currency =
    document.getElementById("currency").value;

  let finalPrice = price;

  if(currency === "MMK"){
    finalPrice = price * 100;
  }

  document.getElementById("total").innerHTML =
    "Total: " +
    finalPrice.toLocaleString() +
    " " + currency;
}

function placeOrder(){

  let player =
    document.getElementById("playerId").value.trim();

  let server =
    document.getElementById("serverId").value.trim();

  let pack =
    document.getElementById("package").value;

  let currency =
    document.getElementById("currency").value;

  if(player === ""){
    alert("Please enter Player ID / User ID");
    return;
  }

  if(currentGame === "MLBB" && server === ""){
    alert("Please enter Server ID");
    return;
  }

  let price = Number(pack);

  if(currency === "MMK"){
    price = price * 100;
  }

  let orderId =
    "SC" + Date.now().toString().slice(-8);

  let text =
    "Order ID: " + orderId +
    "<br>Game: " + currentGame +
    "<br>Player ID: " + player +
    (currentGame === "MLBB"
      ? "<br>Server ID: " + server
      : "") +
    "<br>Package: " + pack +
    "<br>Total: " +
    price.toLocaleString() +
    " " + currency;

  document.getElementById("orderText").innerHTML = text;

  document.getElementById("orderBox").style.display = "block";

  document.getElementById("orderBox").scrollIntoView({
    behavior:"smooth"
  });
}

</script>

</body>
</html>
