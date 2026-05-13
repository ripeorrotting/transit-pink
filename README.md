<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>CTtransit Ticket Replica</title>
<style>
body{
margin:0;
background:#f3f3f3;
font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
color:#2f3136;
}

.screen{
width:100%;
max-width:828px;
margin:0 auto;
min-height:100vh;
position:relative;
background:#f3f3f3;
}

.close-btn{
position:absolute;
top:40px;
right:34px;
width:64px;
height:64px;
border-radius:50%;
background:#ffffff;
box-shadow:0 2px 10px rgba(0,0,0,.08);
display:flex;
align-items:center;
justify-content:center;
font-size:42px;
color:#4a4a4a;
font-weight:300;
}

.content{
padding:160px 52px 80px;
}

.title{
font-size:58px;
font-weight:700;
letter-spacing:-1px;
margin:0;
line-height:1;
display: flex;
align-items: center;
justify-content: flex-start;
gap: 14px;
}

.subtitle{
font-size:34px;
color:#3d3d3d;
margin-top:4px;
font-weight:400;
text-align: left;
}

.ring-wrap{
display:flex;
justify-content:center;
margin-top:90px;
margin-bottom:80px;
}

.ring{
width:290px;
height:290px;
border-radius:50%;
background:#cf2e83;
display:flex;
align-items:center;
justify-content:center;
box-shadow: inset -8px -12px 0 rgba(0,0,0,.12),
0 0 40px rgba(207, 46, 131, 0.4);
animation: timePulse 1s ease-in-out infinite;
position: relative;
}

.ring::before{
content: '';
position: absolute;
width: 100%;
height: 100%;
border-radius: 50%;
background: linear-gradient(135deg,
rgba(255,255,255,0.3) 0%,
rgba(255,255,255,0) 60%);
opacity: 0.7;
}

.ring-inner{
width:190px;
height:190px;
border-radius:50%;
background:#fff;
display:flex;
align-items:center;
justify-content:center;
box-shadow:0 6px 14px rgba(0,0,0,.18),
inset 0 4px 8px rgba(255,255,255,0.8);
z-index: 2;
transition: transform 0.4s ease-out;
}

@keyframes timePulse {
0% { transform: scale(1); }
45% { transform: scale(1.085); }
100% { transform: scale(1); }
}

.time{
text-align:center;
font-size:105px; /* Reduced from 112px */
font-weight:700;
letter-spacing:-4px;
color:#34373d;
margin-top: 20px;
margin-bottom:46px;
}

.ticket-card{
background:#fff;
border-radius:6px;
box-shadow:0 1px 4px rgba(0,0,0,.18);
padding:34px 38px 40px;
}

.ticket-title{
font-size:38px;
line-height:1.2;
font-weight:400;
margin-bottom:16px;
color:#333;
}

.ticket-desc{
font-size:24px;
line-height:1.45;
color:#666;
}

.expiry{
margin-top:48px;
font-size:30px;
font-weight:700;
color:#444;
line-height:1.3;
}

@media (max-width: 700px){
.content{ padding:110px 26px 50px; }
.title{ font-size:34px; }
.subtitle{ font-size:22px; text-align: left; }
.ring{ width:180px; height:180px; }
.ring-inner{ width:118px; height:118px; font-size:18px; }
.time{
font-size:72px; /* Reduced from 76px */
margin-top: 15px;
}
.ticket-title{ font-size:24px; }
.ticket-desc{ font-size:16px; }
.expiry{ font-size:20px; }
.close-btn{
width:52px; height:52px; font-size:30px;
top:24px; right:20px;
}
}
</style>
</head>
<body>
<div class="screen">
<div class="close-btn">×</div>

<div class="content">
<h1 class="title">CT Transit</h1>
<div class="subtitle">Show operator your ticket</div>

<div class="ring-wrap">
<div class="ring" id="ring">
<div class="ring-inner">
CT Transit
</div>
</div>
</div>

<div class="time" id="clock"></div>

<div class="ticket-card">
<div class="ticket-title">Adult 2 Hour - Local Service</div>
<div class="ticket-desc">
Hartford, New Haven, Stamford, Bristol, Meriden,
New Britain, Wallingford, and Waterbury
</div>
<div class="expiry" id="expiry"></div>
</div>
</div>
</div>

<script>
function updateClock(){
const now = new Date();
const options = {
hour: 'numeric',
minute: '2-digit',
second: '2-digit',
hour12: true
};

document.getElementById('clock').textContent =
now.toLocaleTimeString('en-US', options);
}

function updateExpiry() {
const now = new Date();
const expiryDate = new Date(now);
expiryDate.setHours(23, 59, 59, 999);

const dateOptions = { month: 'long', day: 'numeric', year: 'numeric' };
const timeOptions = { hour: 'numeric', minute: '2-digit', hour12: true };

const formattedDate = expiryDate.toLocaleDateString('en-US', dateOptions);
const formattedTime = expiryDate.toLocaleTimeString('en-US', timeOptions);

document.getElementById('expiry').textContent =
`Expires ${formattedDate} at ${formattedTime}`;
}

// Initialize
updateClock();
updateExpiry();
setInterval(updateClock, 1000);
setInterval(updateExpiry, 60000);
</script>
</body>
</html>
