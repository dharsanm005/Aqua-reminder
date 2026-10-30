<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>AQUA REMINDER – Daily Water Recommender</title>
<style>
:root{--bg:#f3f1ea;--card:#fffdf8;--ink:#1d3540;--mute:#5d7078;--line:#ddd8c9;--water:#2b78a3;--water2:#cfe3ee;--ok:#3d8a62;--warn:#b5792b;--btn:#1d3f57;--btnink:#fff;--field:#fff;
color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#10191e;--card:#17242b;--ink:#e6eef1;--mute:#93a7b0;--line:#2b3c45;--water:#6db6dc;--water2:#24404f;--ok:#6fc596;--warn:#e0a85a;--btn:#6db6dc;--btnink:#0c1a22;--field:#1c2c34;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#10191e;--card:#17242b;--ink:#e6eef1;--mute:#93a7b0;--line:#2b3c45;--water:#6db6dc;--water2:#24404f;--ok:#6fc596;--warn:#e0a85a;--btn:#6db6dc;--btnink:#0c1a22;--field:#1c2c34;color-scheme:dark}
*,*::before,*::after{box-sizing:inherit}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
body{margin:0;background:var(--bg);color:var(--ink);font:16px/1.55 "Segoe UI",system-ui,-apple-system,Roboto,sans-serif}
h1,h2,h3{font-family:Georgia,"Times New Roman",serif;font-weight:600;margin:0;line-height:1.2}
button,input,select{font:inherit;color:inherit}
:focus-visible{outline:3px solid var(--water);outline-offset:2px}
.hidden{display:none!important}
.btn{background:var(--btn);color:var(--btnink);border:0;border-radius:10px;padding:.7rem 1.2rem;cursor:pointer;font-weight:600}
.btn:hover{filter:brightness(1.1)}
.btn.ghost{background:transparent;color:var(--ink);border:1px solid var(--line)}
.btn.ghost:hover{background:var(--water2)}
.card{background:var(--card);border:1px solid var(--line);border-radius:14px;padding:1.4rem}
label{display:block;font-weight:600;font-size:.92rem;margin:.9rem 0 .3rem}
input,select{width:100%;padding:.7rem .8rem;border:1px solid var(--line);border-radius:10px;background:var(--field)}
.err{color:#b3392f;font-size:.9rem;min-height:1.3em;margin:.6rem 0 0}
@media (prefers-color-scheme:dark){.err{color:#f0897f}}

/* login */
#auth{min-height:100vh;display:grid;grid-template-columns:1fr 1fr}
.hero{background:linear-gradient(170deg,#1d4a66,#2b78a3);color:#fff;padding:3rem;display:flex;flex-direction:column;justify-content:center;gap:1.2rem}
.hero h1{font-size:2.6rem}
.hero p{max-width:30ch;font-size:1.1rem;opacity:.92;margin:0}
.hero svg{width:84px;height:84px}
.formwrap{display:flex;align-items:center;justify-content:center;padding:2rem}
.formcard{width:100%;max-width:400px}
.formcard h2{font-size:1.7rem;margin-bottom:.3rem}
.tabs{display:flex;gap:.4rem;margin:1rem 0 .4rem}
.tabs button{flex:1;padding:.55rem;border:1px solid var(--line);background:transparent;border-radius:10px;cursor:pointer;font-weight:600}
.tabs button[aria-selected="true"]{background:var(--btn);color:var(--btnink);border-color:var(--btn)}
.row2{display:grid;grid-template-columns:1fr 1fr;gap:.8rem}
.formcard .btn{width:100%;margin-top:1.2rem}
.note{font-size:.82rem;color:var(--mute);margin-top:1rem}

/* dashboard */
header.top{display:flex;align-items:center;justify-content:space-between;gap:1rem;padding:1rem 1.5rem;background:var(--card);border-bottom:1px solid var(--line);position:sticky;top:env(safe-area-inset-top,0px);z-index:5}
header.top .brand{display:flex;align-items:center;gap:.6rem;font-family:Georgia,serif;font-size:1.25rem;font-weight:600}
header.top .brand svg{width:28px;height:28px}
.hactions{display:flex;gap:.5rem;align-items:center}
.hactions .btn{padding:.45rem .9rem}
main{max-width:1040px;margin:0 auto;padding:1.5rem 1.2rem 3rem}
.greet h1{font-size:1.9rem}
.greet p{color:var(--mute);margin:.2rem 0 1.4rem}
.grid{display:grid;grid-template-columns:1.1fr 1fr;gap:1.2rem}
.ringbox{display:flex;align-items:center;gap:1.6rem;flex-wrap:wrap;justify-content:center}
.ring{position:relative;width:210px;height:210px;flex:none}
.ring svg{width:100%;height:100%;transform:rotate(-90deg)}
.ring .track{stroke:var(--water2)}
.ring .bar{stroke:var(--water);transition:stroke-dashoffset .6s ease}
.ring .mid{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
.ring .mid b{font:600 2.3rem Georgia,serif}
.ring .mid span{color:var(--mute);font-size:.9rem}
.stats{display:grid;gap:.8rem;min-width:150px}
.stat small{color:var(--mute);display:block}
.stat strong{font:600 1.35rem Georgia,serif}
.status{display:inline-block;padding:.25rem .7rem;border-radius:99px;font-size:.85rem;font-weight:600;background:var(--water2)}
.status.ok{color:var(--ok)}.status.warn{color:var(--warn)}
.next{display:flex;gap:1rem;align-items:center}
.next .clock{font:600 2.2rem Georgia,serif;color:var(--water)}
.next p{margin:0;color:var(--mute)}
h2.sec{font-size:1.2rem;margin-bottom:.8rem}
.quick{display:flex;flex-wrap:wrap;gap:.6rem;margin-top:.9rem}
.quick button{flex:1 1 90px;padding:.7rem .4rem;border:1px solid var(--water);background:transparent;color:var(--water);border-radius:10px;cursor:pointer;font-weight:600}
.quick button:hover{background:var(--water);color:var(--btnink)}
.custom{display:flex;gap:.5rem;margin-top:.8rem}
.custom input{flex:1}
.custom .btn{width:auto;margin:0}
.slots{display:grid;grid-template-columns:repeat(auto-fill,minmax(110px,1fr));gap:.6rem}
.slot{border:1px solid var(--line);border-radius:12px;padding:.7rem .5rem;text-align:center;font-size:.88rem}
.slot{display:flex;flex-direction:column;align-items:center;gap:.1rem}
.slot b{display:block;font-size:1.05rem}
.slot .ml{display:block;color:var(--mute);font-size:.85rem}
.slot .ic{display:block;font-size:1.1rem;min-height:1.4rem}
.slot.done{background:var(--water2);border-color:var(--water)}
.slot.next{border:2px solid var(--water)}
.slot.missed{border-style:dashed;color:var(--warn)}
.full{grid-column:1/-1}
.log{list-style:none;margin:0;padding:0;max-height:260px;overflow:auto}
.log li{display:flex;justify-content:space-between;align-items:center;padding:.55rem 0;border-bottom:1px solid var(--line)}
.log button{background:none;border:0;color:var(--mute);cursor:pointer;font-size:1.1rem}
.empty{color:var(--mute);margin:0}
.week{display:flex;align-items:flex-end;gap:.6rem;height:150px;margin-top:.4rem;position:relative}
.week .col{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:flex-end;height:100%;font-size:.8rem;color:var(--mute)}
.week .b{width:100%;max-width:44px;background:var(--water2);border-radius:6px 6px 0 0;min-height:3px}
.week .b.hit{background:var(--water)}
.week .b.today{outline:2px solid var(--water);outline-offset:1px}
dialog{border:1px solid var(--line);border-radius:14px;background:var(--card);color:var(--ink);max-width:380px;width:92%}
dialog::backdrop{background:rgba(0,0,0,.45)}
.toast{position:fixed;left:50%;bottom:calc(1.2rem + env(safe-area-inset-bottom,0px));transform:translateX(-50%);background:var(--btn);color:var(--btnink);padding:.6rem 1.1rem;border-radius:10px;font-weight:600;opacity:0;pointer-events:none;transition:opacity .25s}
.toast.show{opacity:1}
@media (max-width:820px){#auth{grid-template-columns:1fr}.hero{padding:2rem 1.5rem}.hero h1{font-size:2rem}.grid{grid-template-columns:1fr}}
@media (prefers-reduced-motion:reduce){*{transition:none!important}}
</style>
</head>
<body>

<section id="auth">
  <div class="hero">
    <svg viewBox="0 0 64 64" aria-hidden="true"><path d="M32 4C20 20 12 30 12 41a20 20 0 0 0 40 0C52 30 44 20 32 4z" fill="#fff" opacity=".95"/><path d="M22 42a10 10 0 0 0 8 9" stroke="#2b78a3" stroke-width="4" fill="none" stroke-linecap="round"/></svg>
    <h1>Clearwater</h1>
    <p>A simple way to drink the right amount of water, one glass at a time.</p>
  </div>
  <div class="formwrap">
    <div class="formcard card">
      <h2 id="authTitle">Welcome back</h2>
      <div class="tabs" role="tablist">
        <button role="tab" id="tabIn" aria-selected="true">Sign in</button>
        <button role="tab" id="tabUp" aria-selected="false">Create account</button>
      </div>
      <form id="authForm" autocomplete="on" novalidate>
        <div id="nameRow" class="hidden"><label for="fName">Your name</label><input id="fName" autocomplete="name"></div>
        <label for="fEmail">Email</label><input id="fEmail" type="email" autocomplete="email">
        <label for="fPass">Password</label><input id="fPass" type="password" autocomplete="current-password">
        <div id="bodyRows" class="hidden">
          <div class="row2">
            <div><label for="fWeight">Weight (kg)</label><input id="fWeight" type="number" min="25" max="250" value="65"></div>
            <div><label for="fAct">Activity</label>
              <select id="fAct"><option value="0">Light</option><option value="350" selected>Moderate</option><option value="700">Very active</option></select></div>
          </div>
        </div>
        <p class="err" id="authErr" role="alert"></p>
        <button class="btn" type="submit" id="authBtn">Sign in</button>
      </form>
      <p class="note">Demo app: accounts and water logs are saved only in this browser.</p>
    </div>
  </div>
</section>

<section id="app" class="hidden">
  <header class="top">
    <div class="brand"><svg viewBox="0 0 64 64" aria-hidden="true"><path d="M32 4C20 20 12 30 12 41a20 20 0 0 0 40 0C52 30 44 20 32 4z" fill="var(--water)"/></svg>AQUA REMINDER</div>
    <div class="hactions">
      <button class="btn ghost" id="goalBtn">Daily goal</button>
      <button class="btn ghost" id="outBtn">Sign out</button>
    </div>
  </header>
  <main>
    <div class="greet"><h1 id="hello"></h1><p id="dateLine"></p></div>
    <div class="grid">
      <div class="card">
        <h2 class="sec">Today’s progress</h2>
        <div class="ringbox">
          <div class="ring">
            <svg viewBox="0 0 200 200" aria-hidden="true"><circle class="track" cx="100" cy="100" r="84" fill="none" stroke-width="16"/><circle class="bar" id="bar" cx="100" cy="100" r="84" fill="none" stroke-width="16" stroke-linecap="round" stroke-dasharray="527.8" stroke-dashoffset="527.8"/></svg>
            <div class="mid"><b id="pct">0%</b><span>of your goal</span></div>
          </div>
          <div class="stats">
            <div class="stat"><small>Consumed</small><strong id="sCons">0 ml</strong></div>
            <div class="stat"><small>Remaining</small><strong id="sRem">0 ml</strong></div>
            <div class="stat"><small>Daily goal</small><strong id="sGoal">0 ml</strong></div>
            <span class="status" id="status"></span>
          </div>
        </div>
      </div>
      <div class="card">
        <h2 class="sec">Next drink</h2>
        <div class="next">
          <div class="clock" id="nextTime">--:--</div>
          <div><strong id="nextAmt"></strong><p id="nextSub"></p></div>
        </div>
        <h2 class="sec" style="margin-top:1.3rem">Add water</h2>
        <div class="quick" id="quick">
          <button data-ml="150">150 ml</button><button data-ml="250">250 ml</button><button data-ml="350">350 ml</button><button data-ml="500">500 ml</button>
        </div>
        <div class="custom"><input id="customMl" type="number" min="10" max="2000" placeholder="Custom amount (ml)" aria-label="Custom amount in millilitres"><button class="btn" id="customBtn">Add</button></div>
      </div>
      <div class="card full">
        <h2 class="sec">Reminder schedule</h2>
        <div class="slots" id="slots"></div>
      </div>
      <div class="card">
        <h2 class="sec">Today’s log</h2>
        <ul class="log" id="log"></ul>
      </div>
      <div class="card">
        <h2 class="sec">Last 7 days</h2>
        <div class="week" id="week"></div>
      </div>
    </div>
  </main>
</section>

<dialog id="goalDlg">
  <form method="dialog" id="goalForm">
    <h2 style="font-size:1.3rem">Daily goal</h2>
    <p class="note" style="margin-top:.4rem">We recommend about 33 ml per kg of body weight, plus extra for activity.</p>
    <div class="row2">
      <div><label for="gWeight">Weight (kg)</label><input id="gWeight" type="number" min="25" max="250"></div>
      <div><label for="gAct">Activity</label><select id="gAct"><option value="0">Light</option><option value="350">Moderate</option><option value="700">Very active</option></select></div>
    </div>
    <label for="gGoal">Goal (ml)</label><input id="gGoal" type="number" min="800" max="6000" step="50">
    <div class="custom" style="margin-top:1.1rem"><button class="btn ghost" type="button" id="gCancel" style="flex:1">Cancel</button><button class="btn" type="submit" style="flex:1">Save goal</button></div>
  </form>
</dialog>
<div class="toast" id="toast" role="status"></div>

<script>
(function(){
var $=function(id){return document.getElementById(id)};
var mem={};
function load(k,d){try{var v=localStorage.getItem(k);return v?JSON.parse(v):d}catch(e){return k in mem?mem[k]:d}}
function save(k,v){mem[k]=v;try{localStorage.setItem(k,JSON.stringify(v))}catch(e){}}
var users=load("cw_users",{}),email=load("cw_session",null),mode="in";
var SLOTS=[8,10,12,14,16,18,20];

function suggest(w,a){return Math.round((w*33+a)/50)*50}
function dkey(d){var y=d.getFullYear(),m=("0"+(d.getMonth()+1)).slice(-2),x=("0"+d.getDate()).slice(-2);return y+"-"+m+"-"+x}
function logs(){return load("cw_logs_"+email,{})}
function today(){return logs()[dkey(new Date())]||[]}
function sum(a){return a.reduce(function(s,e){return s+e.ml},0)}
function hhmm(t){var d=new Date(t);return ("0"+d.getHours()).slice(-2)+":"+("0"+d.getMinutes()).slice(-2)}
function toast(m){var t=$("toast");t.textContent=m;t.classList.add("show");clearTimeout(toast.h);toast.h=setTimeout(function(){t.classList.remove("show")},1800)}

/* auth */
function setMode(m){
  mode=m;var up=m==="up";
  $("tabIn").setAttribute("aria-selected",!up);$("tabUp").setAttribute("aria-selected",up);
  $("nameRow").classList.toggle("hidden",!up);$("bodyRows").classList.toggle("hidden",!up);
  $("authTitle").textContent=up?"Create your account":"Welcome back";
  $("authBtn").textContent=up?"Create account":"Sign in";
  $("fPass").autocomplete=up?"new-password":"current-password";$("authErr").textContent="";
}
$("tabIn").onclick=function(){setMode("in")};
$("tabUp").onclick=function(){setMode("up")};
$("authForm").onsubmit=function(e){
  e.preventDefault();
  var em=$("fEmail").value.trim().toLowerCase(),pw=$("fPass").value,err=$("authErr");
  if(!/^\S+@\S+\.\S+$/.test(em)){err.textContent="Enter a valid email address.";return}
  if(pw.length<6){err.textContent="Use a password of at least 6 characters.";return}
  if(mode==="up"){
    var nm=$("fName").value.trim(),w=+$("fWeight").value,a=+$("fAct").value;
    if(!nm){err.textContent="Please tell us your name.";return}
    if(!(w>=25&&w<=250)){err.textContent="Enter a weight between 25 and 250 kg.";return}
    if(users[em]){err.textContent="An account with this email already exists. Try signing in.";return}
    users[em]={name:nm,pw:btoa(unescape(encodeURIComponent(pw))),weight:w,act:a,goal:suggest(w,a)};
    save("cw_users",users);
  }else{
    var u=users[em];
    if(!u||u.pw!==btoa(unescape(encodeURIComponent(pw)))){err.textContent="Email or password is incorrect.";return}
  }
  email=em;save("cw_session",em);$("authForm").reset();showApp();
};
$("outBtn").onclick=function(){email=null;save("cw_session",null);setMode("in");showAuth()};
function showAuth(){$("app").classList.add("hidden");$("auth").classList.remove("hidden")}
function showApp(){$("auth").classList.add("hidden");$("app").classList.remove("hidden");render()}

/* actions */
function add(ml){
  if(!(ml>=10&&ml<=2000)){toast("Enter an amount between 10 and 2000 ml.");return}
  var all=logs(),k=dkey(new Date());(all[k]=all[k]||[]).push({t:Date.now(),ml:ml});
  save("cw_logs_"+email,all);render();toast("Added "+ml+" ml");
}
$("quick").onclick=function(e){var b=e.target.closest("button");if(b)add(+b.dataset.ml)};
$("customBtn").onclick=function(){add(+$("customMl").value);$("customMl").value=""};
$("customMl").onkeydown=function(e){if(e.key==="Enter")$("customBtn").click()};
$("log").onclick=function(e){
  var b=e.target.closest("button");if(!b)return;
  var all=logs(),k=dkey(new Date());all[k]=(all[k]||[]).filter(function(x){return x.t!==+b.dataset.t});
  save("cw_logs_"+email,all);render();
};

/* goal dialog */
function fillGoal(){var u=users[email];$("gWeight").value=u.weight;$("gAct").value=u.act;$("gGoal").value=u.goal}
$("goalBtn").onclick=function(){fillGoal();$("goalDlg").showModal()};
$("gCancel").onclick=function(){$("goalDlg").close()};
function recalc(){var w=+$("gWeight").value,a=+$("gAct").value;if(w>=25)$("gGoal").value=suggest(w,a)}
$("gWeight").oninput=recalc;$("gAct").onchange=recalc;
$("goalForm").onsubmit=function(){
  var u=users[email],g=+$("gGoal").value;
  if(!(g>=800&&g<=6000)){toast("Choose a goal between 800 and 6000 ml.");return}
  u.weight=+$("gWeight").value;u.act=+$("gAct").value;u.goal=g;save("cw_users",users);render();toast("Goal updated");
};

/* render */
function render(){
  if(!email||!users[email])return;
  var u=users[email],now=new Date(),t=today(),cons=sum(t),goal=u.goal;
  var p=Math.min(100,Math.round(cons/goal*100)),rem=Math.max(0,goal-cons);
  var h=now.getHours();
  $("hello").textContent=(h<12?"Good morning, ":h<18?"Good afternoon, ":"Good evening, ")+u.name.split(" ")[0];
  $("dateLine").textContent=now.toLocaleDateString(undefined,{weekday:"long",day:"numeric",month:"long"});
  $("bar").style.strokeDashoffset=527.8*(1-p/100);
  $("pct").textContent=p+"%";
  $("sCons").textContent=cons+" ml";$("sRem").textContent=rem+" ml";$("sGoal").textContent=goal+" ml";

  /* schedule */
  var per=Math.round(goal/SLOTS.length/10)*10,nextIdx=-1,expected=0;
  var html=SLOTS.map(function(hr,i){
    var target=goal*(i+1)/SLOTS.length,done=cons>=target-1,past=h>=hr;
    if(past)expected=target;
    var cls="slot",icon="💧";
    if(done){cls+=" done";icon="✓"}
    else if(nextIdx<0){nextIdx=i;cls+=" next";icon="⏰"}
    else icon="○";
    if(!done&&past&&i!==nextIdx){cls+=" missed";icon="!"}
    return '<div class="'+cls+'"><span class="ic">'+icon+'</span><b>'+("0"+hr).slice(-2)+':00</b><span class="ml">'+per+' ml</span></div>';
  }).join("");
  $("slots").innerHTML=html;
  var st=$("status");
  if(cons>=goal){st.textContent="Goal reached";st.className="status ok"}
  else if(cons+per*0.5>=expected){st.textContent="On track";st.className="status ok"}
  else{st.textContent="Behind by "+Math.round(expected-cons)+" ml";st.className="status warn"}

  /* next drink */
  if(cons>=goal){$("nextTime").textContent="Done";$("nextAmt").textContent="You reached today’s goal.";$("nextSub").textContent="Sip as you need until bedtime.";}
  else{
    var hr2=SLOTS[nextIdx<0?0:nextIdx],slotMs=new Date(now.getFullYear(),now.getMonth(),now.getDate(),hr2).getTime(),diff=slotMs-now.getTime();
    var amt=Math.min(rem,Math.max(per,Math.round((goal*(nextIdx+1)/SLOTS.length-cons)/10)*10));
    $("nextAmt").textContent="Drink about "+amt+" ml";
    if(diff<=0){$("nextTime").textContent="Now";$("nextSub").textContent="Your "+("0"+hr2).slice(-2)+":00 drink is due.";}
    else{var m=Math.round(diff/60000);$("nextTime").textContent=("0"+hr2).slice(-2)+":00";$("nextSub").textContent="In "+(m>=60?Math.floor(m/60)+" h "+(m%60)+" min":m+" min");}
  }

  /* log */
  var L=$("log");
  if(!t.length)L.innerHTML='<li><p class="empty">Nothing logged yet. Tap an amount above to add your first glass.</p></li>';
  else L.innerHTML=t.slice().reverse().map(function(e){return '<li><span>'+hhmm(e.t)+' &nbsp; <b>'+e.ml+' ml</b></span><button data-t="'+e.t+'" aria-label="Remove '+e.ml+' ml entry">✕</button></li>'}).join("");

  /* week */
  var all=logs(),cols=[],max=goal;
  for(var i=6;i>=0;i--){var d=new Date();d.setDate(d.getDate()-i);var v=sum(all[dkey(d)]||[]);max=Math.max(max,v);cols.push({d:d,v:v,td:i===0})}
  $("week").innerHTML=cols.map(function(c){
    return '<div class="col"><span>'+(c.v?(c.v/1000).toFixed(1)+"L":"")+'</span><div class="b'+(c.v>=goal?" hit":"")+(c.td?" today":"")+'" style="height:'+Math.round(c.v/max*100*0.78)+'%"></div><span>'+c.d.toLocaleDateString(undefined,{weekday:"short"})+'</span></div>';
  }).join("");
}
setInterval(function(){if(email&&users[email]&&!$("app").classList.contains("hidden"))render()},60000);

if(email&&users[email])showApp();else showAuth();
})();
</script>
</body>
</html>
