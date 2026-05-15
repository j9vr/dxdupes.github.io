<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>DXRP Dupes</title>

<style>

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
    font-family:Arial, Helvetica, sans-serif;
}

body{
    background:#0b0b10;
    color:white;
    overflow-x:hidden;
}

/* TOP BAR */

.topbar{
    width:100%;
    background:#151515;
    border-bottom:2px solid #7b2cff;
    padding:12px;
    position:fixed;
    top:0;
    z-index:999;
    display:flex;
    justify-content:center;
    align-items:center;
}

.url-box{
    width:75%;
    background:#0d0d0d;
    border:1px solid #7b2cff;
    border-radius:12px;
    padding:10px 15px;
    color:#b266ff;
    display:flex;
    align-items:center;
    gap:10px;
    box-shadow:0 0 20px rgba(123,44,255,0.3);
}

.lock{
    color:#00ff88;
}

/* SIDEBAR */

.sidebar{
    width:240px;
    height:100vh;
    position:fixed;
    top:58px;
    left:0;
    background:#120018;
    border-right:2px solid #7b2cff;
    padding:20px;
}

.logo{
    text-align:center;
    font-size:32px;
    font-weight:bold;
    color:#b266ff;
    margin-bottom:30px;
}

.nav{
    display:flex;
    flex-direction:column;
    gap:15px;
}

.nav button{
    background:#1f1f1f;
    border:none;
    color:white;
    padding:15px;
    border-radius:10px;
    cursor:pointer;
    transition:0.2s;
    font-size:15px;
}

.nav button:hover{
    background:#7b2cff;
    transform:translateX(5px);
}

/* MAIN */

.main{
    margin-left:240px;
    margin-top:70px;
    padding:30px;
}

.title{
    font-size:40px;
    color:#b266ff;
    margin-bottom:25px;
}

/* STATS */

.stats{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
    gap:20px;
    margin-bottom:30px;
}

.card{
    background:#151515;
    border:1px solid #7b2cff;
    border-radius:15px;
    padding:20px;
    box-shadow:0 0 20px rgba(123,44,255,0.15);
}

.card h2{
    color:#b266ff;
    margin-bottom:10px;
}

.card p{
    font-size:28px;
    font-weight:bold;
}

.online{
    color:#00ff88;
}

/* LOGS */

.logs{
    background:#141414;
    border:1px solid #7b2cff;
    border-radius:15px;
    padding:25px;
}

.logs-top{
    display:flex;
    justify-content:space-between;
    align-items:center;
    flex-wrap:wrap;
    gap:15px;
    margin-bottom:20px;
}

.search{
    background:#0d0d0d;
    border:1px solid #7b2cff;
    padding:12px;
    border-radius:10px;
    color:white;
    width:250px;
    outline:none;
}

.generate-btn{
    background:#7b2cff;
    border:none;
    color:white;
    padding:12px 20px;
    border-radius:10px;
    cursor:pointer;
    margin-left:10px;
    transition:0.2s;
}

.generate-btn:hover{
    background:#9f66ff;
}

.log{
    background:#1b1b1b;
    border-left:5px solid #7b2cff;
    border-radius:10px;
    padding:18px;
    margin-bottom:15px;
    animation:fade 0.3s ease;
}

.log span{
    color:#b266ff;
    font-weight:bold;
}

/* FOOTER */

.footer{
    margin-top:30px;
    text-align:center;
    color:#666;
}

@keyframes fade{
    from{
        opacity:0;
        transform:translateY(10px);
    }

    to{
        opacity:1;
        transform:translateY(0);
    }
}

/* MOBILE */

@media(max-width:800px){

    .sidebar{
        display:none;
    }

    .main{
        margin-left:0;
    }

    .url-box{
        width:95%;
    }

}

</style>
</head>
<body>

<!-- TOP URL BAR -->

<div class="topbar">

    <div class="url-box">
        <span class="lock">🔒</span>

        <span id="githubUrl">
            https://YOURNAME.github.io/dxrpdupes
        </span>
    </div>

</div>

<!-- SIDEBAR -->

<div class="sidebar">

    <div class="logo">
        DXRP
    </div>

    <div class="nav">
        <button>Dashboard</button>
        <button>Dupe Logs</button>
        <button>Players</button>
        <button>Bans</button>
        <button>Settings</button>
    </div>

</div>

<!-- MAIN -->

<div class="main">

    <h1 class="title">
        DXRP Dupe Detection
    </h1>

    <!-- STATS -->

    <div class="stats">

        <div class="card">
            <h2>Total Dupes</h2>
            <p id="dupeCount">14</p>
        </div>

        <div class="card">
            <h2>Players Flagged</h2>
            <p>8</p>
        </div>

        <div class="card">
            <h2>Server Status</h2>
            <p class="online">ONLINE</p>
        </div>

    </div>

    <!-- LOGS -->

    <div class="logs">

        <div class="logs-top">

            <h2>Recent Logs</h2>

            <div>

                <input
                    type="text"
                    class="search"
                    placeholder="Search logs..."
                    onkeyup="searchLogs(this.value)"
                >

                <button
                    class="generate-btn"
                    onclick="generateLog()"
                >
                    Generate Log
                </button>

            </div>

        </div>

        <div id="logsContainer">

            <div class="log">
                <p><span>Player:</span> Justin</p>
                <p><span>SteamID:</span> STEAM_0:1:78213</p>
                <p><span>Item:</span> Money Printer</p>
                <p><span>Amount:</span> x12</p>
                <p><span>Time:</span> 22:41</p>
            </div>

            <div class="log">
                <p><span>Player:</span> Alpha</p>
                <p><span>SteamID:</span> STEAM_0:1:99812</p>
                <p><span>Item:</span> Meth Lab</p>
                <p><span>Amount:</span> x5</p>
                <p><span>Time:</span> 22:44</p>
            </div>

            <div class="log">
                <p><span>Player:</span> Shadow</p>
                <p><span>SteamID:</span> STEAM_0:1:22291</p>
                <p><span>Item:</span> Weapon Shipment</p>
                <p><span>Amount:</span> x9</p>
                <p><span>Time:</span> 22:47</p>
            </div>

        </div>

    </div>

    <div class="footer">
        Hosted with GitHub Pages
    </div>

</div>

<script>

/* PLAYERS */

const players = [
    "Justin",
    "Alpha",
    "Shadow",
    "Nova",
    "Ghost",
    "Blaze",
    "Venom",
    "Vortex"
];

/* ITEMS */

const items = [
    "Money Printer",
    "Meth Lab",
    "Weapon Shipment",
    "Ammo Box",
    "Diamond Crate",
    "AK47 Crate",
    "Vault Cash"
];

/* RANDOM */

function random(arr){
    return arr[Math.floor(Math.random() * arr.length)];
}

/* GENERATE LOG */

function generateLog(){

    const player = random(players);

    const item = random(items);

    const amount =
        Math.floor(Math.random() * 15) + 1;

    const steamid =
        "STEAM_0:1:" +
        Math.floor(Math.random() * 99999);

    const now = new Date();

    const time =
        now.getHours() + ":" +
        String(now.getMinutes()).padStart(2,"0");

    const log =
        document.createElement("div");

    log.className = "log";

    log.innerHTML = `
        <p><span>Player:</span> ${player}</p>
        <p><span>SteamID:</span> ${steamid}</p>
        <p><span>Item:</span> ${item}</p>
        <p><span>Amount:</span> x${amount}</p>
        <p><span>Time:</span> ${time}</p>
    `;

    document
        .getElementById("logsContainer")
        .prepend(log);

    const count =
        document.getElementById("dupeCount");

    count.innerText =
        parseInt(count.innerText) + 1;
}

/* SEARCH */

function searchLogs(value){

    const logs =
        document.querySelectorAll(".log");

    logs.forEach(log => {

        if(
            log.innerText
            .toLowerCase()
            .includes(value.toLowerCase())
        ){
            log.style.display = "block";
        }
        else{
            log.style.display = "none";
        }

    });

}

/* AUTO URL */

const githubName = "YOURNAME";

document.getElementById("githubUrl")
.innerText =
`https://${githubName}.github.io/dxrpdupes`;

</script>

</body>
</html>
