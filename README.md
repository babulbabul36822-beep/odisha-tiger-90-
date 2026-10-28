
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>ODISHA TIGER 90 Tournament</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#090c13;color:#fff;font-family:Arial}
header{text-align:center;padding:25px 10px;background:linear-gradient(135deg,#ff7900,#a31600,#111)}
header h1{color:#ffd064;font-size:28px}
main{max-width:700px;margin:auto;padding:14px}
.card{background:#191f2c;border:1px solid #75451e;border-radius:13px;padding:17px;margin:15px 0}
h2{color:#ffc04a}
input,button{width:100%;padding:12px;margin:7px 0;border-radius:7px;font-size:15px}
input{background:#0c111b;color:white;border:1px solid #555}
button{background:#ff6500;color:white;border:0;font-weight:bold}
.secondary{background:#394253}
table{width:100%;border-collapse:collapse}
td,th{padding:9px 4px;border-bottom:1px solid #444;text-align:left;overflow-wrap:anywhere}
.small{font-size:12px;color:#c7cbd4}
</style>
</head>
<body>
<header>
<h1>🐯 ODISHA TIGER 90</h1>
<p>🔥 FREE FIRE TOURNAMENT 🔥</p>
<strong>PLAY LIKE A TIGER!</strong>
</header>
<main>

<section class="card">
<h2>🏆 Tournament Schedule</h2>
<label>Match Date</label>
<input id="date" type="date">
<label>Match Time</label>
<input id="time" type="time">
<p id="schedule">Match schedule coming soon!</p>
</section>

<section class="card">
<h2>📝 Player Registration</h2>
<form id="register">
<input id="team" placeholder="Team Name" required>
<input id="player" placeholder="Player Name" required>
<input id="uid" placeholder="Free Fire UID" inputmode="numeric"
 pattern="[0-9]{5,20}" required>
<input id="captain" placeholder="Captain Name" required>
<button type="submit">REGISTER NOW 🔥</button>
</form>
<p class="small">Demo registrations are saved only in this browser.</p>
</section>

<section class="card">
<h2>🔐 Room Details</h2>
<p>Room ID: <strong id="room">Not announced</strong></p>
<p>Room Password: <strong id="password">Not announced</strong></p>
</section>

<section class="card">
<h2>📋 Registered Players</h2>
<div id="players">No registrations yet.</div>
</section>

<section class="card">
<h2>🥇 Winner List</h2>
<div id="winners">Winner not announced yet.</div>
</section>

<section class="card">
<h2>👑 Admin Panel</h2>
<p class="small">Demo PIN: 9090. Do not use this PIN for a public website.</p>
<input id="pin" type="password" placeholder="Admin PIN">
<button id="login">ADMIN LOGIN</button>
<div id="admin" hidden>
<hr>
<h3>Update Room</h3>
<input id="newRoom" placeholder="Room ID">
<input id="newPassword" placeholder="Room Password">
<button id="saveRoom">SAVE ROOM DETAILS</button>
<h3>Declare Winner</h3>
<input id="winnerName" placeholder="Winning Team Name">
<button id="saveWinner">PUBLISH WINNER</button>
<button id="clearPlayers" class="secondary">CLEAR ALL DEMO PLAYERS</button>
</div>
<p id="status" class="small"></p>
</section>
</main>

<script>
const $ = id => document.getElementById(id);
const KEY = "tiger90_demo_players";
let players = [];
try { players = JSON.parse(localStorage.getItem(KEY) || "[]"); }
catch { players = []; }

function renderPlayers(){
 if(!players.length){$("players").textContent="No registrations yet.";return;}
 const table=document.createElement("table");
 table.innerHTML="<tr><th>Team</th><th>Player</th><th>UID</th></tr>";
 players.forEach(p=>{
  const tr=document.createElement("tr");
  [p.team,p.player,p.uid].forEach(value=>{
   const td=document.createElement("td");
   td.textContent=value;
   tr.appendChild(td);
  });
  table.appendChild(tr);
 });
 $("players").replaceChildren(table);
}
renderPlayers();

$("register").addEventListener("submit",e=>{
 e.preventDefault();
 const p={
  team:$("team").value.trim(),
  player:$("player").value.trim(),
  uid:$("uid").value.trim(),
  captain:$("captain").value.trim()
 };
 if(players.some(x=>x.uid===p.uid)){
  alert("This UID is already registered in this browser.");
  return;
 }
 players.push(p);
 localStorage.setItem(KEY,JSON.stringify(players));
 renderPlayers();
 $("status").textContent="Demo registration saved on this device.";
 e.target.reset();
});

function updateSchedule(){
 const d=$("date").value,t=$("time").value;
 $("schedule").textContent=d ? d+(t?" at "+t:"") : "Match schedule coming soon!";
}
$("date").addEventListener("change",updateSchedule);
$("time").addEventListener("change",updateSchedule);

$("login").addEventListener("click",()=>{
 if($("pin").value==="9090"){
  $("admin").hidden=false;
  $("status").textContent="Demo admin panel opened.";
 } else {
  $("status").textContent="Incorrect PIN.";
 }
});

$("saveRoom").addEventListener("click",()=>{
 $("room").textContent=$("newRoom").value.trim()||"Not announced";
 $("password").textContent=$("newPassword").value.trim()||"Not announced";
 $("status").textContent="Room details updated in this page.";
});

$("saveWinner").addEventListener("click",()=>{
 const name=$("winnerName").value.trim();
 if(!name){alert("Enter the winning team name.");return;}
 $("winners").textContent="🏆 Champion: "+name;
 $("status").textContent="Winner shown on this page.";
});

$("clearPlayers").addEventListener("click",()=>{
 if(!confirm("Delete all demo registrations from this browser?"))return;
 players=[];
 localStorage.removeItem(KEY);
 renderPlayers();
 $("status").textContent="Demo registrations cleared.";
});
</script>
</body>
</html>
