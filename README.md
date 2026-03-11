<!DOCTYPE html>
<html>
<head>
<title>Westbrook Secondary Moderation Logger</title>
<style>
body{
    background:#0f172a;
    font-family:monospace;
    color:white;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
}
.panel{
    background:#1e293b;
    padding:25px;
    border-radius:10px;
    width:400px;
}
input,select,button{
    width:100%;
    margin-top:8px;
    padding:8px;
    border:none;
    border-radius:5px;
}
button{
    background:#2563eb;
    color:white;
    cursor:pointer;
}
button:hover{
    background:#1d4ed8;
}
</style>
</head>

<body>

<div class="panel">

<h2>Westbrook Secondary</h2>

<label>Staff Username</label>
<input id="staff">

<label>Discord Username</label>
<input id="duser">

<label>Discord ID</label>
<input id="did">

<label>Roblox Username</label>
<input id="ruser">

<label>Type</label>
<select id="type" onchange="checkBan()">
<option>warning</option>
<option>verbal warning</option>
<option>kick</option>
<option>ban</option>
<option>temporary ban</option>
<option>permanent ban</option>
<option>blacklist</option>
</select>

<div id="tempBanBox" style="display:none;">
<label>Unban Date</label>
<input id="unban">
</div>

<label>Reason</label>
<input id="reason">

<br><br>
<button onclick="sendLog()">Send Log</button>

</div>

<script>

function checkBan(){
    let type = document.getElementById("type").value;
    let box = document.getElementById("tempBanBox");

    if(type === "temporary ban"){
        box.style.display="block";
    }else{
        box.style.display="none";
    }
}

function sendLog(){

const webhook = "PASTE_WEBHOOK_HERE";

let staff = document.getElementById("staff").value;
let duser = document.getElementById("duser").value;
let did = document.getElementById("did").value;
let ruser = document.getElementById("ruser").value;
let type = document.getElementById("type").value;
let reason = document.getElementById("reason").value;
let unban = document.getElementById("unban").value || "N/A";

let message =
`**Westbrook Secondary Moderation Log**

Staff: ${staff}
Discord Username: ${duser}
Discord ID: ${did}
Roblox Username: ${ruser}
Type: ${type}
Unban Date: ${unban}
Reason: ${reason}`;

fetch(webhook,{
method:"POST",
headers:{
"Content-Type":"application/json"
},
body:JSON.stringify({
content: message
})
});

alert("Log sent to Discord!");

}

</script>

</body>
</html>
