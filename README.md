<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Max Garden – Jardinería Premium</title>
<link rel="icon" href="logo-max-garden.png">
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital@0;1&display=swap" rel="stylesheet">
<style>
:root{
  --verde:#3f6f4e; --verde-claro:#5fa87a; --dorado:#c9a24d;
  --osc:#0d1a14; --cla:#f4f7f5; --card-osc:#13261d; --card-cla:#ffffff;
  --texto-osc:#ecf0ec; --texto-cla:#1e2b24;
}
body{margin:0;font-family:'Playfair Display',serif;font-style:italic;transition:.5s;overflow-x:hidden;}
body.claro{background:var(--cla);color:var(--texto-cla);}
body.oscuro{background:radial-gradient(circle at top,#13261d,#08120d);color:var(--texto-osc);}
header{position:relative;text-align:center;padding:100px 20px;background:linear-gradient(rgba(0,0,0,0.4), rgba(0,0,0,0.4)), url('https://images.unsplash.com/photo-1560250097-0b93528c311a?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=1080') center/cover no-repeat;color:#fff;overflow:hidden;}
header h1{font-size:4rem;margin:20px 0;}
header span{color:var(--dorado);}
header p{opacity:.9;font-size:1.4rem;margin-bottom:50px;}
header .logo{width:220px;animation:logoAnim 5s ease-in-out infinite;}
@keyframes logoAnim{0%{transform:rotate(0);}25%{transform:rotate(2deg);}50%{transform:rotate(0);}75%{transform:rotate(-2deg);}100%{transform:rotate(0);}}
.leaf{position:absolute;width:60px;animation:leafAnim linear infinite;}
@keyframes leafAnim{0%{transform:translateY(0) rotate(0deg);}100%{transform:translateY(900px) rotate(360deg);}}
section{max-width:1400px;margin:auto;padding:60px 20px;display:grid;grid-template-columns:1fr 1fr;gap:50px;}
@media(max-width:1100px){section{grid-template-columns:1fr}}
.card{background:var(--card-osc);padding:40px;border-radius:30px;box-shadow:0 20px 50px rgba(0,0,0,.6);transition:.5s;}
body.claro .card{background:var(--card-cla);}
input,textarea,select,button{width:100%;padding:16px;margin:12px 0;border:none;border-radius:18px;font-size:1rem;}
button{background:var(--verde-claro);cursor:pointer;transition:.4s;font-weight:bold;}
button:hover{background:var(--dorado);}
.grass{position:fixed;bottom:0;width:100%;height:150px;background:linear-gradient(var(--verde),#1b3a2a);z-index:-1;}
.toggle{position:fixed;top:20px;right:20px;background:var(--dorado);color:#000;border:none;padding:12px 18px;border-radius:25px;cursor:pointer;font-size:1rem;z-index:100;}
.galeria{display:flex;overflow-x:auto;gap:20px;padding:20px 0;animation:scrollGallery 50s linear infinite;}
@keyframes scrollGallery{0%{transform:translateX(0);}100%{transform:translateX(-30%);}}
.galeria img{width:280px;height:180px;object-fit:cover;border-radius:25px;transition:.5s;}
.galeria img:hover{transform:scale(1.15);}
.chat{height:350px;display:flex;flex-direction:column;margin-top:15px;}
.chat-box{flex:1;overflow-y:auto;padding:12px;border-radius:18px;background:rgba(0,0,0,.12);}
.msg{margin:10px 0;padding:12px;border-radius:18px;max-width:85%;line-height:1.4;}
.ia{background:#1e3a2c;color:#fff;}
.user{background:var(--verde-claro);color:#000;margin-left:auto;}
h2{border-bottom:3px solid var(--dorado);padding-bottom:10px;margin-bottom:25px;}
hr{border:0;height:3px;background:var(--dorado);margin:50px 0;}
ul{list-style:none;padding-left:0;}
li{margin:10px 0;padding-left:15px;position:relative;}
li::before{content:"🌿";position:absolute;left:0;}
</style>
</head>
<body class="oscuro">
<div class="grass"></div>
<button class="toggle" onclick="toggleModo()">☀ / 🌙</button>

<header>
<img src="logo-max-garden.png" class="logo" alt="Max Garden">
<h1><span>Max</span> Garden</h1>
<p>Jardinería premium, corte de pasto y mantenimiento integral personalizado</p>
<img src="https://images.unsplash.com/photo-1591088390270-5e8724cb18e3?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=60" class="leaf" style="left:5%;animation-duration:12s;">
<img src="https://images.unsplash.com/photo-1591088390270-5e8724cb18e3?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=60" class="leaf" style="left:45%;animation-duration:16s;">
<img src="https://images.unsplash.com/photo-1591088390270-5e8724cb18e3?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&w=60" class="leaf" style="left:85%;animation-duration:10s;">
</header>

<section>
<div class="card">
<h2>📋 Solicitar servicio</h2>
<input id="nombre" placeholder="Nombre completo">
<input id="direccion" placeholder="Dirección">
<input id="telefono" type="tel" placeholder="Teléfono" required>
<textarea id="detalle" placeholder="Contanos sobre tu jardín"></textarea>
<label>💳 Método de pago</label>
<select id="pago">
<option>Mercado Pago</option>
<option>Transferencia</option>
</select>
<button onclick="enviarSolicitud()">Continuar al pago</button>
<p id="estado"></p>
</div>

<div class="card">
<h2>📅 Horarios confirmados</h2>
<ul id="horariosReservados"></ul>
</div>

<div class="card">
<h2>🖼 Galería de trabajos</h2>
<div class="galeria" id="galeria"></div>
</div>

<div class="card" id="seccionAnuncios">
<h2>📢 Anuncios recientes</h2>
<ul id="listaAnuncios"></ul>
</div>

<div class="card" id="panelMaxi">
<h2>🔐 Panel Maxi Garden</h2>
<button onclick="loginPanel()">Ingresar panel</button>
<div id="panelPrivado" style="display:none;">
<h3>Solicitudes de clientes</h3>
<ul id="solicitudesList"></ul>
<input id="nuevoHorario" placeholder="Agregar horario (ej: 15:30-16:30)">
<button onclick="agregarHorario()">Agregar horario</button>

<h3>Galería de trabajos</h3>
<input type="file" id="subirImg" multiple accept="image/*">
<button onclick="agregarImagenes()">Subir imágenes</button>

<h3>📢 Anuncios y novedades</h3>
<textarea id="nuevoAnuncio" placeholder="Escribí tu anuncio aquí"></textarea>
<button onclick="publicarAnuncio()">Publicar anuncio</button>
</div>
</div>

<div class="card">
<h2>🤖 Chat IA GPT-4</h2>
<div class="chat">
<div class="chat-box" id="chat"></div>
<input id="chatInput" placeholder="Consultá por clima, reservas, servicios..." onkeydown="if(event.key==='Enter')chatSend()">
</div>
</div>

<hr>

<section style="grid-template-columns:1fr">
<div class="card">
<h2>🌿 Servicios destacados</h2>
<ul>
<li>Corte de pasto profesional</li>
<li>Poda de árboles y arbustos</li>
<li>Mantenimiento integral de jardines</li>
<li>Asesoría personalizada</li>
<li>Control de plagas y fertilización</li>
</ul>
</div>
<div class="card">
<h2>📍 Contacto</h2>
<p>Teléfono: 2236701789</p>
<p>Ubicación: mar del plata</p>
</div>
</section>

<script>
// Modo oscuro/claro
function toggleModo(){document.body.classList.toggle("oscuro");document.body.classList.toggle("claro");}

// Variables globales
let horarios=[]; let solicitudes=[]; let galeriaImgs=[]; let anuncios=[]; let panelPass="MxG@2026Secure!";

// Panel
function loginPanel(){const pass=prompt("Contraseña panel Maxi:");if(pass===panelPass){document.getElementById("panelPrivado").style.display="block";}else{alert("Contraseña incorrecta");}}

// Funciones IA GPT-4
const chatBox=document.getElementById("chat");
function addMessage(text,sender){const msg=document.createElement("div");msg.className="msg "+sender;msg.textContent=text;chatBox.appendChild(msg);chatBox.scrollTop=chatBox.scrollHeight;}
addMessage("Hola 🌱 Soy la IA GPT-4 de Max Garden. Puedo ayudarte con clima, horarios, servicios y reservas.","ia");

async function chatSend(){
  const input = document.getElementById("chatInput");
  if(!input.value) return;
  addMessage(input.value,"user");
  const userText = input.value;
  input.value = "";

  try {
    const response = await fetch("https://api.openai.com/v1/chat/completions", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        "Authorization": "Bearer TU_API_KEY_AQUI"
      },
      body: JSON.stringify({
        model: "gpt-4",
        messages: [
          {role: "system", content: "Eres la IA de Max Garden, experta en jardinería, reservas, clima y servicios. Responde de manera clara, profesional y amigable."},
          {role: "user", content: userText}
        ],
        max_tokens: 250
      })
    });
    const data = await response.json();
    const reply = data.choices[0].message.content;
    addMessage(reply, "ia");
  } catch (err) {
    addMessage("Lo siento, no puedo responder ahora. Intentá más tarde.", "ia");
  }
}

// Reservas
function enviarSolicitud(){
  const nombre=document.getElementById("nombre").value;
  const direccion=document.getElementById("direccion").value;
  const telefono=document.getElementById("telefono").value;
  const detalle=document.getElementById("detalle").value;
  const pago=document.getElementById("pago").value;
  if(!nombre||!direccion||!telefono){alert("Completá todos los campos");return;}
  solicitudes.push({nombre,direccion,telefono,detalle,pago,dia:null});
  document.getElementById("estado").innerText="Solicitud enviada. Maxi la confirmará y asignará horario.";
}

// Panel Maxi
function agregarHorario(){const h=document.getElementById("nuevoHorario").value;if(h){horarios.push(h);document.getElementById("horariosReservados").innerHTML=horarios.map(h=>`<li>${h}</li>`).join("");document.getElementById("nuevoHorario").value="";}}
function publicarAnuncio(){const a=document.getElementById("nuevoAnuncio").value;if(a){anuncios.push(a);document.getElementById("listaAnuncios").innerHTML=anuncios.map(a=>`<li>${a}</li>`).join("");document.getElementById("nuevoAnuncio").value="";}}
function agregarImagenes(){const input=document.getElementById("subirImg");Array.from(input.files).forEach(f=>{const url=URL.createObjectURL(f);galeriaImgs.push(url);document.getElementById("galeria").innerHTML+=`<img src="${url}" alt="Trabajo jardin">`;});}
</script>
</body>
</html>
