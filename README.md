<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<title>Pickleball Scoreboard</title>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent;
}
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  background: #f5f7fa;
  padding: 12px;
  max-width: 100%;
}
.card {
  background: white;
  border-radius: 16px;
  padding: 16px;
  margin-bottom: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}
.title {
  text-align: center;
  color: #007aff;
  font-size: 22px;
  margin-bottom: 12px;
}
.lang-row {
  display: flex;
  gap: 8px;
  margin-bottom: 10px;
}
.lang-btn {
  flex:1;
  padding:10px;
  border-radius:12px;
  border:none;
  background:#eef2ff;
  font-size:15px;
  font-weight:500;
}
.lang-btn.active {
  background:#007aff;
  color:white;
}
.name-row {
  display: flex;
  gap: 10px;
  margin-bottom: 10px;
}
.name-group {
  flex: 1;
}
.name-group label {
  font-size: 12px;
  color: #666;
}
.name-group input {
  width: 100%;
  padding: 10px;
  border-radius: 10px;
  border: 1px solid #ddd;
  font-size: 16px;
  margin-top: 4px;
}
.btn-row {
  display: flex;
  gap: 8px;
  margin-bottom: 10px;
}
.btn {
  flex: 1;
  padding: 12px 10px;
  border-radius: 12px;
  border: none;
  background: #eef2ff;
  font-size: 15px;
  font-weight: 500;
  color: #333;
  cursor: pointer;
}
.btn.active {
  background: #007aff;
  color: white;
}
.btn:disabled {
  background: #e0e0e0;
  color: #999;
  cursor: not-allowed;
}
.timer {
  text-align: center;
  font-size: 32px;
  font-weight: bold;
  margin: 10px 0;
  color: #222;
}
.timer-row {
  display: flex;
  gap: 8px;
  justify-content: center;
  margin-bottom: 10px;
}
.timer-btn {
  padding: 10px 14px;
  border-radius: 10px;
  border: none;
  background: #eef2ff;
  font-size: 15px;
}
.win-score {
  text-align: center;
  margin: 10px 0;
  font-size: 15px;
}
.win-score input {
  width: 60px;
  padding: 8px;
  border-radius: 8px;
  border: 1px solid #ddd;
  text-align: center;
  font-size: 16px;
}
.score-box {
  display: flex;
  align-items: center;
  justify-content: space-around;
  text-align: center;
  margin: 16px 0;
}
.score-box h2 {
  font-size: 18px;
  margin-bottom: 4px;
}
.score-num {
  font-size: 48px;
  font-weight: bold;
}
.score-call {
  text-align: center;
  font-size: 20px;
  font-weight: bold;
  margin: 8px 0;
  color: #222;
}
.server {
  text-align: center;
  font-size: 16px;
  color: #007aff;
  font-weight: 600;
  margin-bottom: 10px;
}
.court {
  display: grid;
  grid-template-areas:
    "aLeft bRight"
    "aRight bLeft";
  grid-template-columns: 1fr 1fr;
  gap: 8px;
  margin: 20px auto;
  max-width: 320px;
}
.zone {
  border: 2px solid #ddd;
  border-radius: 12px;
  padding: 14px 8px;
  text-align: center;
  font-weight: 600;
  background: #f8f9fa;
}
.zone.serve {
  background: #ffeb3b;
  border-color: #ff9900;
}
.zone.receive {
  background: #d1e7ff;
  border-color: #007aff;
}
.zone-a-right { grid-area: aRight; }
.zone-a-left  { grid-area: aLeft; }
.zone-b-right { grid-area: bRight; }
.zone-b-left  { grid-area: bLeft; }
.action {
  display: flex;
  gap: 12px;
  margin: 20px 0;
}
.action-btn {
  flex: 1;
  padding: 24px 12px;
  border-radius: 16px;
  border: none;
  font-size: 17px;
  font-weight: bold;
  color: white;
  cursor: pointer;
}
.action-a { background: #007aff; }
.action-b { background: #34c759; }
.utility {
  display: flex;
  gap: 8px;
  margin-bottom: 12px;
}
.utility-btn {
  flex: 1;
  padding: 12px;
  border-radius: 12px;
  border: none;
  font-size: 15px;
  color: white;
}
.undo    { background: #888; }
.reset   { background: #ff9500; }
.clear   { background: #ff3b30; }
.winner  { text-align: center; font-size: 22px; color: #34c759; font-weight: bold; margin:16px 0; }
.next-game {
  display: block; margin:0 auto 20px; padding:14px 24px; border-radius:14px;
  background:#34c759; color:white; font-size:17px; border:none; font-weight:bold;
}
.history h3 {
  text-align: center; margin-bottom:10px; font-size:18px;
}
table {
  width:100%; border-collapse:collapse; border-radius:12px; overflow:hidden;
}
th,td { padding:12px; text-align:center; border-bottom:1px solid #eee; }
th { background:#f2f2f7; font-weight:600; }
.win-text { color:#34c759; font-weight:600; }
.hidden { display:none !important; }
</style>
</head>

<body>

<h1 class="title" id="pageTitle">Pickleball Scoreboard</h1>

<div class="card">
  <div class="lang-row">
    <button class="lang-btn active" id="btnEn">English</button>
    <button class="lang-btn" id="btnCn">中文</button>
  </div>

  <div class="name-row">
    <div class="name-group">
      <label id="labelTeamA">Team A</label>
      <input type="text" id="teamA" value="Team A">
    </div>
    <div class="name-group">
      <label id="labelTeamB">Team B</label>
      <input type="text" id="teamB" value="Team B">
    </div>
  </div>

  <div class="btn-row">
    <button class="btn" id="singlesBtn">Singles</button>
    <button class="btn" id="doublesBtn">Doubles</button>
  </div>

  <div class="btn-row">
    <button class="btn" id="serveOnlyBtn" disabled>Serve Only</button>
    <button class="btn" id="rallyBtn" disabled>Rally Scoring</button>
  </div>

  <div class="timer" id="timerDisplay">00:00</div>
  <div class="timer-row">
    <button class="timer-btn" id="startTimer">Start</button>
    <button class="timer-btn" id="pauseTimer">Pause</button>
    <button class="timer-btn" id="resetTimer">Reset</button>
  </div>

  <div class="win-score">
    <span id="winScoreText">Win Score:</span> <input type="number" id="winScore" value="11">
  </div>
</div>

<div class="card">
  <div class="score-box">
    <div>
      <h2 id="teamAName">Team A</h2>
      <div class="score-num" id="scoreA">0</div>
    </div>
    <h2 id="vsText">VS</h2>
    <div>
      <h2 id="teamBName">Team B</h2>
      <div class="score-num" id="scoreB">0</div>
    </div>
  </div>

  <div class="server" id="serverText">Server: Team A (Right)</div>
  <div class="score-call" id="scoreCall">Score: 0 - 0</div>
</div>

<div id="singlesCourt" class="court hidden">
  <div class="zone zone-a-left" id="aLeft">A Left</div>
  <div class="zone zone-b-right" id="bRight">B Right</div>
  <div class="zone zone-a-right" id="aRight">A Right</div>
  <div class="zone zone-b-left" id="bLeft">B Left</div>
</div>

<div id="doublesCourt" class="court hidden">
  <div class="zone zone-a-left" id="dALeft">A Left</div>
  <div class="zone zone-b-right" id="dBRight">B Right</div>
  <div class="zone zone-a-right" id="dARight">A Right</div>
  <div class="zone zone-b-left" id="dBLeft">B Left</div>
</div>

<div id="winArea" class="hidden">
  <div class="winner" id="winnerText"></div>
  <button class="next-game" id="nextGame">Next Game</button>
</div>

<div class="action">
  <button class="action-btn action-a" id="winA">Team A wins rally</button>
  <button class="action-btn action-b" id="winB">Team B wins rally</button>
</div>

<div class="utility">
  <button class="utility-btn undo" id="undo">Undo</button>
  <button class="utility-btn reset" id="reset">Reset Game</button>
  <button class="utility-btn clear" id="clearAll">Clear History</button>
</div>

<div class="card history">
  <h3 id="historyTitle">Match History</h3>
  <table>
    <tr>
      <th id="thGame">Game</th>
      <th id="thA">Team A</th>
      <th id="thB">Team B</th>
      <th id="thWinner">Winner</th>
    </tr>
    <tbody id="recordBody"></tbody>
  </table>
</div>

<script>
const texts = {
  en: {
    title: "Pickleball Scoreboard",
    teamA: "Team A",
    teamB: "Team B",
    singles: "Singles",
    doubles: "Doubles",
    serveOnly: "Serve Only",
    rally: "Rally Scoring",
    winScore: "Win Score:",
    vs: "VS",
    score: "Score:",
    server: "Server:",
    start: "Start",
    pause: "Pause",
    reset: "Reset",
    winA: "Team A wins rally",
    winB: "Team B wins rally",
    undo: "Undo",
    resetGame: "Reset Game",
    clearHistory: "Clear History",
    nextGame: "Next Game",
    history: "Match History",
    game: "Game",
    winner: "Winner",
    right: "Right",
    left: "Left"
  },
  cn: {
    title: "匹克球记分牌",
    teamA: "A队",
    teamB: "B队",
    singles: "单打",
    doubles: "双打",
    serveOnly: "发球得分",
    rally: "每球得分",
    winScore: "获胜分数:",
    vs: "对战",
    score: "比分:",
    server: "发球方:",
    start: "开始",
    pause: "暂停",
    reset: "重置",
    winA: "A队赢下此球",
    winB: "B队赢下此球",
    undo: "撤销",
    resetGame: "重置本局",
    clearHistory: "清空记录",
    nextGame: "下一局",
    history: "比赛记录",
    game: "局数",
    winner: "胜者",
    right: "右区",
    left: "左区"
  }
};

const state = {
  lang: 'en',
  mode: null, // null = not selected yet
  scoring: null,
  a: 0, b: 0,
  winScore: 11,
  server: 'A',
  serverNum: 2,
  firstServiceDone: false,
  winner: '',
  history: [],
  lastState: null,
  seconds: 0,
  timer: null
};

const $ = (id) => document.getElementById(id);

function setLang(lang) {
  state.lang = lang;
  const t = texts[lang];
  $('pageTitle').innerText = t.title;
  $('labelTeamA').innerText = t.teamA;
  $('labelTeamB').innerText = t.teamB;
  $('singlesBtn').innerText = t.singles;
  $('doublesBtn').innerText = t.doubles;
  $('serveOnlyBtn').innerText = t.serveOnly;
  $('rallyBtn').innerText = t.rally;
  $('winScoreText').innerText = t.winScore;
  $('vsText').innerText = t.vs;
  $('startTimer').innerText = t.start;
  $('pauseTimer').innerText = t.pause;
  $('resetTimer').innerText = t.reset;
  $('winA').innerText = t.winA;
  $('winB').innerText = t.winB;
  $('undo').innerText = t.undo;
  $('reset').innerText = t.resetGame;
  $('clearAll').innerText = t.clearHistory;
  $('nextGame').innerText = t.nextGame;
  $('historyTitle').innerText = t.history;
  $('thGame').innerText = t.game;
  $('thA').innerText = t.teamA;
  $('thB').innerText = t.teamB;
  $('thWinner').innerText = t.winner;

  document.querySelectorAll('.lang-btn').forEach(btn => btn.classList.remove('active'));
  lang === 'en' ? $('btnEn').classList.add('active') : $('btnCn').classList.add('active');
  render();
}

function enableScoringButtons(enable) {
  $('serveOnlyBtn').disabled = !enable;
  $('rallyBtn').disabled = !enable;
}

function selectMode(mode) {
  state.mode = mode;
  state.scoring = null;
  document.querySelectorAll('.btn').forEach(b => b.classList.remove('active'));
  mode === 'singles' ? $('singlesBtn').classList.add('active') : $('doublesBtn').classList.add('active');
  enableScoringButtons(true);
  render();
}

function selectScoring(scoring) {
  if (!state.mode) return;
  state.scoring = scoring;
  document.querySelectorAll('.btn-row:nth-child(4) .btn').forEach(b => b.classList.remove('active'));
  scoring === 'serveOnly' ? $('serveOnlyBtn').classList.add('active') : $('rallyBtn').classList.add('active');
  render();
}

function startTimer() {
  if (state.timer) return;
  state.timer = setInterval(() => { state.seconds++; updateTimer(); }, 1000);
}
function pauseTimer() { clearInterval(state.timer); state.timer = null; }
function resetTimer() { pauseTimer(); state.seconds = 0; updateTimer(); }
function updateTimer() {
  const m = String(Math.floor(state.seconds/60)).padStart(2,'0');
  const s = String(state.seconds%60).padStart(2,'0');
  $('timerDisplay').innerText = `${m}:${s}`;
}

function syncNames() {
  $('teamAName').innerText = $('teamA').value || texts[state.lang].teamA;
  $('teamBName').innerText = $('teamB').value || texts[state.lang].teamB;
}

function render() {
  syncNames();
  const t = texts[state.lang];
  $('scoreA').innerText = state.a;
  $('scoreB').innerText = state.b;
  $('winArea').classList.toggle('hidden', !state.winner);
  if (state.winner) $('winnerText').innerText = `${state.winner} ${t.winner}!`;

  // Show court
  if (state.mode === 'singles') {
    $('singlesCourt').classList.remove('hidden');
    $('doublesCourt').classList.add('hidden');
  } else if (state.mode === 'doubles') {
    $('doublesCourt').classList.remove('hidden');
    $('singlesCourt').classList.add('hidden');
  } else {
    $('singlesCourt').classList.add('hidden');
    $('doublesCourt').classList.add('hidden');
  }

  // Score display
  const srv = state.server === 'A' ? state.a : state.b;
  const rec = state.server === 'A' ? state.b : state.a;
  if (state.scoring === 'serveOnly' && state.mode === 'doubles') {
    $('scoreCall').innerText = `${t.score} ${srv} - ${rec} - ${state.serverNum}`;
  } else {
    $('scoreCall').innerText = `${t.score} ${srv} - ${rec}`;
  }

  updateServer();
  highlightCourt();
  updateHistory();
}

function updateServer() {
  const t = texts[state.lang];
  if (!state.mode) {
    $('serverText').innerText = `${t.server} —`;
    return;
  }
  const score = state.server === 'A' ? state.a : state.b;
  const side = state.scoring === 'rally' ? (score % 2 === 0 ? t.right : t.left) : t.right;
  const name = state.server === 'A' ? $('teamA').value : $('teamB').value;
  let num = '';
  if (state.mode === 'doubles' && state.scoring === 'serveOnly') num = ` #${state.serverNum}`;
  $('serverText').innerText = `${t.server} ${name}${num} (${side})`;
}

function highlightCourt() {
  if (!state.mode) return;
  document.querySelectorAll('.zone').forEach(z => z.classList.remove('serve','receive'));
  const t = texts[state.lang];
  const score = state.server === 'A' ? state.a : state.b;
  const side = (state.scoring === 'rally' && score % 2 !== 0) ? 'L' : 'R';

  let s, r;
  if (state.mode === 'singles') {
    if (state.server === 'A') {
      s = side === 'R' ? 'aRight' : 'aLeft';
      r = side === 'R' ? 'bRight' : 'bLeft';
    } else {
      s = side === 'R' ? 'bRight' : 'bLeft';
      r = side === 'R' ? 'aRight' : 'aLeft';
    }
  } else {
    if (state.server === 'A') {
      s = side === 'R' ? 'dARight' : 'dALeft';
      r = side === 'R' ? 'dBRight' : 'dBLeft';
    } else {
      s = side === 'R' ? 'dBRight' : 'dBLeft';
      r = side === 'R' ? 'dARight' : 'dALeft';
    }
  }
  $(s).classList.add('serve');
  $(r).classList.add('receive');
}

function isGameOver() {
  const max = Math.max(state.a, state.b);
  const diff = Math.abs(state.a-state.b);
  return max >= state.winScore && diff >=2;
}

function saveState() {
  state.lastState = JSON.parse(JSON.stringify(state));
}

function rallyWin(winner) {
  if (!state.scoring || state.winner) return;
  saveState();
  winner === 'A' ? state.a++ : state.b++;
  state.server = winner;
  state.winner = isGameOver() ? (winner === 'A' ? $('teamA').value : $('teamB').value) : '';
  render();
}

function serveOnlyWin(winner) {
  if (!state.scoring || state.winner) return;
  saveState();
  if (state.server === winner) {
    state[winner === 'A' ? 'a' : 'b']++;
  } else {
    if (!state.firstServiceDone) {
      state.firstServiceDone = true;
      state.server = state.server === 'A' ? 'B' : 'A';
      state.serverNum = 1;
    } else {
      state.serverNum === 1 ? (state.serverNum = 2) : (state.server = state.server === 'A' ? 'B' : 'A', state.serverNum = 1);
    }
  }
  state.winner = isGameOver() ? (state.server === 'A' ? $('teamA').value : $('teamB').value) : '';
  render();
}

function updateHistory() {
  const b = $('recordBody'); b.innerHTML='';
  state.history.forEach((g,i)=>{
    const tr=document.createElement('tr');
    tr.innerHTML=`<td>${i+1}</td><td>${g.a}</td><td>${g.b}</td><td class="win-text">${g.winner}</td>`;
    b.appendChild(tr);
  });
}

// Bindings
$('winA').onclick = ()=> state.scoring==='rally' ? rallyWin('A') : serveOnlyWin('A');
$('winB').onclick = ()=> state.scoring==='rally' ? rallyWin('B') : serveOnlyWin('B');

$('singlesBtn').onclick = ()=>selectMode('singles');
$('doublesBtn').onclick = ()=>selectMode('doubles');
$('serveOnlyBtn').onclick = ()=>selectScoring('serveOnly');
$('rallyBtn').onclick = ()=>selectScoring('rally');

$('startTimer').onclick = startTimer;
$('pauseTimer').onclick = pauseTimer;
$('resetTimer').onclick = resetTimer;

$('undo').onclick = ()=>{ if(state.lastState){ Object.assign(state, state.lastState); render(); } };
$('reset').onclick = ()=>{
  saveState();
  state.a=state.b=0; state.winner=''; state.server='A'; state.serverNum=2; state.firstServiceDone=false;
  render();
};
$('nextGame').onclick = ()=>{
  state.history.push({a:state.a,b:state.b,winner:state.winner});
  state.a=state.b=0; state.winner=''; state.server='A'; state.serverNum=2; state.firstServiceDone=false;
  render();
};
$('clearAll').onclick = ()=>{ state.history=[]; render(); };

$('teamA').addEventListener('input', render);
$('teamB').addEventListener('input', render);
$('btnEn').onclick = ()=>setLang('en');
$('btnCn').onclick = ()=>setLang('cn');

setLang('en');
</script>
</body>
</html>
