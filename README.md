<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>DXRP Community</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body {
  margin:0;
  font-family: Arial;
  background:#0b0f1a;
  color:white;
  overflow:hidden;
}

.bg {
  position:fixed;
  width:100%;
  height:100%;
  background: radial-gradient(circle at top, #2a0f3a, #05060a);
  animation: move 10s infinite alternate;
  z-index:-1;
}

@keyframes move {
  0% {filter:hue-rotate(0deg);}
  100% {filter:hue-rotate(60deg);}
}

#app {
  display:flex;
  height:100vh;
}

/* SIDEBAR */
#servers {
  width:70px;
  background:#111;
  display:flex;
  flex-direction:column;
  align-items:center;
  padding-top:10px;
}

.server {
  width:45px;
  height:45px;
  background:#222;
  margin:8px;
  border-radius:50%;
  display:flex;
  justify-content:center;
  align-items:center;
  cursor:pointer;
}

/* CHANNELS */
#channels {
  width:200px;
  background:#151821;
  padding:10px;
}

.channel {
  padding:8px;
  margin:5px 0;
  background:#222;
  border-radius:6px;
  cursor:pointer;
}

/* CHAT */
#chat {
  flex:1;
  display:flex;
  flex-direction:column;
}

#messages {
  flex:1;
  overflow:auto;
  padding:10px;
}

.msg {
  background:#1a1f2e;
  margin:5px;
  padding:8px;
  border-radius:8px;
}

/* INPUT */
#inputBar {
  display:flex;
  padding:10px;
  background:#111;
}

input {
  flex:1;
  padding:10px;
  border:none;
  border-radius:6px;
}

button {
  margin-left:5px;
  padding:10px;
  background:#6c2cff;
  color:white;
  border:none;
  border-radius:6px;
  cursor:pointer;
}

/* RIGHT PANEL */
#members {
  width:220px;
  background:#151821;
  padding:10px;
}

.member {
  padding:6px;
  margin:5px 0;
  background:#222;
  border-radius:6px;
}

/* LOGIN */
#login {
  position:fixed;
  width:100%;
  height:100%;
  background:#000000cc;
  display:flex;
  justify-content:center;
  align-items:center;
}

.loginBox {
  background:#111;
  padding:20px;
  border-radius:10px;
  width:300px;
}

.hidden {display:none;}
</style>
</head>

<body>

<div class="bg"></div>

<div id="login">
  <div class="loginBox">
    <h2>DXRP Login</h2>
    <input id="user" placeholder="username"><br><br>
    <input id="pass" type="password" placeholder="password"><br><br>
    <button onclick="login()">Login / Signup</button>
  </div>
</div>

<div id="app" class="hidden">

  <!-- SERVERS -->
  <div id="servers">
    <div class="server" onclick="setChannel('general')">G</div>
    <div class="server" onclick="setChannel('announcements')">A</div>
    <div class="server" onclick="setChannel('dupes')">D</div>
    <div class="server" onclick="setChannel('tickets')">T</div>
  </div>

  <!-- CHANNELS -->
  <div id="channels">
    <h3>Channels</h3>
    <div class="channel" onclick="setChannel('general')"># general</div>
    <div class="channel" onclick="setChannel('announcements')"># announcements</div>
    <div class="channel" onclick="setChannel('dupes')"># dupe-share</div>
    <div class="channel" onclick="setChannel('tickets')"># tickets</div>
  </div>

  <!-- CHAT -->
  <div id="chat">
    <div id="messages"></div>
    <div id="inputBar">
      <input id="msg" placeholder="message...">
      <button onclick="send()">Send</button>
    </div>
  </div>

  <!-- MEMBERS -->
  <div id="members">
    <h3>Online</h3>
    <div id="memberList"></div>
  </div>

</div>

<script>
let currentUser = null;
let channel = "general";

let users = JSON.parse(localStorage.getItem("users")||"{}");
let messages = JSON.parse(localStorage.getItem("msgs")||"{}");

function login(){
  let u = user.value;
  let p = pass.value;

  if(!users[u]){
    users[u] = {pass:p, rank:"User"};
  }

  if(users[u].pass !== p){
    alert("Wrong password");
    return;
  }

  localStorage.setItem("users", JSON.stringify(users));
  currentUser = u;

  login.style.display="none";
  app.classList.remove("hidden");

  renderMembers();
  loadMessages();
}

function setChannel(c){
  channel = c;
  loadMessages();
}

function send(){
  let text = msg.value;
  if(!text) return;

  if(!messages[channel]) messages[channel]=[];

  messages[channel].push({
    user:currentUser,
    text
  });

  localStorage.setItem("msgs", JSON.stringify(messages));
  msg.value="";
  loadMessages();

  // Discord webhook (optional)
  fetch("YOUR_WEBHOOK_URL", {
    method:"POST",
    headers:{"Content-Type":"application/json"},
    body:JSON.stringify({content:`${currentUser}: ${text}`})
  }).catch(()=>{});
}

function loadMessages(){
  messagesDiv.innerHTML="";
  (messages[channel]||[]).forEach(m=>{
    let div=document.createElement("div");
    div.className="msg";
    div.innerHTML="<b>"+m.user+"</b>: "+m.text;
    messagesDiv.appendChild(div);
  });
}

function renderMembers(){
  memberList.innerHTML="";
  Object.keys(users).forEach(u=>{
    let div=document.createElement("div");
    div.className="member";
    div.innerText=u + " ("+users[u].rank+")";
    memberList.appendChild(div);
  });
}
</script>

</body>
</html>
