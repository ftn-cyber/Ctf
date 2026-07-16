<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>DONATE PLISS // BREACH PROTOCOL</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700;800&family=Share+Tech+Mono&display=swap" rel="stylesheet">
<style>
  :root{
    --bg: #030812;
    --panel: #071022;
    --panel-2: #0b1830;
    --line: #123055;
    --cyan: #35e6ff;
    --blue: #2f6fff;
    --dim: #4d7ba8;
    --text: #cfe8ff;
    --ok: #23ff9d;
    --err: #ff3860;
    --warn: #ffcf4d;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background: var(--bg);
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    min-height:100vh;
    overflow-x:hidden;
    position:relative;
  }
  canvas#rain{
    position:fixed; inset:0; z-index:0; opacity:0.35;
  }
  .scanlines{
    position:fixed; inset:0; z-index:1; pointer-events:none;
    background: repeating-linear-gradient(
      to bottom, rgba(255,255,255,0.02) 0px, rgba(255,255,255,0.02) 1px,
      transparent 1px, transparent 3px
    );
    mix-blend-mode: overlay;
  }
  .wrap{
    position:relative; z-index:2;
    max-width: 980px;
    margin: 0 auto;
    padding: 32px 20px 80px;
  }
  header{
    border: 1px solid var(--line);
    background: linear-gradient(180deg, var(--panel), var(--bg));
    border-radius: 4px;
    padding: 20px 24px;
    margin-bottom: 28px;
    position:relative;
    overflow:hidden;
  }
  header::before{
    content:"";
    position:absolute; top:0; left:0; right:0; height:2px;
    background: linear-gradient(90deg, transparent, var(--cyan), transparent);
    animation: sweep 3s linear infinite;
  }
  @keyframes sweep{
    0%{ transform: translateX(-100%); }
    100%{ transform: translateX(100%); }
  }
  .eyebrow{
    font-family:'Share Tech Mono', monospace;
    color: var(--dim);
    font-size: 12px;
    letter-spacing: 3px;
    text-transform: uppercase;
  }
  h1{
    margin: 6px 0 4px;
    font-size: clamp(24px, 5vw, 38px);
    letter-spacing: 1px;
    color: #eaf6ff;
    text-shadow: 0 0 12px rgba(53,230,255,0.35);
  }
  h1 span{ color: var(--cyan); }
  .sub{
    color: var(--dim);
    font-size: 13px;
    line-height: 1.6;
  }
  .progress-row{
    display:flex; gap:10px; margin-top:16px;
  }
  .bulb{
    flex:1;
    height: 8px;
    border-radius:2px;
    background: var(--panel-2);
    border: 1px solid var(--line);
    overflow:hidden;
    position:relative;
  }
  .bulb.done{ background: var(--ok); box-shadow: 0 0 10px var(--ok); border-color: var(--ok); }

  .start-btn{
    display: inline-block;
    margin-top: 18px;
    background: linear-gradient(135deg, var(--blue), var(--cyan));
    color: #001225;
    text-decoration: none;
    border: none;
    font-family: 'JetBrains Mono', monospace;
    font-weight: 800;
    font-size: 13px;
    letter-spacing: 1.5px;
    padding: 12px 26px;
    border-radius: 4px;
    cursor: pointer;
    text-transform: uppercase;
    transition: transform .15s, box-shadow .2s;
    box-shadow: 0 0 18px rgba(53,230,255,0.25);
  }
  .start-btn:hover{
    transform: translateY(-2px);
    box-shadow: 0 0 26px rgba(53,230,255,0.45);
  }

  .card{
    border: 1px solid var(--line);
    background: var(--panel);
    border-radius: 4px;
    margin-bottom: 22px;
    padding: 22px 24px;
    position: relative;
    transition: border-color .3s, box-shadow .3s;
  }
  .card.solved{
    border-color: var(--ok);
    box-shadow: 0 0 24px rgba(35,255,157,0.15);
  }
  .card-head{
    display:flex; align-items:center; justify-content:space-between;
    flex-wrap: wrap; gap: 10px;
    margin-bottom: 10px;
  }
  .flag-tag{
    font-family:'Share Tech Mono', monospace;
    color: var(--cyan);
    font-size: 13px;
    letter-spacing: 2px;
  }
  .status{
    font-size: 11px;
    padding: 3px 10px;
    border-radius: 20px;
    border: 1px solid var(--line);
    color: var(--dim);
    letter-spacing: 1px;
  }
  .status.locked{ color: var(--warn); border-color: var(--warn); }
  .status.open{ color: var(--ok); border-color: var(--ok); }

  .title-line{
    font-size: 16px;
    color: #eaf6ff;
    margin: 4px 0 12px;
  }
  .hint-box{
    background: var(--panel-2);
    border-left: 3px solid var(--blue);
    padding: 12px 14px;
    font-size: 13px;
    color: var(--dim);
    margin-bottom: 16px;
    line-height: 1.7;
    font-family: 'Share Tech Mono', monospace;
  }
  .hint-box b{ color: var(--cyan); }

  .prompt-row{
    display:flex; align-items:center; gap:8px;
    background: #01060d;
    border: 1px solid var(--line);
    border-radius: 3px;
    padding: 10px 12px;
    flex-wrap: wrap;
  }
  .prompt-row .ps1{
    color: var(--ok); font-size: 13px; white-space:nowrap;
  }
  .prompt-row input{
    flex: 1;
    min-width: 180px;
    background: transparent;
    border: none;
    outline: none;
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    font-size: 14px;
  }
  .prompt-row input::placeholder{ color: #375a80; }
  .submit-btn{
    background: var(--blue);
    color: #001225;
    border: none;
    font-weight: 700;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    letter-spacing: 1px;
    padding: 8px 16px;
    border-radius: 3px;
    cursor: pointer;
    text-transform: uppercase;
    transition: transform .15s, background .2s;
  }
  .submit-btn:hover{ background: var(--cyan); transform: translateY(-1px); }
  .submit-btn:disabled, .prompt-row input:disabled{
    opacity: 0.5; cursor: not-allowed; transform:none;
  }
  .submit-btn:disabled:hover{ background: var(--blue); }

  .reset-row{
    text-align:center; margin-top: 24px;
  }
  .reset-btn{
    background: transparent; color: var(--dim); border: 1px solid var(--line);
    font-family:'JetBrains Mono', monospace; font-size: 11px; letter-spacing: 1px;
    padding: 7px 16px; border-radius: 4px; cursor:pointer; text-transform: uppercase;
  }
  .reset-btn:hover{ color: var(--err); border-color: var(--err); }

  .feedback{
    margin-top: 10px; font-size: 12px; min-height: 16px;
    font-family:'Share Tech Mono', monospace;
  }
  .feedback.err{ color: var(--err); }
  .feedback.ok{ color: var(--ok); }

  .flag-value{
    margin-top: 12px;
    font-size: 13px;
    color: var(--ok);
    display:none;
  }
  .flag-value code{
    background:#021b12; border:1px solid var(--ok); padding:4px 10px; border-radius:3px;
  }

  footer{
    text-align:center; color: var(--dim); font-size: 12px; margin-top: 30px;
  }

  /* ===== Overlay Hacking Sequence ===== */
  #overlay{
    position: fixed; inset:0; background: rgba(1,4,10,0.97);
    z-index: 50; display:none; align-items:center; justify-content:center;
    padding: 20px;
  }
  #overlay.show{ display:flex; }
  .terminal{
    width: min(680px, 92vw);
    background: #000;
< truncated lines 261-387 >
      <button class="submit-btn" onclick="checkFlag(3)">exec</button>
    </div>
    <div class="feedback" id="feedback3"></div>
    <div class="flag-value" id="value3">Flag ditemukan: <code>yah aku udh ketahuan sebagai admin di web donate pliss</code></div>
  </div>

  <!-- FLAG 4 -->
  <div class="card" id="card4">
    <div class="card-head">
      <span class="flag-tag">🚩 FLAG_04 // COLD_CASE</span>
      <span class="status locked" id="status4">TERKUNCI</span>
    </div>
    <div class="title-line">Bayangan di Balik Admin</div>
    <div class="hint-box">
      <b>Hint:</b> "Aku adalah seorang yang terkait admin panel."
    </div>
    <div class="prompt-row">
      <span class="ps1">root@case:~$</span>
      <input type="text" id="input4" placeholder="masukkan jawaban flag..." autocomplete="off">
      <button class="submit-btn" onclick="checkFlag(4)">exec</button>
    </div>
    <div class="feedback" id="feedback4"></div>
    <div class="flag-value" id="value4">Flag ditemukan: <code>aku adalah pembunuh yaang membunuh Edo</code></div>
  </div>

  <!-- FLAG 5 -->
  <div class="card" id="card5">
    <div class="card-head">
      <span class="flag-tag">🚩 FLAG_05 // TAKEDOWN</span>
      <span class="status locked" id="status5">TERKUNCI</span>
    </div>
    <div class="title-line">Tangan Tak Terlihat</div>
    <div class="hint-box">
      <b>Hint:</b> "Aku adalah pejabat."
    </div>
    <div class="prompt-row">
      <span class="ps1">root@authority:~$</span>
      <input type="text" id="input5" placeholder="masukkan jawaban flag..." autocomplete="off">
      <button class="submit-btn" onclick="checkFlag(5)">exec</button>
    </div>
    <div class="feedback" id="feedback5"></div>
    <div class="flag-value" id="value5">Flag ditemukan: <code>aku adalah sebuah pejabat yang memblokir web donate pliss</code></div>
  </div>

  <div class="final-banner" id="finalBanner">
    ⚠ SEMUA LAPISAN KEAMANAN "DONATE PLISS" BERHASIL DITEMBUS ⚠<br>
    Kamu berhasil menyelesaikan kelima tantangan. Sistem donate pliss resmi dinyatakan aman kembali setelah dilaporkan.
    <br><br>
    Akses terakhir yang ditemukan:
    <br>
    <a href="https://ftn-cyber.github.io/Admin-panel-donate-pliss/" target="_blank" rel="noopener noreferrer" style="color:var(--ok); word-break:break-all;">
      https://ftn-cyber.github.io/Admin-panel-donate-pliss/
    </a>
    <br><br>
    Username: <code>root</code><br>
    Password: <code>edorauhan donate pliss</code>
  </div>

  <div class="reset-row">
    <button class="reset-btn" onclick="resetProgress()">↺ Reset Progres Tersimpan</button>
  </div>

  <footer>DONATE PLISS SECURITY LAB — simulasi edukatif, tidak terhubung ke sistem nyata.</footer>
</div>

<div id="overlay">
  <div>
    <div class="terminal">
      <div class="term-bar"><span>breach_sequence.sh</span><span id="termFlagLabel">FLAG_01</span></div>
      <div class="term-body" id="termBody"></div>
    </div>
    <div class="glitch" id="glitchText">ACCESS GRANTED</div>
    <button class="close-btn" onclick="closeOverlay()">[ tutup terminal ]</button>
  </div>
</div>

<script>
// ================= Matrix rain background =================
const canvas = document.getElementById('rain');
const ctx = canvas.getContext('2d');
function resize(){ canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
resize(); window.addEventListener('resize', resize);
const glyphs = "01アイウエオカキクケコ$#%&*<>/\\{}[]";
const fontSize = 15;
let columns = Math.floor(canvas.width / fontSize);
let drops = new Array(columns).fill(1);
function drawRain(){
  ctx.fillStyle = 'rgba(3,8,18,0.12)';
  ctx.fillRect(0,0,canvas.width,canvas.height);
  ctx.fillStyle = '#35e6ff';
  ctx.font = fontSize + 'px monospace';
  for(let i=0;i<drops.length;i++){
    const text = glyphs[Math.floor(Math.random()*glyphs.length)];
    ctx.fillText(text, i*fontSize, drops[i]*fontSize);
    if(drops[i]*fontSize > canvas.height && Math.random() > 0.975){ drops[i] = 0; }
    drops[i]++;
  }
}
setInterval(drawRain, 50);

// ================= Penyimpanan progres di perangkat (localStorage) =================
const STORAGE_KEY = 'donatePlissCtfProgress';

function saveProgress(){
  try{
    localStorage.setItem(STORAGE_KEY, JSON.stringify(solved));
  }catch(e){
    console.error('Gagal menyimpan progres ke perangkat:', e);
  }
}

function applySolvedUI(n, animate){
  document.getElementById('card'+n).classList.add('solved');
  document.getElementById('status'+n).textContent = "TEREKSPOS";
  document.getElementById('status'+n).className = "status open";
  document.getElementById('value'+n).style.display = "block";
  document.getElementById('bulb'+n).classList.add('done');
  const input = document.getElementById('input'+n);
  input.value = "";
  input.disabled = true;
  document.querySelector('#card'+n+' .submit-btn').disabled = true;

  if(n === 4){
    const startBtn = document.getElementById('startBtn');
    startBtn.href = "https://ftn-cyber.github.io/Donate-pliss-blocked/";
    startBtn.textContent = "▶ Lihat Server Donate Pliss";
  }
}

function loadProgress(){
  let saved = null;
  try{
    const raw = localStorage.getItem(STORAGE_KEY);
    if(raw) saved = JSON.parse(raw);
  }catch(e){
    console.error('Gagal memuat progres dari perangkat:', e);
  }
  if(!saved) return;
  for(let n=1; n<=5; n++){
    if(saved[n]){
      solved[n] = true;
      applySolvedUI(n);
    }
  }
  checkAllSolved();
}

function resetProgress(){
  if(!confirm('Hapus semua progres yang tersimpan di perangkat ini?')) return;
  try{ localStorage.removeItem(STORAGE_KEY); }catch(e){}
  location.reload();
}

window.addEventListener('DOMContentLoaded', loadProgress);

// ================= Flag logic =================
const answers = {
  1: "satpam sql injection telah ketahuan",
  2: "yah hacker yang pura-pura donate ketahuan",
  3: "yah aku udh ketahuan sebagai admin di web donate pliss",
  4: "aku adalah pembunuh yaang membunuh edo",
  5: "aku adalah sebuah pejabat yang memblokir web donate pliss"
};
const solved = {1:false, 2:false, 3:false, 4:false, 5:false};

function normalize(str){
  return str
    .toLowerCase()
    .trim()
    .replace(/^flag\{(.*)\}$/,'$1')
    .replace(/[.,!?;:"'`]/g, '')
    .replace(/\s+/g, ' ')
    .trim();
}

function checkFlag(n){
  const input = document.getElementById('input'+n);
  const feedback = document.getElementById('feedback'+n);
  const val = normalize(input.value);
  if(val === answers[n]){
    feedback.textContent = "✓ Jawaban benar. Memulai sekuens penetrasi...";
    feedback.className = "feedback ok";
    solved[n] = true;
    applySolvedUI(n);
    saveProgress();
    runHackSequence(n);
    checkAllSolved();
  } else if(val.length === 0){
    feedback.textContent = "Masukkan jawaban terlebih dahulu.";
    feedback.className = "feedback err";
  } else {
    feedback.textContent = "✗ Jawaban salah. Coba baca ulang hint-nya.";
    feedback.className = "feedback err";
  }
}

function checkAllSolved(){
  if(solved[1] && solved[2] && solved[3] && solved[4] && solved[5]){
    setTimeout(()=>{ document.getElementById('finalBanner').style.display = 'block'; }, 800);
  }
}

// ================= Hacking overlay animation =================
const hackLines = [
  "[*] Menghubungkan ke server donate-pliss.local ...",
  "[*] Melewati firewall lapis-1 ................ OK",
  "[*] Menyuntikkan paket payload ke port 443 ....",
  "[*] Mendekripsi tabel kredensial ..............",
  "[*] Menganalisis pola akses log admin .........",
  "[*] Menyusun ulang fragmen data flag ..........",
  "[*] Memverifikasi integritas token sesi .......",
  "[*] Mengonfirmasi identitas target ............",
];

function runHackSequence(n){
  const overlay = document.getElementById('overlay');
  const body = document.getElementById('termBody');
  const glitch = document.getElementById('glitchText');
  const label = document.getElementById('termFlagLabel');
  label.textContent = "FLAG_0" + n;
  body.innerHTML = "";
  glitch.style.display = "none";
  overlay.classList.add('show');

  let i = 0;
  function typeLine(){
    if(i < hackLines.length){
      const line = document.createElement('div');
      body.appendChild(line);
      let charIndex = 0;
      const text = hackLines[i];
      const typer = setInterval(()=>{
        line.textContent = text.slice(0, charIndex) + (charIndex < text.length ? "▌" : "");
        charIndex++;
        body.scrollTop = body.scrollHeight;
        if(charIndex > text.length){
          clearInterval(typer);
          i++;
          setTimeout(typeLine, 150);
        }
      }, 18);
    } else {
      const done = document.createElement('div');
      done.style.color = "#7dffb0";
      done.style.marginTop = "10px";
      done.textContent = "[✓] FLAG_0"+n+" berhasil diekstraksi dari sistem donate pliss.";
      body.appendChild(done);
      body.scrollTop = body.scrollHeight;
      setTimeout(()=>{ glitch.style.display = "block"; }, 400);
    }
  }
  typeLine();
}

function closeOverlay(){
  document.getElementById('overlay').classList.remove('show');
}
</script>
</body>
</html>
