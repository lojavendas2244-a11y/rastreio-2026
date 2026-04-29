
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>CekPack PRO | Rastreamento</title>

<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"/>

<style>
body{
background:#020617;
color:#fff;
font-family:Arial;
text-align:center;
}

.container{
max-width:800px;
margin:auto;
padding:20px;
}

h1{
color:#fbbf24;
}

input{
padding:10px;
width:60%;
border-radius:10px;
border:none;
}

button{
padding:10px 20px;
background:#fbbf24;
border:none;
border-radius:10px;
font-weight:bold;
cursor:pointer;
}

.result{
margin-top:30px;
background:#0f172a;
padding:20px;
border-radius:15px;
display:none;
}

.status{
color:#10b981;
font-weight:bold;
line-height:1.6;
}

#map{
height:300px;
margin-top:20px;
border-radius:15px;
}
</style>
</head>

<body>

<div class="container">

<h1>CekPack PRO 📦</h1>
<p>Rastreie seu pedido em tempo real</p>

<input type="text" id="codigo" placeholder="Digite o código">
<button onclick="rastrear()">Rastrear</button>

<div class="result" id="resultado">
<p><strong>Código:</strong> <span id="cod"></span></p>

<p class="status" id="status"></p>

<div id="map"></div>
</div>

</div>

<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>

let map;

function rastrear(){
let codigo = document.getElementById("codigo").value.trim().toUpperCase();

if(codigo === ""){
alert("Digite um código!");
return;
}

// valida código
if(codigo !== "BR123456789BR"){
alert("Código não encontrado!");
return;
}

// mostra resultado
document.getElementById("resultado").style.display = "block";
document.getElementById("cod").innerText = codigo;

// status atualizado
document.getElementById("status").innerHTML = `
Status: Em trânsito<br>
Recife - PE<br>
Data: 29/04/2026
`;

// remove mapa antigo
if(map){
map.remove();
}

// coordenadas Recife
let lat = -8.0476;
let lng = -34.8770;

// cria mapa
map = L.map('map').setView([lat, lng], 14);

L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);

// marcador
let marker = L.marker([lat, lng]).addTo(map);
marker.bindPopup("📍 Recife - PE").openPopup();
}

</script>

</body>
</html>
