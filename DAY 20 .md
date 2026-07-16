<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1, user-scalable=no">
<title>Puzzle Booth — Face Puzzle Game</title>
<style>
  :root{
    --bg-deep: #1b1f3b;
    --bg-deep-2: #12142a;
    --paper: #fdf6ec;
    --ink: #2a2418;
    --ink-soft: #6b6455;
    --marigold: #f4a621;
    --marigold-dark: #c9800f;
    --coral: #ef6461;
    --teal: #3f9d77;
    --line: rgba(42,36,24,0.14);
    --cream: #f4efe4;
    --font-display: Georgia, 'Times New Roman', serif;
    --font-mono: ui-monospace, 'SFMono-Regular', Menlo, Consolas, 'Courier New', monospace;
  }

  * { box-sizing: border-box; }

  html, body {
    margin: 0;
    padding: 0;
    min-height: 100%;
    background: radial-gradient(circle at 20% -10%, #2a2f57 0%, var(--bg-deep) 45%, var(--bg-deep-2) 100%);
    color: var(--cream);
    font-family: var(--font-display);
    -webkit-font-smoothing: antialiased;
  }

  body {
    display: flex;
    flex-direction: column;
    align-items: center;
    min-height: 100vh;
    padding: 24px 16px 60px;
  }

  .brand {
    text-align: center;
    margin-bottom: 22px;
  }

  .brand .eyebrow {
    font-family: var(--font-mono);
    letter-spacing: 0.32em;
    font-size: 11px;
    text-transform: uppercase;
    color: var(--marigold);
    margin: 0 0 6px;
  }

  .brand h1 {
    margin: 0;
    font-size: clamp(28px, 6vw, 44px);
    font-weight: 700;
    letter-spacing: -0.01em;
  }

  .brand h1 span {
    color: var(--coral);
    font-style: italic;
  }

  .brand p {
    margin: 8px 0 0;
    color: rgba(244,239,228,0.65);
    font-size: 14px;
  }

  .stage {
    width: 100%;
    max-width: 560px;
  }

  .screen {
    display: none;
  }
  .screen.active {
    display: block;
    animation: fadeUp 0.35s ease;
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(8px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .panel {
    background: var(--paper);
    color: var(--ink);
    border-radius: 18px;
    padding: 22px;
    box-shadow: 0 24px 50px -20px rgba(0,0,0,0.55), 0 2px 0 rgba(255,255,255,0.04) inset;
  }

  .frame-wrap {
    position: relative;
    border-radius: 12px;
    overflow: hidden;
    background: #000;
    aspect-ratio: 1 / 1;
    max-width: 420px;
    margin: 0 auto;
  }

  .frame-wrap::before {
    content: "";
    position: absolute;
    inset: 0;
    border: 3px solid rgba(244,166,33,0.9);
    border-radius: 12px;
    pointer-events: none;
    z-index: 3;
  }

  .corner-tick {
    position: absolute;
    width: 18px;
    height: 18px;
    border: 3px solid var(--marigold);
    z-index: 4;
  }
  .corner-tick.tl { top: -3px; left: -3px; border-right: none; border-bottom: none; }
  .corner-tick.tr { top: -3px; right: -3px; border-left: none; border-bottom: none; }
  .corner-tick.bl { bottom: -3px; left: -3px; border-right: none; border-top: none; }
  .corner-tick.br { bottom: -3px; right: -3px; border-left: none; border-top: none; }

  video#camVideo {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transform: scaleX(-1);
    display: block;
  }

  #captureCanvas, #previewCanvas {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }

  .cam-status {
    text-align: center;
    font-family: var(--font-mono);
    font-size: 13px;
    color: var(--ink-soft);
    margin-top: 14px;
    min-height: 18px;
  }

  .btn-row {
    display: flex;
    gap: 10px;
    justify-content: center;
    flex-wrap: wrap;
    margin-top: 18px;
  }

  button, .file-label {
    font-family: var(--font-mono);
    font-size: 13px;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    border: none;
    border-radius: 999px;
    padding: 13px 22px;
    cursor: pointer;
    font-weight: 700;
    transition: transform 0.12s ease, box-shadow 0.12s ease, opacity 0.12s ease;
    display: inline-flex;
    align-items: center;
    gap: 8px;
  }
  button:active, .file-label:active { transform: scale(0.96); }
  button:disabled { opacity: 0.45; cursor: not-allowed; }

  .btn-primary {
    background: var(--marigold);
    color: #241a02;
    box-shadow: 0 8px 18px -6px rgba(244,166,33,0.6);
  }
  .btn-primary:hover:not(:disabled) { background: var(--marigold-dark); }

  .btn-ghost {
    background: transparent;
    color: var(--ink);
    border: 2px solid var(--line);
  }
  .btn-ghost:hover:not(:disabled) { border-color: var(--ink); }

  .btn-coral {
    background: var(--coral);
    color: #2a0d0c;
    box-shadow: 0 8px 18px -6px rgba(239,100,97,0.55);
  }

  .file-label {
    background: rgba(0,0,0,0.06);
    color: var(--ink);
    border: 2px dashed var(--line);
  }
  input[type="file"] { display: none; }

  .difficulty-select {
    margin-top: 20px;
  }

  .difficulty-select p.label {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--ink-soft);
    margin: 0 0 10px;
    text-align: center;
  }

  .seg {
    display: flex;
    gap: 8px;
    justify-content: center;
  }

  .seg button {
    background: rgba(0,0,0,0.05);
    color: var(--ink);
    border: 2px solid transparent;
    border-radius: 12px;
    padding: 12px 18px;
    min-width: 68px;
    justify-content: center;
  }

  .seg button.selected {
    background: var(--paper);
    border-color: var(--marigold);
    color: var(--marigold-dark);
    box-shadow: 0 4px 10px -4px rgba(244,166,33,0.5);
  }

  /* --- Ticket stub stats bar --- */
  .ticket {
    position: relative;
    background: var(--paper);
    border-radius: 14px;
    margin-bottom: 16px;
    padding: 14px 22px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 10px;
    box-shadow: 0 16px 30px -18px rgba(0,0,0,0.55);
  }
  .ticket::before, .ticket::after {
    content: "";
    position: absolute;
    top: 50%;
    width: 22px;
    height: 22px;
    background: var(--bg-deep-2);
    border-radius: 50%;
    transform: translateY(-50%);
  }
  .ticket::before { left: -11px; }
  .ticket::after { right: -11px; }

  .ticket-stat {
    font-family: var(--font-mono);
    text-align: center;
  }
  .ticket-stat .num {
    font-size: 20px;
    font-weight: 700;
    color: var(--ink);
    display: block;
    letter-spacing: 0.02em;
  }
  .ticket-stat .lbl {
    font-size: 10px;
    letter-spacing: 0.16em;
    text-transform: uppercase;
    color: var(--ink-soft);
  }
  .ticket-divider {
    width: 1px;
    height: 30px;
    background: repeating-linear-gradient(to bottom, var(--line) 0 4px, transparent 4px 8px);
  }

  /* --- Puzzle board --- */
  .board-wrap {
    max-width: 420px;
    margin: 0 auto;
  }

  #puzzleBoard {
    display: grid;
    gap: 4px;
    width: 100%;
    aspect-ratio: 1 / 1;
    background: var(--bg-deep-2);
    border-radius: 10px;
    padding: 4px;
    touch-action: none;
    user-select: none;
  }

  .tile {
    position: relative;
    border-radius: 6px;
    overflow: hidden;
    cursor: grab;
    border: 3px solid transparent;
    background-color: #333;
    background-repeat: no-repeat;
    transition: border-color 0.15s ease, box-shadow 0.15s ease;
    -webkit-user-drag: none;
    touch-action: none;
  }

  .tile .badge {
    position: absolute;
    top: 3px;
    left: 3px;
    background: rgba(0,0,0,0.55);
    color: #fff;
    font-family: var(--font-mono);
    font-size: 10px;
    line-height: 1;
    padding: 3px 5px;
    border-radius: 5px;
    pointer-events: none;
  }

  .tile.correct {
    border-color: var(--teal);
    box-shadow: 0 0 0 2px rgba(63,157,119,0.35);
  }

  .tile.is-source {
    opacity: 0.25;
    outline: 2px dashed rgba(244,239,228,0.6);
    outline-offset: -2px;
  }

  .tile.drop-hover {
    border-color: var(--marigold);
  }

  .tile-ghost {
    position: fixed;
    border-radius: 6px;
    border: 3px solid var(--coral) !important;
    box-shadow: 0 18px 30px -10px rgba(0,0,0,0.6);
    pointer-events: none;
    z-index: 1000;
    background-repeat: no-repeat;
  }

  .puzzle-toolbar {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-top: 16px;
    flex-wrap: wrap;
  }

  .hint-toggle {
    display: flex;
    align-items: center;
    gap: 8px;
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--ink-soft);
    justify-content: center;
    margin-top: 12px;
  }
  .hint-toggle input { transform: scale(1.1); }

  /* --- Overlay --- */
  .overlay {
    position: fixed;
    inset: 0;
    background: rgba(18,20,42,0.82);
    display: none;
    align-items: center;
    justify-content: center;
    padding: 20px;
    z-index: 2000;
  }
  .overlay.active { display: flex; }

  .overlay-panel {
    background: var(--paper);
    color: var(--ink);
    border-radius: 20px;
    padding: 30px;
    max-width: 420px;
    width: 100%;
    text-align: center;
    box-shadow: 0 30px 60px -20px rgba(0,0,0,0.6);
    animation: popIn 0.3s cubic-bezier(.2,1.4,.4,1);
  }

  @keyframes popIn {
    from { opacity: 0; transform: scale(0.9); }
    to { opacity: 1; transform: scale(1); }
  }

  .overlay-panel .eyebrow {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--teal);
    margin: 0 0 6px;
  }

  .overlay-panel h2 {
    margin: 0 0 18px;
    font-size: 28px;
  }

  .result-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    margin-bottom: 20px;
  }
  .result-grid div {
    background: rgba(0,0,0,0.05);
    border-radius: 12px;
    padding: 12px 6px;
  }
  .result-grid .num {
    font-family: var(--font-mono);
    font-weight: 700;
    font-size: 18px;
    display: block;
  }
  .result-grid .lbl {
    font-family: var(--font-mono);
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 0.12em;
    color: var(--ink-soft);
  }

  .leaderboard {
    margin-top: 8px;
    text-align: left;
    background: rgba(0,0,0,0.04);
    border-radius: 12px;
    padding: 12px 16px;
  }
  .leaderboard h3 {
    font-family: var(--font-mono);
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--ink-soft);
    margin: 0 0 10px;
  }
  .leaderboard ol {
    margin: 0;
    padding-left: 20px;
    font-family: var(--font-mono);
    font-size: 13px;
  }
  .leaderboard li {
    margin-bottom: 6px;
    display: flex;
    justify-content: space-between;
    gap: 8px;
  }
  .leaderboard li .lb-time { font-weight: 700; color: var(--ink); }
  .leaderboard li .lb-meta { color: var(--ink-soft); font-size: 11px; }
  .leaderboard .empty {
    font-family: var(--font-mono);
    font-size: 12px;
    color: var(--ink-soft);
  }

  .error-box {
    background: rgba(239,100,97,0.12);
    border: 1px solid rgba(239,100,97,0.4);
    color: #7a2422;
    border-radius: 10px;
    padding: 12px 14px;
    font-size: 13px;
    margin-top: 14px;
    text-align: center;
  }

  @media (max-width: 480px) {
    .panel { padding: 16px; }
    .result-grid { grid-template-columns: repeat(3, 1fr); }
  }
</style>
</head>
<body>

  <div class="brand">
    <p class="eyebrow">Photo Booth · Puzzle Ticket No. 001</p>
    <h1>Puzzle <span>Booth</span></h1>
    <p>Snap your face. Scramble it. Race the clock to put yourself back together.</p>
  </div>

  <div class="stage">

    <!-- CAMERA SCREEN -->
    <section id="screen-camera" class="screen active">
      <div class="panel">
        <div class="frame-wrap">
          <div class="corner-tick tl"></div>
          <div class="corner-tick tr"></div>
          <div class="corner-tick bl"></div>
          <div class="corner-tick br"></div>
          <video id="camVideo" autoplay playsinline muted></video>
          <canvas id="captureCanvas" style="display:none;"></canvas>
        </div>
        <p class="cam-status" id="camStatus">Requesting camera access…</p>
        <div id="camError"></div>
        <div class="btn-row">
          <button class="btn-primary" id="btnTakePhoto" disabled>📸 Take Photo</button>
          <label class="file-label" for="fileUpload">🖼️ Upload Photo</label>
          <input type="file" id="fileUpload" accept="image/*">
        </div>
        <div class="leaderboard" id="lobbyLeaderboard" style="margin-top:20px;"></div>
      </div>
    </section>

    <!-- PREVIEW / DIFFICULTY SCREEN -->
    <section id="screen-preview" class="screen">
      <div class="panel">
        <div class="frame-wrap">
          <div class="corner-tick tl"></div>
          <div class="corner-tick tr"></div>
          <div class="corner-tick bl"></div>
          <div class="corner-tick br"></div>
          <canvas id="previewCanvas"></canvas>
        </div>
        <div class="difficulty-select">
          <p class="label">Choose your difficulty</p>
          <div class="seg" id="difficultySeg">
            <button data-size="3" class="selected">3 × 3</button>
            <button data-size="4">4 × 4</button>
            <button data-size="5">5 × 5</button>
          </div>
        </div>
        <div class="btn-row">
          <button class="btn-ghost" id="btnRetake">↺ Retake Photo</button>
          <button class="btn-primary" id="btnStartPuzzle">Start Puzzle →</button>
        </div>
      </div>
    </section>

    <!-- PUZZLE SCREEN -->
    <section id="screen-puzzle" class="screen">
      <div class="ticket">
        <div class="ticket-stat">
          <span class="num" id="statTime">00:00.0</span>
          <span class="lbl">Time</span>
        </div>
        <div class="ticket-divider"></div>
        <div class="ticket-stat">
          <span class="num" id="statMoves">0</span>
          <span class="lbl">Moves</span>
        </div>
        <div class="ticket-divider"></div>
        <div class="ticket-stat">
          <span class="num" id="statCorrect">0 / 9</span>
          <span class="lbl">Placed</span>
        </div>
      </div>
      <div class="board-wrap">
        <div id="puzzleBoard"></div>
      </div>
      <div class="hint-toggle">
        <input type="checkbox" id="toggleNumbers" checked>
        <label for="toggleNumbers">Show position numbers</label>
      </div>
      <div class="puzzle-toolbar">
        <button class="btn-ghost" id="btnReshuffle">🔀 Reshuffle</button>
        <button class="btn-coral" id="btnNewPhotoFromPuzzle">🖼️ New Photo</button>
      </div>
    </section>

  </div>

  <!-- WIN OVERLAY -->
  <div class="overlay" id="winOverlay">
    <div class="overlay-panel">
      <p class="eyebrow">Solved!</p>
      <h2>Face Reassembled 🎉</h2>
      <div class="result-grid">
        <div><span class="num" id="resTime">00:00.0</span><span class="lbl">Time</span></div>
        <div><span class="num" id="resMoves">0</span><span class="lbl">Moves</span></div>
        <div><span class="num" id="resDiff">3×3</span><span class="lbl">Difficulty</span></div>
      </div>
      <div class="leaderboard" id="resultLeaderboard"></div>
      <div class="btn-row" style="margin-top:20px;">
        <button class="btn-ghost" id="btnPlayAgain">↺ Play Again</button>
        <button class="btn-primary" id="btnNewPhotoFromWin">🖼️ New Photo</button>
      </div>
    </div>
  </div>

<script>
(function(){
  "use strict";

  var LB_KEY = "facePuzzleLeaderboard";
  var OUT_SIZE = 640;

  var camVideo = document.getElementById("camVideo");
  var captureCanvas = document.getElementById("captureCanvas");
  var previewCanvas = document.getElementById("previewCanvas");
  var camStatus = document.getElementById("camStatus");
  var camError = document.getElementById("camError");
  var btnTakePhoto = document.getElementById("btnTakePhoto");
  var fileUpload = document.getElementById("fileUpload");

  var screenCamera = document.getElementById("screen-camera");
  var screenPreview = document.getElementById("screen-preview");
  var screenPuzzle = document.getElementById("screen-puzzle");

  var difficultySeg = document.getElementById("difficultySeg");
  var btnRetake = document.getElementById("btnRetake");
  var btnStartPuzzle = document.getElementById("btnStartPuzzle");

  var puzzleBoard = document.getElementById("puzzleBoard");
  var statTime = document.getElementById("statTime");
  var statMoves = document.getElementById("statMoves");
  var statCorrect = document.getElementById("statCorrect");
  var toggleNumbers = document.getElementById("toggleNumbers");
  var btnReshuffle = document.getElementById("btnReshuffle");
  var btnNewPhotoFromPuzzle = document.getElementById("btnNewPhotoFromPuzzle");

  var winOverlay = document.getElementById("winOverlay");
  var resTime = document.getElementById("resTime");
  var resMoves = document.getElementById("resMoves");
  var resDiff = document.getElementById("resDiff");
  var resultLeaderboard = document.getElementById("resultLeaderboard");
  var btnPlayAgain = document.getElementById("btnPlayAgain");
  var btnNewPhotoFromWin = document.getElementById("btnNewPhotoFromWin");

  var lobbyLeaderboard = document.getElementById("lobbyLeaderboard");

  var mediaStream = null;
  var capturedDataURL = null;
  var gridSize = 3;

  var tileEls = [];
  var tileAt = [];
  var slotOf = [];
  var movesCount = 0;
  var correctCount = 0;
  var startTime = 0;
  var timerInterval = null;
  var elapsedMs = 0;
  var puzzleActive = false;

  var dragTileId = null;
  var dragStartSlot = null;
  var ghostEl = null;
  var dragOffsetX = 0;
  var dragOffsetY = 0;
  var lastHoverEl = null;

  function showScreen(el){
    [screenCamera, screenPreview, screenPuzzle].forEach(function(s){
      s.classList.remove("active");
    });
    el.classList.add("active");
  }

  function initCamera(){
    if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia){
      camStatus.textContent = "Camera not supported on this browser.";
      showCamError("Your browser doesn't support camera access. You can still upload a photo instead.");
      return;
    }
    navigator.mediaDevices.getUserMedia({ video: { facingMode: "user", width: { ideal: 1280 }, height: { ideal: 1280 } }, audio: false })
      .then(function(stream){
        mediaStream = stream;
        camVideo.srcObject = stream;
        camStatus.textContent = "Camera live — center your face and smile.";
        btnTakePhoto.disabled = false;
      })
      .catch(function(err){
        var msg = "Camera access was denied or unavailable.";
        if (err && err.name === "NotAllowedError"){
          msg = "Camera permission denied. You can allow it in your browser settings, or upload a photo instead.";
        } else if (err && err.name === "NotFoundError"){
          msg = "No camera was found on this device. Upload a photo instead.";
        }
        camStatus.textContent = "Camera unavailable.";
        showCamError(msg);
      });
  }

  function showCamError(msg){
    camError.innerHTML = '<div class="error-box">' + msg + '</div>';
  }

  function cropVideoToCanvas(canvas){
    var vw = camVideo.videoWidth;
    var vh = camVideo.videoHeight;
    if (!vw || !vh) return false;
    var size = Math.min(vw, vh);
    var sx = (vw - size) / 2;
    var sy = (vh - size) / 2;
    canvas.width = OUT_SIZE;
    canvas.height = OUT_SIZE;
    var ctx = canvas.getContext("2d");
    ctx.save();
    ctx.translate(OUT_SIZE, 0);
    ctx.scale(-1, 1);
    ctx.drawImage(camVideo, sx, sy, size, size, 0, 0, OUT_SIZE, OUT_SIZE);
    ctx.restore();
    return true;
  }

  function cropImageToCanvas(img, canvas){
    var iw = img.naturalWidth || img.width;
    var ih = img.naturalHeight || img.height;
    var size = Math.min(iw, ih);
    var sx = (iw - size) / 2;
    var sy = (ih - size) / 2;
    canvas.width = OUT_SIZE;
    canvas.height = OUT_SIZE;
    var ctx = canvas.getContext("2d");
    ctx.drawImage(img, sx, sy, size, size, 0, 0, OUT_SIZE, OUT_SIZE);
  }

  btnTakePhoto.addEventListener("click", function(){
    if (!cropVideoToCanvas(captureCanvas)) return;
    capturedDataURL = captureCanvas.toDataURL("image/png");
    drawPreview();
    showScreen(screenPreview);
  });

  fileUpload.addEventListener("change", function(e){
    var file = e.target.files && e.target.files[0];
    if (!file) return;
    var reader = new FileReader();
    reader.onload = function(ev){
      var img = new Image();
      img.onload = function(){
        cropImageToCanvas(img, captureCanvas);
        capturedDataURL = captureCanvas.toDataURL("image/png");
        drawPreview();
        showScreen(screenPreview);
      };
      img.src = ev.target.result;
    };
    reader.readAsDataURL(file);
  });

  function drawPreview(){
    previewCanvas.width = OUT_SIZE;
    previewCanvas.height = OUT_SIZE;
    var ctx = previewCanvas.getContext("2d");
    var img = new Image();
    img.onload = function(){
      ctx.drawImage(img, 0, 0, OUT_SIZE, OUT_SIZE);
    };
    img.src = capturedDataURL;
  }

  btnRetake.addEventListener("click", function(){
    showScreen(screenCamera);
    if (mediaStream){
      camStatus.textContent = "Camera live — center your face and smile.";
    }
  });

  Array.prototype.forEach.call(difficultySeg.querySelectorAll("button"), function(btn){
    btn.addEventListener("click", function(){
      Array.prototype.forEach.call(difficultySeg.querySelectorAll("button"), function(b){
        b.classList.remove("selected");
      });
      btn.classList.add("selected");
      gridSize = parseInt(btn.getAttribute("data-size"), 10);
    });
  });

  btnStartPuzzle.addEventListener("click", function(){
    showScreen(screenPuzzle);
    buildPuzzle(gridSize, true);
  });

  function shuffledIndices(n){
    var arr = [];
    for (var i = 0; i < n; i++) arr.push(i);
    var isIdentity = true;
    do {
      for (var i2 = arr.length - 1; i2 > 0; i2--){
        var j = Math.floor(Math.random() * (i2 + 1));
        var tmp = arr[i2]; arr[i2] = arr[j]; arr[j] = tmp;
      }
      isIdentity = arr.every(function(v, idx){ return v === idx; });
    } while (isIdentity);
    return arr;
  }

  function buildPuzzle(size, resetTimer){
    gridSize = size;
    var n = size * size;
    puzzleBoard.innerHTML = "";
    puzzleBoard.style.gridTemplateColumns = "repeat(" + size + ", 1fr)";

    tileAt = shuffledIndices(n);
    slotOf = new Array(n);
    for (var s = 0; s < n; s++){ slotOf[tileAt[s]] = s; }

    tileEls = new Array(n);

    for (var tileId = 0; tileId < n; tileId++){
      var row = Math.floor(tileId / size);
      var col = tileId % size;
      var el = document.createElement("div");
      el.className = "tile";
      el.dataset.tileId = String(tileId);
      el.style.backgroundImage = "url(" + capturedDataURL + ")";
      el.style.backgroundSize = (size * 100) + "% " + (size * 100) + "%";
      el.style.backgroundPosition = (col / (size - 1) * 100) + "% " + (row / (size - 1) * 100) + "%";
      el.style.order = String(slotOf[tileId]);

      var badge = document.createElement("span");
      badge.className = "badge";
      badge.textContent = String(tileId + 1);
      badge.style.display = toggleNumbers.checked ? "block" : "none";
      el.appendChild(badge);

      el.addEventListener("pointerdown", makePointerDownHandler(tileId));
      puzzleBoard.appendChild(el);
      tileEls[tileId] = el;
    }

    movesCount = 0;
    updateCorrectHighlights();
    updateStatsDisplay();

    if (resetTimer){
      movesCount = 0;
    }
    startTimer();
    puzzleActive = true;
  }

  function updateCorrectHighlights(){
    var count = 0;
    for (var tileId = 0; tileId < tileEls.length; tileId++){
      var isCorrect = slotOf[tileId] === tileId;
      tileEls[tileId].classList.toggle("correct", isCorrect);
      if (isCorrect) count++;
    }
    correctCount = count;
  }

  function updateStatsDisplay(){
    statMoves.textContent = String(movesCount);
    statCorrect.textContent = correctCount + " / " + (gridSize * gridSize);
  }

  function startTimer(){
    stopTimer();
    startTime = Date.now();
    elapsedMs = 0;
    updateTimeDisplay();
    timerInterval = setInterval(function(){
      elapsedMs = Date.now() - startTime;
      updateTimeDisplay();
    }, 100);
  }

  function stopTimer(){
    if (timerInterval){
      clearInterval(timerInterval);
      timerInterval = null;
    }
  }

  function formatTime(ms){
    var totalTenths = Math.floor(ms / 100);
    var tenths = totalTenths % 10;
    var totalSeconds = Math.floor(totalTenths / 10);
    var seconds = totalSeconds % 60;
    var minutes = Math.floor(totalSeconds / 60);
    function pad(v){ return v < 10 ? "0" + v : String(v); }
    return pad(minutes) + ":" + pad(seconds) + "." + tenths;
  }

  function updateTimeDisplay(){
    statTime.textContent = formatTime(elapsedMs);
  }

  function swap(slotA, slotB){
    if (slotA === slotB) return;
    var tileA = tileAt[slotA];
    var tileB = tileAt[slotB];
    tileAt[slotA] = tileB;
    tileAt[slotB] = tileA;
    slotOf[tileA] = slotB;
    slotOf[tileB] = slotA;
    tileEls[tileA].style.order = String(slotB);
    tileEls[tileB].style.order = String(slotA);
    movesCount++;
    updateCorrectHighlights();
    updateStatsDisplay();
    checkWin();
  }

  function checkWin(){
    if (!puzzleActive) return;
    if (correctCount === gridSize * gridSize){
      puzzleActive = false;
      stopTimer();
      var finalMs = elapsedMs;
      var finalMoves = movesCount;
      var diffLabel = gridSize + "×" + gridSize;
      resTime.textContent = formatTime(finalMs);
      resMoves.textContent = String(finalMoves);
      resDiff.textContent = diffLabel;
      saveResult(finalMs, finalMoves, diffLabel);
      renderLeaderboard(resultLeaderboard);
      winOverlay.classList.add("active");
    }
  }

  function saveResult(ms, moves, diffLabel){
    var list = loadLeaderboard();
    list.push({
      date: new Date().toLocaleDateString(),
      timeMs: ms,
      timeLabel: formatTime(ms),
      moves: moves,
      difficulty: diffLabel
    });
    list.sort(function(a, b){ return a.timeMs - b.timeMs; });
    list = list.slice(0, 5);
    try {
      localStorage.setItem(LB_KEY, JSON.stringify(list));
    } catch (e){ /* storage unavailable, ignore */ }
  }

  function loadLeaderboard(){
    try {
      var raw = localStorage.getItem(LB_KEY);
      if (!raw) return [];
      var parsed = JSON.parse(raw);
      if (Array.isArray(parsed)) return parsed;
      return [];
    } catch (e){
      return [];
    }
  }

  function renderLeaderboard(container){
    var list = loadLeaderboard();
    var html = '<h3>Top 5 Best Times</h3>';
    if (list.length === 0){
      html += '<p class="empty">No times saved yet. Be the first to finish!</p>';
    } else {
      html += "<ol>";
      list.forEach(function(entry){
        html += "<li><span>" + entry.difficulty + " · <span class='lb-time'>" + entry.timeLabel + "</span></span>" +
                "<span class='lb-meta'>" + entry.moves + " moves · " + entry.date + "</span></li>";
      });
      html += "</ol>";
    }
    container.innerHTML = html;
  }

  function getPointerFromEvent(e){
    return { x: e.clientX, y: e.clientY };
  }

  function makePointerDownHandler(tileId){
    return function(e){
      if (!puzzleActive) return;
      e.preventDefault();
      dragTileId = tileId;
      dragStartSlot = slotOf[tileId];
      var el = tileEls[tileId];
      var rect = el.getBoundingClientRect();
      var pt = getPointerFromEvent(e);
      dragOffsetX = pt.x - rect.left;
      dragOffsetY = pt.y - rect.top;

      ghostEl = document.createElement("div");
      ghostEl.className = "tile tile-ghost";
      ghostEl.style.backgroundImage = el.style.backgroundImage;
      ghostEl.style.backgroundSize = el.style.backgroundSize;
      ghostEl.style.backgroundPosition = el.style.backgroundPosition;
      ghostEl.style.width = rect.width + "px";
      ghostEl.style.height = rect.height + "px";
      ghostEl.style.left = rect.left + "px";
      ghostEl.style.top = rect.top + "px";
      document.body.appendChild(ghostEl);

      el.classList.add("is-source");

      window.addEventListener("pointermove", onPointerMove);
      window.addEventListener("pointerup", onPointerUp);
    };
  }

  function onPointerMove(e){
    if (!ghostEl) return;
    var pt = getPointerFromEvent(e);
    ghostEl.style.left = (pt.x - dragOffsetX) + "px";
    ghostEl.style.top = (pt.y - dragOffsetY) + "px";

    ghostEl.style.pointerEvents = "none";
    var under = document.elementFromPoint(pt.x, pt.y);
    var hoverTile = under ? under.closest(".tile:not(.tile-ghost)") : null;

    if (lastHoverEl && lastHoverEl !== hoverTile){
      lastHoverEl.classList.remove("drop-hover");
    }
    if (hoverTile && hoverTile !== tileEls[dragTileId]){
      hoverTile.classList.add("drop-hover");
      lastHoverEl = hoverTile;
    } else {
      lastHoverEl = null;
    }
  }

  function onPointerUp(e){
    window.removeEventListener("pointermove", onPointerMove);
    window.removeEventListener("pointerup", onPointerUp);

    var pt = getPointerFromEvent(e);
    if (ghostEl){
      ghostEl.remove();
      ghostEl = null;
    }
    if (lastHoverEl){
      lastHoverEl.classList.remove("drop-hover");
      lastHoverEl = null;
    }

    var srcEl = tileEls[dragTileId];
    srcEl.classList.remove("is-source");

    var under = document.elementFromPoint(pt.x, pt.y);
    var targetTileEl = under ? under.closest(".tile") : null;

    if (targetTileEl && targetTileEl !== srcEl){
      var targetTileId = parseInt(targetTileEl.dataset.tileId, 10);
      var targetSlot = slotOf[targetTileId];
      swap(dragStartSlot, targetSlot);
    }

    dragTileId = null;
    dragStartSlot = null;
  }

  toggleNumbers.addEventListener("change", function(){
    var show = toggleNumbers.checked;
    Array.prototype.forEach.call(puzzleBoard.querySelectorAll(".badge"), function(b){
      b.style.display = show ? "block" : "none";
    });
  });

  btnReshuffle.addEventListener("click", function(){
    buildPuzzle(gridSize, true);
  });

  btnNewPhotoFromPuzzle.addEventListener("click", function(){
    stopTimer();
    puzzleActive = false;
    showScreen(screenCamera);
  });

  btnNewPhotoFromWin.addEventListener("click", function(){
    winOverlay.classList.remove("active");
    showScreen(screenCamera);
  });

  btnPlayAgain.addEventListener("click", function(){
    winOverlay.classList.remove("active");
    showScreen(screenPuzzle);
    buildPuzzle(gridSize, true);
  });

  renderLeaderboard(lobbyLeaderboard);
  initCamera();

})();
</script>
</body>
</html>

SCREENSHOTS:
<img width="1570" height="1032" alt="Screenshot 2026-07-16 114434" src="https://github.com/user-attachments/assets/1b63c6e7-3651-459d-b8da-6d07867450e0" />
<img width="1418" height="960" alt="Screenshot 2026-07-16 114457" src="https://github.com/user-attachments/assets/3a8d7f8b-a5ff-4be7-bbe4-cf20e3d894ae" />
<img width="817" height="756" alt="Screenshot 2026-07-16 114551" src="https://github.com/user-attachments/assets/beb1ce3d-a4ba-4b20-b064-7cf0a9fda325" />


