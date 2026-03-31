<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
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

  .feedback-msg {
    margin-top: 10px;
    font-size: 0.85rem;
    letter-spacing: 0.05em;
    min-height: 22px;
    transition: color 0.3s;
  }
  .feedback-msg.ok { color: var(--green); }
  .feedback-msg.bad { color: var(--red); }

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
  .pip.miss { background: #5a3e3e; } /* neutral for attempts already used (inactive) */

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
  <h1>Deutsch Üben <span>IB German Flashcards • 5 correct = mastered</span></h1>
  <label class="file-label" for="fileInput">
    ⬆ Upload .xlsx
    <input type="file" id="fileInput" accept=".xlsx">
  </label>
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

<div id="flashcard">
  <div class="empty-state">
    <div class="icon">📂</div>
    <p>Upload your Excel file to start practising.<br>Each word needs 5 correct answers to be mastered.</p>
  </div>
</div>

<div id="completionScreen">
  <h2>Alle Karten gemeistert! 🎉</h2>
  <p>You've completed every word with 5 correct answers each.</p>
  <button class="btn" onclick="restartAll()">Start Over</button>
</div>

<div class="card-actions" id="cardActions" style="display:none;">
  <button class="btn secondary" onclick="toggleWordList()">Word List</button>
  <button class="btn" onclick="startGame()">▶ Start / Restart</button>
</div>

<div class="table-wrap" id="tableWrap">
  <table id="wordListTable"><table>
</div>

<script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.0/dist/xlsx.full.min.js"></script>
<script>
  // ─────────────────────────────────────────────────────────────
  // NEW CONFIG: 5 attempts (correct answers) required per word
  const REQUIRED_CORRECT = 5;   // each word must be answered correctly 5 times
  // ─────────────────────────────────────────────────────────────
  const WINDOW_SIZE = 5;

  // Global state
  let allCards = [];       // each: { phrase, definition, correctCount, done }
  let windowStart = 0;
  let currentCard = null;
  let wrongShown = false;  // track if we already displayed correct answer for current wrong attempt
  let totalCorrect = 0;     // total correct inputs across game (session)
  let totalWrong = 0;       // total wrong inputs

  // DOM elements
  const fileInput = document.getElementById('fileInput');
  const flashcardDiv = document.getElementById('flashcard');
  const completionScreen = document.getElementById('completionScreen');
  const cardActions = document.getElementById('cardActions');
  const tableWrap = document.getElementById('tableWrap');
  const wordListTable = document.getElementById('wordListTable');

  // ── File handling ────────────────────────────────────────────
  fileInput.addEventListener('change', handleFile);

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
    for (let row of rows) {
      if (row[0] && row[1]) {
        allCards.push({
          phrase: String(row[0]),
          definition: String(row[1]),
          correctCount: 0,     // number of times answered correctly (max REQUIRED_CORRECT)
          done: false
        });
      }
    }
    updateStats();
  }

  // ── Game logic ───────────────────────────────────────────────
  function startGame() {
    if (allCards.length === 0) { alert('Upload an Excel file first (with columns: German, English).'); return; }
    windowStart = 0;
    // Reset all cards: correctCount = 0, done = false
    allCards.forEach(c => { c.correctCount = 0; c.done = false; });
    totalCorrect = 0;
    totalWrong = 0;
    completionScreen.style.display = 'none';
    flashcardDiv.style.display = 'block';
    updateStats();
    nextCard();
  }

  // Advances windowStart so it points to a block that has at least one active (non-done) card
  function advanceWindow() {
    while (windowStart < allCards.length) {
      const end = Math.min(windowStart + WINDOW_SIZE, allCards.length);
      const windowSlice = allCards.slice(windowStart, end);
      const anyActive = windowSlice.some(c => !c.done);
      if (anyActive) break;
      windowStart += WINDOW_SIZE;
    }
  }

  // Returns array of active (not done) cards within current sliding window
  function getActiveWindowCards() {
    advanceWindow();
    const end = Math.min(windowStart + WINDOW_SIZE, allCards.length);
    return allCards.slice(windowStart, end).filter(c => !c.done);
  }

  function nextCard() {
    const activePool = getActiveWindowCards();
    if (activePool.length === 0) {
      // no active cards in current window -> move to next window if possible
      if (windowStart + WINDOW_SIZE < allCards.length) {
        windowStart += WINDOW_SIZE;
        nextCard();
      } else {
        // check if all cards globally are done
        if (allCards.every(c => c.done)) {
          showCompletion();
        } else {
          // fallback: restart from first window? but it should not happen: ensure loop
          if (windowStart >= allCards.length) windowStart = 0;
          advanceWindow();
          nextCard();
        }
      }
      return;
    }
    // pick random active card from window
    const randomIndex = Math.floor(Math.random() * activePool.length);
    currentCard = activePool[randomIndex];
    wrongShown = false;
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
    // visual indicator: show how many correct answers still needed
    const livesHtml = Array.from({ length: REQUIRED_CORRECT }, (_, i) => {
      const isCompleted = i < currentCard.correctCount;
      // completed steps look "filled" (greenish), remaining steps as empty outline style
      return `<span class="life${!isCompleted ? '' : ' dead'}" style="opacity: ${isCompleted ? 0.35 : 1};">★</span>`;
    }).join('');

    fc.innerHTML = `
      <div class="word-badge">Deutsch → Englisch (${remainingAttempts} more correct to master)</div>
      <div class="phrase-text">${escHtml(currentCard.phrase)}</div>
      <div class="lives-row">
        ${livesHtml}
        <span style="margin-left:8px">${currentCard.correctCount} / ${REQUIRED_CORRECT} correct</span>
      </div>
      <div class="input-row">
        <input type="text" id="defGuess" placeholder="Enter definition…" autocomplete="off"
               onkeydown="if(event.key==='Enter') checkAnswer()">
        <button class="btn" onclick="checkAnswer()">Check</button>
      </div>
      <div class="feedback-msg" id="feedbackMsg"></div>
    `;
    const inputField = document.getElementById('defGuess');
    if (inputField) inputField.focus();
  }

  function checkAnswer() {
    if (!currentCard) return;
    const input = document.getElementById('defGuess');
    if (!input) return;
    const userAnswer = input.value.trim();
    const correctAnswer = currentCard.definition;
    const fc = flashcardDiv;
    const msgDiv = document.getElementById('feedbackMsg');

    if (userAnswer.toLowerCase() === correctAnswer.toLowerCase()) {
      // CORRECT
      totalCorrect++;
      // Increase correct count for this card, but not beyond REQUIRED_CORRECT
      if (currentCard.correctCount < REQUIRED_CORRECT) {
        currentCard.correctCount++;
      }
      // If card reached REQUIRED_CORRECT correct answers -> mark as done
      if (currentCard.correctCount >= REQUIRED_CORRECT) {
        currentCard.done = true;
      }
      fc.className = 'correct';
      if (msgDiv) {
        msgDiv.className = 'feedback-msg ok';
        msgDiv.textContent = `✓ Richtig! (${currentCard.correctCount}/${REQUIRED_CORRECT} correct)`;
      }
      input.value = '';
      // clear any extra reveal if exists
      const existingReveal = fc.querySelector('.answer-reveal');
      if (existingReveal) existingReveal.remove();
      setTimeout(() => {
        fc.className = '';
        nextCard();
      }, 800);
    } else {
      // WRONG answer
      totalWrong++;
      fc.className = 'wrong';
      if (msgDiv) {
        msgDiv.className = 'feedback-msg bad';
        msgDiv.textContent = `✗ Falsch. Try again.`;
      }
      // Show correct answer only once per wrong attempt (like original design)
      if (!wrongShown) {
        wrongShown = true;
        const reveal = document.createElement('div');
        reveal.className = 'answer-reveal';
        reveal.innerHTML = `<strong>Correct answer:</strong> ${escHtml(correctAnswer)}`;
        fc.appendChild(reveal);
        // auto-clean after timeout so it disappears when next card loads or after 2 sec
        setTimeout(() => {
          if (reveal && reveal.parentNode) reveal.remove();
        }, 2000);
      }
      // No deduction of progress: wrong answers do NOT decrease correctCount.
      input.value = '';
      setTimeout(() => { fc.className = ''; }, 700);
    }
    updateStats();
    renderWordList(); // update progress pips in word list
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

  // ── Word list table (shows progress per card as 5 circles) ──
  function toggleWordList() {
    if (!tableWrap) return;
    tableWrap.style.display = tableWrap.style.display === 'none' ? 'block' : 'none';
  }

  function renderWordList() {
    if (!wordListTable) return;
    if (allCards.length === 0) { wordListTable.innerHTML = ''; return; }
    const rowsHtml = allCards.map((card, idx) => {
      // Generate REQUIRED_CORRECT circles (pips) representing correct answers achieved
      const pips = [];
      for (let i = 0; i < REQUIRED_CORRECT; i++) {
        if (card.done) {
          pips.push(`<span class="pip done" title="mastered"></span>`);
        } else if (i < card.correctCount) {
          pips.push(`<span class="pip active" title="correct answer achieved"></span>`);
        } else {
          pips.push(`<span class="pip" title="remaining correct needed"></span>`);
        }
      }
      const pipContainer = `<div class="badge-lives">${pips.join('')}</div>`;
      const rowStyle = card.done ? 'opacity:0.5' : (currentCard === card ? 'background:var(--surface2)' : '');
      return `<tr style="${rowStyle}">
        <td style="color:var(--muted);font-size:0.7rem">${idx + 1}</td>
        <td style="font-weight:500;">${escHtml(card.phrase)}</td>
        <td style="color:var(--muted)">${escHtml(card.definition)}</td>
        <td>${pipContainer} <span style="font-size:0.65rem; margin-left:6px;">${card.correctCount}/${REQUIRED_CORRECT}</span></td>
      </tr>`;
    }).join('');

    wordListTable.innerHTML = `
      <thead>
        <tr>
          <th>#</th>
          <th>Deutsch</th>
          <th>Definition</th>
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

  // expose needed functions to global for inline onclick
  window.checkAnswer = checkAnswer;
  window.startGame = startGame;
  window.toggleWordList = toggleWordList;
  window.restartAll = restartAll;
</script>
</body>
</html>
