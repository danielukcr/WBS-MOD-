<!DOCTYPE html>
<html>
<head>
<title>Westbrook Secondary Terminal</title>

<style>
body{
    background:black;
    color:#00ff00;
    font-family:Consolas, monospace;
    padding:20px;
}

#terminal{
    white-space:pre-line;
}

input{
    background:black;
    border:none;
    color:#00ff00;
    font-family:Consolas, monospace;
    outline:none;
    width:300px;
}
</style>
</head>

<body>

<div id="terminal"></div>
<input id="input" autofocus>

<script>

const webhook = "https://discord.com/api/v10/webhooks/1481135662454407189/apMsgafcg7mSROI9vqtDSbrPJV7lAFpaHQ8pZKF6_QjnPiw2hBg45LCdVfmgjyjGl6PI";

let step = 0;

let data = {};

const terminal = document.getElementById("terminal");
const input = document.getElementById("input");

function print(text){
    terminal.innerHTML += text + "\n";
}

print("Westbrook Secondary Moderation System");
print("");
print("Enter your username:");

input.addEventListener("keydown", function(e){

if(e.key === "Enter"){

let value = input.value;
input.value="";

if(step === 0){
data.staff = value;
print("Loading...");
setTimeout(()=>{
print("");
print("Moderation Panel Loaded");
print("");
print("Discord Username:");
},1000);
step=1;
return;
}

if(step === 1){
data.discordUser = value;
print("Discord ID:");
step=2;
return;
}

if(step === 2){
data.discordID = value;
print("Roblox Username:");
step=3;
return;
}

if(step === 3){
data.roblox = value;
print("Type (warning, verbal warning, kick, ban, temporary ban, permanent ban, blacklist):");
step=4;
return;
}

if(step === 4){
data.type = value;

if(value.toLowerCase() === "temporary ban"){
print("When should they be unbanned?");
step=5;
}else{
data.unban="N/A";
print("Reason:");
step=6;
}

return;
}

if(step === 5){
data.unban = value;
print("Reason:");
step=6;
return;
}

if(step === 6){
data.reason = value;

print("");
print("Sending log to Discord...");

let message =
`**Westbrook Secondary Moderation Log**

Staff: ${data.staff}
Discord Username: ${data.discordUser}
Discord ID: ${data.discordID}
Roblox Username: ${data.roblox}
Type: ${data.type}
Unban Date: ${data.unban}
Reason: ${data.reason}`;

fetch(webhook,{
method:"POST",
headers:{"Content-Type":"application/json"},
body:JSON.stringify({content:message})
});

print("Log sent successfully.");

step=7;
}

}

});

</script>

</body>
</html>
