game_code = """<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>SCI-FI Quiz Brawl</title>
  <style>
    body{
      margin:0;
      font-family: sans-serif;
      background:#0b1020;
      color:#e8f3ff;
      min-height:100vh;
      display:flex;
      justify-content:center;
      align-items:center;
    }
    .container{
      max-width:900px;
      width:95%;
      background:#121a35;
      border:2px solid #66e0ff55;
      border-radius:16px;
      padding:20px;
    }
    h1{margin-top:0;color:#66e0ff;}
    .btn{
      display:inline-block;
      background:#0a1430;
      color:#e8f3ff;
      border:1px solid #66e0ff99;
      padding:10px 14px;
      border-radius:10px;
      cursor:pointer;
      margin:4px 0;
    }
    .btn:hover{background:#13244c;}
    .char{
      border:1px solid #66e0ff55;
      border-radius:12px;
      padding:10px;
      margin:8px 0;
      cursor:pointer;
    }
    .char:hover{background:#1c2850;}
    .bar{height:12px;border:1px solid #fff2;border-radius:8px;overflow:hidden;margin:4px 0;}
    .hp{background:linear-gradient(90deg,#39ffb3,#9af5a2);}
    .en{background:linear-gradient(90deg,#66e0ff,#7ecbff);}
  </style>
</head>
<body>
  <div class="container">
    <h1>⚡ SCI-FI Quiz Brawl</h1>
    <div id="screenSelect">
      <p>Pilih karakter:</p>
      <div class="char" onclick="pickChar('🤖','CYBR-01',{hp:120,atk:12,def:4,en:100})">🤖 CYBR-01 (Cyborg) • HP 120 • ATK 12 • DEF 4</div>
      <div class="char" onclick="pickChar('👨‍🚀','ZENT-9',{hp:100,atk:14,def:3,en:100})">👨‍🚀 ZENT-9 (Space Marine) • HP 100 • ATK 14 • DEF 3</div>
      <div class="char" onclick="pickChar('🛰️','DRN-Ω',{hp:90,atk:10,def:2,en:120})">🛰️ DRN-Ω (Drone AI) • HP 90 • ATK 10 • DEF 2</div>
    </div>

    <div id="screenBattle" style="display:none;">
      <div>
        <h3 id="pName"></h3>
        <div class="bar"><div id="pHP" class="hp" style="width:100%"></div></div>
        <small id="pHPText"></small>
      </div>
      <hr>
      <div>
        <h3 id="eName"></h3>
        <div class="bar"><div id="eHP" class="hp" style="width:100%"></div></div>
        <small id="eHPText"></small>
      </div>
      <hr>
      <div id="questionBox"></div>
      <div id="answers"></div>
    </div>
  </div>

<script>
let player={}, enemy={}, deck=[];
const questions=[
  {q:"Planet ke-4 dari Matahari?",a:["Bumi","Venus","Mars","Jupiter"],c:2},
  {q:"Biner dari angka 5?",a:["101","110","111","100"],c:0},
  {q:"Hasil 12 × 8 = ?",a:["80","88","96","108"],c:2},
  {q:"Galaksi tempat Bumi berada?",a:["Andromeda","Milky Way","Sombrero","Triangulum"],c:1},
];

function pickChar(emoji,name,stats){
  player={emoji,name,...stats,hp:stats.hp};
  enemy={emoji:"👾",name:"Alien Grunt",hp:80,maxHP:80,atk:8,def:2};
  document.getElementById("screenSelect").style.display="none";
  document.getElementById("screenBattle").style.display="block";
  document.getElementById("pName").innerText=player.emoji+" "+player.name;
  document.getElementById("eName").innerText=enemy.emoji+" "+enemy.name;
  updateBars();
  nextQ();
}
function updateBars(){
  document.getElementById("pHP").style.width=(player.hp/player.hp)*100+"%";
  document.getElementById("pHPText").innerText=player.hp+" / "+player.hp;
  document.getElementById("eHP").style.width=(enemy.hp/enemy.maxHP)*100+"%";
  document.getElementById("eHPText").innerText=enemy.hp+" / "+enemy.maxHP;
}
function nextQ(){
  const q=questions[Math.floor(Math.random()*questions.length)];
  deck=q;
  document.getElementById("questionBox").innerText=q.q;
  let ansHTML="";
  q.a.forEach((ans,i)=>{
    ansHTML+=`<button class="btn" onclick="answer(${i})">${ans}</button><br>`;
  });
  document.getElementById("answers").innerHTML=ansHTML;
}
function answer(i){
  if(i===deck.c){
    enemy.hp-=player.atk;
    if(enemy.hp<=0){alert("Kamu menang!");return;}
  }else{
    player.hp-=enemy.atk;
    if(player.hp<=0){alert("Kamu kalah!");return;}
  }
  updateBars();
  nextQ();
}
</script>
</body>
</html>"""
