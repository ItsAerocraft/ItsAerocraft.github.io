<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Amogus</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0e0e10;
    --surface: #1a1a1e;
    --surface2: #232328;
    --border: #2e2e36;
    --accent: #e8c547;
    --accent2: #5bc8af;
    --red: #e85454;
    --green: #5bc87a;
    --purple: #a78bfa;
    --text: #f0eee6;
    --muted: #7a7a8a;
    --radius: 12px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Mono', monospace;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 32px 16px;
  }

  header {
    width: 100%;
    max-width: 680px;
    margin-bottom: 28px;
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    gap: 16px;
  }

  header h1 {
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    color: var(--accent);
    letter-spacing: 0.02em;
    line-height: 1;
  }

  header h1 span {
    font-size: 0.85rem;
    font-family: 'DM Mono', monospace;
    color: var(--muted);
    display: block;
    font-weight: 300;
    margin-top: 4px;
    letter-spacing: 0.08em;
  }

  .file-label {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 8px 14px;
    font-size: 0.75rem;
    color: var(--muted);
    cursor: pointer;
    transition: border-color 0.2s, color 0.2s;
    white-space: nowrap;
  }
  .file-label:hover { border-color: var(--accent); color: var(--accent); }
  #fileInput { display: none; }

  .controls-row {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    flex-wrap: wrap;
    justify-content: flex-end;
  }

  .small-btn {
    background: var(--surface2);
    color: var(--text);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 8px 10px;
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    cursor: pointer;
    transition: border-color 0.2s, color 0.2s;
  }
  .small-btn:hover { border-color: var(--accent); color: var(--accent); }

  /* 2-part mode toggle */
  #twoPartBtn {
    background: var(--surface2);
    color: var(--muted);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 8px 12px;
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    cursor: pointer;
    transition: border-color 0.2s, color 0.2s, background 0.2s;
    white-space: nowrap;
  }
  #twoPartBtn.active {
    background: #1e1530;
    border-color: var(--purple);
    color: var(--purple);
  }
  #twoPartBtn:hover { border-color: var(--purple); color: var(--purple); }

  .stats-bar {
    width: 100%;
    max-width: 680px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    margin-bottom: 24px;
  }

  .stat-box {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 12px 14px;
    text-align: center;
  }

  .stat-box .val {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem;
    color: var(--accent);
    line-height: 1;
  }
  .stat-box .lbl {
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-top: 4px;
  }

  .progress-wrap {
    width: 100%;
    max-width: 680px;
    margin-bottom: 24px;
  }
  .progress-track {
    height: 4px;
    background: var(--border);
    border-radius: 99px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent2), var(--accent));
    border-radius: 99px;
    transition: width 0.4s ease;
    width: 0%;
  }
  .progress-labels {
    display: flex;
    justify-content: space-between;
    font-size: 0.65rem;
    color: var(--muted);
    margin-top: 6px;
    letter-spacing: 0.08em;
  }

  .window-indicator {
    width: 100%;
    max-width: 680px;
    margin-bottom: 16px;
    font-size: 0.7rem;
    color: var(--muted);
    letter-spacing: 0.06em;
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .window-indicator .dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--accent2);
    display: inline-block;
    animation: pulse 1.6s infinite;
  }
  @keyframes pulse {
    0%,100%{ opacity:1; } 50%{ opacity:0.3; }
  }

  /* 2-part mode banner */
  .two-part-banner {
    width: 100%;
    max-width: 680px;
    margin-bottom: 12px;
    background: #1e1530;
    border: 1px solid var(--purple);
    border-radius: 8px;
    padding: 7px 14px;
    font-size: 0.72rem;
    color: var(--purple);
    letter-spacing: 0.07em;
    display: none;
    align-items: center;
    gap: 8px;
  }
  .two-part-banner.visible { display: flex; }

  #flashcard {
    width: 100%;
    max-width: 680px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 18px;
    padding: 36px 32px 28px;
    transition: background 0.35s, border-color 0.35s;
    position: relative;
    min-height: 200px;
  }

  #flashcard.correct { background: #1b2e21; border-color: var(--green); }
  #flashcard.wrong   { background: #2e1b1b; border-color: var(--red); }
  #flashcard.partial { background: #1e1530; border-color: var(--purple); }

  .word-badge {
    display: inline-block;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: 6px;
    font-size: 0.65rem;
    color: var(--muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 3px 8px;
    margin-bottom: 14px;
  }

  .phrase-text {
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    color: var(--text);
    margin-bottom: 24px;
    line-height: 1.2;
  }

  .lives-row {
    display: flex;
    gap: 6px;
    margin-bottom: 20px;
    align-items: center;
    font-size: 0.7rem;
    color: var(--muted);
    letter-spacing: 0.06em;
  }
  .life { font-size: 1rem; transition: opacity 0.3s; }
  .life.dead { opacity: 0.2; }

  .input-row {
    display: flex;
    gap: 10px;
    margin-bottom: 14px;
  }

  /* Two-part inputs layout */
  .two-part-inputs {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 14px;
  }

  .two-part-input-group {
    display: flex;
    gap: 10px;
    align-items: center;
  }

  .two-part-label {
    font-size: 0.68rem;
    color: var(--muted);
    letter-spacing: 0.08em;
    text-transform: uppercase;
    white-space: nowrap;
    min-width: 52px;
  }

  .part-status {
    font-size: 0.9rem;
    min-width: 20px;
    text-align: center;
  }

  input[type="text"] {
    flex: 1;
    background: var(--surface2);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 12px 16px;
    color: var(--text);
    font-family: 'DM Mono', monospace;
    font-size: 0.95rem;
    outline: none;
    transition: border-color 0.2s;
  }
  input[type="text"]:focus { border-color: var(--accent2); }
  input[type="text"].input-correct { border-color: var(--green); background: #1b2e21; }
  input[type="text"].input-wrong  { border-color: var(--red); }
  input[type="text"].input-purple { border-color: var(--purple); }

  .btn {
    background: var(--accent);
    color: #0e0e10;
    border: none;
    border-radius: var(--radius);
    padding: 12px 22px;
    font-family: 'DM Mono', monospace;
    font-size: 0.85rem;
    font-weight: 500;
    cursor: pointer;
    letter-spacing: 0.05em;
    transition: background 0.2s, transform 0.1s;
    white-space: nowrap;
  }
  .btn:hover { background: #f0d060; }
  .btn:active { transform: scale(0.97); }
  .btn.secondary {
    background: var(--surface2);
    color: var(--text);
    border: 1px solid var(--border);
  }
  .btn.secondary:hover { border-color: var(--accent); color: var(--accent); background: var(--surface2); }

  .answer-reveal {
    margin-top: 10px;
    padding: 12px 16px;
    background: #2e1b1b;
    border: 1px solid var(--red);
    border-radius: var(--radius);
    font-size: 0.9rem;
    color: #f0a0a0;
    letter-spacing: 0.04em;
  }
  .answer-reveal strong { color: var(--red); }

  /* partial reveal for 2-part */
  .answer-reveal.partial-reveal {
    background: #1e1530;
    border-color: var(--purple);
    color: #c4b5fd;
  }
  .answer-reveal.partial-reveal strong { color: var(--purple); }

  .feedback-msg {
    margin-top: 10px;
    font-size: 0.85rem;
    letter-spacing: 0.05em;
    min-height: 22px;
    transition: color 0.3s;
  }
  .feedback-msg.ok { color: var(--green); }
  .feedback-msg.bad { color: var(--red); }
  .feedback-msg.partial { color: var(--purple); }

  .card-actions {
    width: 100%;
    max-width: 680px;
    display: flex;
    gap: 10px;
    margin-top: 16px;
  }

  .table-wrap {
    width: 100%;
    max-width: 680px;
    margin-top: 24px;
    display: none;
    border: 1px solid var(--border);
    border-radius: var(--radius);
    overflow: hidden;
  }
  table { width: 100%; border-collapse: collapse; }
  thead { background: var(--surface2); }
  th { padding: 10px 14px; font-size: 0.7rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--muted); text-align: left; }
  td { padding: 10px 14px; font-size: 0.85rem; border-top: 1px solid var(--border); vertical-align: middle; }
  tr:hover td { background: var(--surface2); }
  .badge-lives {
    display: flex; gap: 4px;
  }
  .pip {
    width: 8px; height: 8px; border-radius: 50%;
    background: var(--border);
  }
  .pip.active { background: var(--accent2); }
  .pip.done { background: var(--green); }

  .empty-state {
    text-align: center;
    color: var(--muted);
    padding: 40px 0;
  }
  .empty-state .icon { font-size: 2.5rem; margin-bottom: 10px; }
  .empty-state p { font-size: 0.85rem; letter-spacing: 0.05em; }

  #completionScreen {
    display: none;
    width: 100%;
    max-width: 680px;
    background: var(--surface);
    border: 1px solid var(--accent);
    border-radius: 18px;
    padding: 48px 32px;
    text-align: center;
  }
  #completionScreen h2 {
    font-family: 'Playfair Display', serif;
    font-size: 2.2rem;
    color: var(--accent);
    margin-bottom: 10px;
  }
  #completionScreen p { color: var(--muted); font-size: 0.85rem; margin-bottom: 24px; }
</style>
</head>
<body>

<header>
  <h1>Flashcards<span>Choose # correct and mode</span></h1>

  <div class="controls-row">
    <label class="file-label" for="fileInput">
      ⬆ Upload .xlsx
      <input type="file" id="fileInput" accept=".xlsx">
    </label>

    <button id="randomiseBtn" class="small-btn" title="Shuffle card order">🔀 Randomise</button>

    <!-- 2-part mode toggle -->
    <button id="twoPartBtn" title="Require both parts of the definition (split by ; or /)">✦ 2-Part Mode</button>

    <div style="display:inline-flex; align-items:center; gap:6px; color:var(--muted); font-size:0.82rem;">
      <label style="display:inline-flex; align-items:center; gap:6px; color:var(--muted);">
        <input type="radio" name="repeatChoice" id="repeat1" value="1"> 1
      </label>
      <label style="display:inline-flex; align-items:center; gap:6px; color:var(--muted);">
        <input type="radio" name="repeatChoice" id="repeat5" value="5" checked> 5
      </label>
    </div>
  </div>
</header>

<div class="stats-bar">
  <div class="stat-box"><div class="val" id="statRemaining">—</div><div class="lbl">Remaining</div></div>
  <div class="stat-box"><div class="val" id="statDone">0</div><div class="lbl">Mastered</div></div>
  <div class="stat-box"><div class="val" id="statCorrect">0</div><div class="lbl">Correct</div></div>
  <div class="stat-box"><div class="val" id="statWrong">0</div><div class="lbl">Wrong</div></div>
</div>

<div class="progress-wrap">
  <div class="progress-track"><div class="progress-fill" id="progressFill"></div></div>
  <div class="progress-labels"><span id="progressLabel">Upload a file to begin</span><span id="progressPct"></span></div>
</div>

<div class="window-indicator" id="windowIndicator" style="display:none;">
  <span class="dot"></span>
  <span id="windowLabel">Window: cards 1–5</span>
</div>

<!-- 2-part mode banner -->
<div class="two-part-banner" id="twoPartBanner">
  ✦ 2-Part Mode active — definitions split by <code style="background:#2e2040;padding:1px 5px;border-radius:4px;">;</code> or <code style="background:#2e2040;padding:1px 5px;border-radius:4px;">/</code> — fill in both parts to score
</div>

<div id="flashcard">
  <div class="empty-state">
    <div class="icon">📂</div>
    <p>Upload your Excel file to start practising.<br>Each word needs 5 correct answers to be mastered.</p>
  </div>
</div>

<div id="completionScreen">
  <h2>Complete! 🎉</h2>
  <p>You've completed every word with the selected correct-count requirement each.</p>
  <button class="btn" onclick="restartAll()">Start Over</button>
</div>

<div class="card-actions" id="cardActions" style="display:none;">
  <button class="btn secondary" onclick="toggleWordList()">Word List</button>
  <button class="btn" onclick="startGame()">▶ Start / Restart</button>
</div>

<div class="table-wrap" id="tableWrap">
  <table id="wordListTable"></table>
</div>

<script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.0/dist/xlsx.full.min.js"></script>
<script>
  let REQUIRED_CORRECT = 5;
  const WINDOW_SIZE = 5;

  // 2-part mode state
  let twoPartMode = false;

  let allCards = [];
  let windowStart = 0;
  let currentCard = null;
  let wrongShown = false;
  let totalCorrect = 0;
  let totalWrong = 0;

  // For 2-part mode: track which parts have been correctly entered this attempt
  let part1Correct = false;
  let part2Correct = false;

  const fileInput = document.getElementById('fileInput');
  const flashcardDiv = document.getElementById('flashcard');
  const completionScreen = document.getElementById('completionScreen');
  const cardActions = document.getElementById('cardActions');
  const tableWrap = document.getElementById('tableWrap');
  const wordListTable = document.getElementById('wordListTable');
  const randomiseBtn = document.getElementById('randomiseBtn');
  const twoPartBtn = document.getElementById('twoPartBtn');
  const twoPartBanner = document.getElementById('twoPartBanner');
  const repeat1 = document.getElementById('repeat1');
  const repeat5 = document.getElementById('repeat5');

  fileInput.addEventListener('change', handleFile);
  randomiseBtn.addEventListener('click', handleRandomise);
  repeat1.addEventListener('change', onRepeatChange);
  repeat5.addEventListener('change', onRepeatChange);
  twoPartBtn.addEventListener('click', toggleTwoPartMode);

  // ── 2-Part Mode ──────────────────────────────────────────────
  function toggleTwoPartMode() {
    twoPartMode = !twoPartMode;
    twoPartBtn.classList.toggle('active', twoPartMode);
    twoPartBanner.classList.toggle('visible', twoPartMode);
    // Re-render current card if one is showing
    if (currentCard) {
      wrongShown = false;
      part1Correct = false;
      part2Correct = false;
      renderCard();
    }
  }

  /**
   * Split a definition into up to 2 parts using ; or / as delimiter.
   * Returns array of 1 or 2 trimmed strings.
   */
  function splitDefinition(def) {
    // Try semicolon first, then slash
    const bySemi = def.split(';');
    if (bySemi.length >= 2) {
      return [bySemi[0].trim(), bySemi.slice(1).join(';').trim()];
    }
    const bySlash = def.split('/');
    if (bySlash.length >= 2) {
      return [bySlash[0].trim(), bySlash.slice(1).join('/').trim()];
    }
    // No delimiter found — return as single part
    return [def.trim()];
  }

  function onRepeatChange() {
    const val = document.querySelector('input[name="repeatChoice"]:checked').value;
    REQUIRED_CORRECT = parseInt(val, 10) || 5;
    document.querySelector('h1 span').textContent = `IB German Flashcards • ${REQUIRED_CORRECT} correct = mastered`;
    renderWordList();
    updateStats();
  }

  // ── File handling ────────────────────────────────────────────
  function handleFile(e) {
    const file = e.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = function(ev) {
      const data = new Uint8Array(ev.target.result);
      const wb = XLSX.read(data, { type: 'array' });
      const sheet = wb.Sheets[wb.SheetNames[0]];
      const json = XLSX.utils.sheet_to_json(sheet, { header: 1 });
      buildCards(json);
      renderWordList();
      cardActions.style.display = 'flex';
      startGame();
    };
    reader.readAsArrayBuffer(file);
  }

  function buildCards(data) {
    allCards = [];
    windowStart = 0;
    totalCorrect = 0;
    totalWrong = 0;
    const rows = data.slice(1);
    let idCounter = 1;
    for (let row of rows) {
      if (row[0] && row[1]) {
        allCards.push({
          id: idCounter++,
          phrase: String(row[0]),
          definition: String(row[1]),
          correctCount: 0,
          done: false
        });
      }
    }
    updateStats();
  }

  function shuffleInPlace(arr) {
    for (let i = arr.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [arr[i], arr[j]] = [arr[j], arr[i]];
    }
  }

  function handleRandomise() {
    if (allCards.length === 0) return;
    shuffleInPlace(allCards);
    windowStart = 0;
    nextCard();
    renderWordList();
    updateStats();
    randomiseBtn.animate([{ transform: 'scale(1)' }, { transform: 'scale(1.04)' }, { transform: 'scale(1)' }], { duration: 220 });
  }

  // ── Game logic ───────────────────────────────────────────────
  function startGame() {
    if (allCards.length === 0) { alert('Upload an Excel file first (with columns: German, English).'); return; }
    windowStart = 0;
    allCards.forEach(c => { c.correctCount = 0; c.done = false; });
    totalCorrect = 0;
    totalWrong = 0;
    completionScreen.style.display = 'none';
    flashcardDiv.style.display = 'block';
    updateStats();
    nextCard();
  }

  function advanceWindow() {
    while (windowStart < allCards.length) {
      const end = Math.min(windowStart + WINDOW_SIZE, allCards.length);
      const windowSlice = allCards.slice(windowStart, end);
      const anyActive = windowSlice.some(c => !c.done);
      if (anyActive) break;
      windowStart += WINDOW_SIZE;
    }
  }

  function getActiveWindowCards() {
    advanceWindow();
    const end = Math.min(windowStart + WINDOW_SIZE, allCards.length);
    return allCards.slice(windowStart, end).filter(c => !c.done);
  }

  function nextCard() {
    const activePool = getActiveWindowCards();
    if (activePool.length === 0) {
      if (windowStart + WINDOW_SIZE < allCards.length) {
        windowStart += WINDOW_SIZE;
        nextCard();
      } else {
        if (allCards.every(c => c.done)) {
          showCompletion();
        } else {
          if (windowStart >= allCards.length) windowStart = 0;
          advanceWindow();
          nextCard();
        }
      }
      return;
    }
    const randomIndex = Math.floor(Math.random() * activePool.length);
    currentCard = activePool[randomIndex];
    wrongShown = false;
    part1Correct = false;
    part2Correct = false;
    renderCard();
    updateStats();
    updateWindowIndicator();
    renderWordList();
  }

  function renderCard() {
    if (!currentCard) return;
    const fc = flashcardDiv;
    fc.className = '';
    fc.style.display = 'block';

    const remainingAttempts = REQUIRED_CORRECT - currentCard.correctCount;
    const livesHtml = Array.from({ length: REQUIRED_CORRECT }, (_, i) => {
      const isCompleted = i < currentCard.correctCount;
      return `<span class="life${isCompleted ? ' dead' : ''}" style="opacity:${isCompleted ? 0.35 : 1}">★</span>`;
    }).join('');

    const parts = twoPartMode ? splitDefinition(currentCard.definition) : null;
    const isTrulyTwoPart = parts && parts.length === 2;

    let inputHtml;
    if (isTrulyTwoPart) {
      const p1Class = part1Correct ? 'input-correct' : '';
      const p2Class = part2Correct ? 'input-correct' : '';
      inputHtml = `
        <div class="two-part-inputs">
          <div class="two-part-input-group">
            <span class="two-part-label">Part 1</span>
            <input type="text" id="defGuess1" class="${p1Class}" placeholder="First part of definition…" autocomplete="off"
              ${part1Correct ? 'readonly' : ''}
              onkeydown="if(event.key==='Enter') checkAnswer()">
            <span class="part-status">${part1Correct ? '✓' : ''}</span>
          </div>
          <div class="two-part-input-group">
            <span class="two-part-label">Part 2</span>
            <input type="text" id="defGuess2" class="${p2Class}" placeholder="Second part of definition…" autocomplete="off"
              ${part2Correct ? 'readonly' : ''}
              onkeydown="if(event.key==='Enter') checkAnswer()">
            <span class="part-status">${part2Correct ? '✓' : ''}</span>
          </div>
        </div>
        <div style="display:flex; gap:10px; margin-bottom:14px;">
          <button class="btn" onclick="checkAnswer()">Check</button>
          <span style="font-size:0.72rem; color:var(--muted); align-self:center; letter-spacing:0.05em;">Both parts must be correct</span>
        </div>`;
    } else {
      // Normal single-input mode (or 2-part toggled but definition has no delimiter)
      inputHtml = `
        <div class="input-row">
          <input type="text" id="defGuess" placeholder="Enter definition…" autocomplete="off"
                 onkeydown="if(event.key==='Enter') checkAnswer()">
          <button class="btn" onclick="checkAnswer()">Check</button>
        </div>`;
    }

    const modeBadgeSuffix = isTrulyTwoPart ? ' · ✦ 2-part' : (twoPartMode ? ' · (no split found)' : '');

    fc.innerHTML = `
      <div class="word-badge">Word → Definition (${remainingAttempts} more correct to master${modeBadgeSuffix})</div>
      <div class="phrase-text">${escHtml(currentCard.phrase)}</div>
      <div class="lives-row">
        ${livesHtml}
        <span style="margin-left:8px">${currentCard.correctCount} / ${REQUIRED_CORRECT} correct</span>
      </div>
      ${inputHtml}
      <div class="feedback-msg" id="feedbackMsg"></div>
    `;

    // Focus first available input
    const firstInput = fc.querySelector('input[type="text"]:not([readonly])');
    if (firstInput) firstInput.focus();
  }

  function checkAnswer() {
    if (!currentCard) return;
    const fc = flashcardDiv;
    const msgDiv = document.getElementById('feedbackMsg');

    const parts = twoPartMode ? splitDefinition(currentCard.definition) : null;
    const isTrulyTwoPart = parts && parts.length === 2;

    if (isTrulyTwoPart) {
      // ── 2-part check ──
      const input1 = document.getElementById('defGuess1');
      const input2 = document.getElementById('defGuess2');
      if (!input1 || !input2) return;

      let changed = false;

      if (!part1Correct) {
        const val1 = input1.value.trim();
        if (val1.toLowerCase() === parts[0].toLowerCase()) {
          part1Correct = true;
          input1.classList.add('input-correct');
          input1.readOnly = true;
          changed = true;
        } else if (val1.length > 0) {
          input1.classList.add('input-wrong');
          setTimeout(() => input1.classList.remove('input-wrong'), 600);
        }
      }

      if (!part2Correct) {
        const val2 = input2.value.trim();
        if (val2.toLowerCase() === parts[1].toLowerCase()) {
          part2Correct = true;
          input2.classList.add('input-correct');
          input2.readOnly = true;
          changed = true;
        } else if (val2.length > 0) {
          input2.classList.add('input-wrong');
          setTimeout(() => input2.classList.remove('input-wrong'), 600);
        }
      }

      if (part1Correct && part2Correct) {
        // Both correct!
        totalCorrect++;
        if (currentCard.correctCount < REQUIRED_CORRECT) currentCard.correctCount++;
        if (currentCard.correctCount >= REQUIRED_CORRECT) currentCard.done = true;
        fc.className = 'correct';
        if (msgDiv) {
          msgDiv.className = 'feedback-msg ok';
          msgDiv.textContent = `✓ Both parts correct! (${currentCard.correctCount}/${REQUIRED_CORRECT} correct)`;
        }
        // Remove any reveal
        const existingReveal = fc.querySelector('.answer-reveal');
        if (existingReveal) existingReveal.remove();
        setTimeout(() => { fc.className = ''; nextCard(); }, 900);

      } else if (part1Correct || part2Correct) {
        // Partial
        fc.className = 'partial';
        const doneCount = (part1Correct ? 1 : 0) + (part2Correct ? 1 : 0);
        if (msgDiv) {
          msgDiv.className = 'feedback-msg partial';
          msgDiv.textContent = `✦ ${doneCount}/2 parts correct — keep going!`;
        }
        // Focus the remaining input
        if (!part1Correct && document.getElementById('defGuess1')) document.getElementById('defGuess1').focus();
        else if (!part2Correct && document.getElementById('defGuess2')) document.getElementById('defGuess2').focus();

      } else {
        // Both wrong
        totalWrong++;
        fc.className = 'wrong';
        if (msgDiv) {
          msgDiv.className = 'feedback-msg bad';
          msgDiv.textContent = `✗ Try again — both parts needed.`;
        }
        if (!wrongShown) {
          wrongShown = true;
          const reveal = document.createElement('div');
          reveal.className = 'answer-reveal partial-reveal';
          reveal.innerHTML = `<strong>Correct answers:</strong> Part 1: ${escHtml(parts[0])} &nbsp;|&nbsp; Part 2: ${escHtml(parts[1])}`;
          fc.appendChild(reveal);
          setTimeout(() => { if (reveal && reveal.parentNode) reveal.remove(); }, 2500);
        }
        setTimeout(() => { fc.className = part1Correct || part2Correct ? 'partial' : ''; }, 700);
      }

    } else {
      // ── Normal single-input check ──
      const input = document.getElementById('defGuess');
      if (!input) return;
      const userAnswer = input.value.trim();
      const correctAnswer = currentCard.definition;

      if (userAnswer.toLowerCase() === correctAnswer.toLowerCase()) {
        totalCorrect++;
        if (currentCard.correctCount < REQUIRED_CORRECT) currentCard.correctCount++;
        if (currentCard.correctCount >= REQUIRED_CORRECT) currentCard.done = true;
        fc.className = 'correct';
        if (msgDiv) {
          msgDiv.className = 'feedback-msg ok';
          msgDiv.textContent = `✓ Correct! (${currentCard.correctCount}/${REQUIRED_CORRECT} correct)`;
        }
        input.value = '';
        const existingReveal = fc.querySelector('.answer-reveal');
        if (existingReveal) existingReveal.remove();
        setTimeout(() => { fc.className = ''; nextCard(); }, 800);
      } else {
        totalWrong++;
        fc.className = 'wrong';
        if (msgDiv) {
          msgDiv.className = 'feedback-msg bad';
          msgDiv.textContent = `✗ Try again.`;
        }
        if (!wrongShown) {
          wrongShown = true;
          const reveal = document.createElement('div');
          reveal.className = 'answer-reveal';
          reveal.innerHTML = `<strong>Correct answer:</strong> ${escHtml(correctAnswer)}`;
          fc.appendChild(reveal);
          setTimeout(() => { if (reveal && reveal.parentNode) reveal.remove(); }, 2000);
        }
        input.value = '';
        setTimeout(() => { fc.className = ''; }, 700);
      }
    }

    updateStats();
    renderWordList();
  }

  // ── Stats & UI ───────────────────────────────────────────────
  function updateStats() {
    const remaining = allCards.filter(c => !c.done).length;
    const mastered = allCards.filter(c => c.done).length;
    const total = allCards.length;

    document.getElementById('statRemaining').textContent = total > 0 ? remaining : '—';
    document.getElementById('statDone').textContent = mastered;
    document.getElementById('statCorrect').textContent = totalCorrect;
    document.getElementById('statWrong').textContent = totalWrong;

    const pct = total > 0 ? Math.round((mastered / total) * 100) : 0;
    document.getElementById('progressFill').style.width = pct + '%';
    document.getElementById('progressLabel').textContent =
      total > 0 ? `${mastered} of ${total} mastered (${REQUIRED_CORRECT} correct each)` : 'Upload a file to begin';
    document.getElementById('progressPct').textContent = total > 0 ? pct + '%' : '';
  }

  function updateWindowIndicator() {
    const el = document.getElementById('windowIndicator');
    const lbl = document.getElementById('windowLabel');
    if (!el || !lbl) return;
    el.style.display = 'flex';
    const end = Math.min(windowStart + WINDOW_SIZE, allCards.length);
    lbl.textContent = `Active window: cards ${windowStart + 1}–${end} of ${allCards.length} (${REQUIRED_CORRECT} correct = mastered)`;
  }

  function showCompletion() {
    flashcardDiv.style.display = 'none';
    completionScreen.style.display = 'block';
    updateStats();
  }

  function restartAll() {
    allCards.forEach(c => { c.correctCount = 0; c.done = false; });
    windowStart = 0;
    totalCorrect = 0;
    totalWrong = 0;
    completionScreen.style.display = 'none';
    flashcardDiv.style.display = 'block';
    updateStats();
    nextCard();
  }

  function toggleWordList() {
    if (!tableWrap) return;
    tableWrap.style.display = tableWrap.style.display === 'none' ? 'block' : 'none';
  }

  function renderWordList() {
    if (!wordListTable) return;
    if (allCards.length === 0) { wordListTable.innerHTML = ''; return; }
    const rowsHtml = allCards.map((card, idx) => {
      const pips = [];
      for (let i = 0; i < REQUIRED_CORRECT; i++) {
        if (card.done) pips.push(`<span class="pip done"></span>`);
        else if (i < card.correctCount) pips.push(`<span class="pip active"></span>`);
        else pips.push(`<span class="pip"></span>`);
      }
      const pipContainer = `<div class="badge-lives">${pips.join('')}</div>`;
      const rowStyle = card.done ? 'opacity:0.5' : (currentCard === card ? 'background:var(--surface2)' : '');

      // Show definition with parts highlighted if 2-part mode
      const parts = splitDefinition(card.definition);
      let defDisplay = escHtml(card.definition);
      if (twoPartMode && parts.length === 2) {
        defDisplay = `<span style="color:var(--purple)">${escHtml(parts[0])}</span> <span style="color:var(--muted)">·</span> <span style="color:var(--accent2)">${escHtml(parts[1])}</span>`;
      }

      return `<tr style="${rowStyle}">
        <td style="color:var(--muted);font-size:0.7rem">${idx + 1}</td>
        <td style="font-weight:500;">${escHtml(card.phrase)}</td>
        <td style="color:var(--muted)">${defDisplay}</td>
        <td>${pipContainer} <span style="font-size:0.65rem; margin-left:6px;">${card.correctCount}/${REQUIRED_CORRECT}</span></td>
      </tr>`;
    }).join('');

    wordListTable.innerHTML = `
      <thead>
        <tr>
          <th>#</th>
          <th>Deutsch</th>
          <th>Definition${twoPartMode ? ' (Part 1 · Part 2)' : ''}</th>
          <th>Progress (${REQUIRED_CORRECT}✔️)</th>
        </tr>
      </thead>
      <tbody>${rowsHtml}</tbody>
    `;
  }

  function escHtml(str) {
    if (!str) return '';
    return str.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;').replace(/"/g, '&quot;');
  }

  window.checkAnswer = checkAnswer;
  window.startGame = startGame;
  window.toggleWordList = toggleWordList;
  window.restartAll = restartAll;

  document.addEventListener('DOMContentLoaded', () => {
    onRepeatChange();
  });
</script>
</body>
</html>
