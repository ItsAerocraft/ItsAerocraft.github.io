<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dietz</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&family=DM+Sans:wght@300;400;500;600&family=Playfair+Display:wght@400;700&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  /* ── Nav ─────────────────────────────────────────────── */
  :root {
    --bg: #0e0e10;
    --surface: #16161a;
    --surface2: #1e1e24;
    --border: rgba(255,255,255,0.08);
    --border-strong: rgba(255,255,255,0.15);
    --text: #f0eff4;
    --muted: rgba(240,239,244,0.45);
    --accent: #c3dee8;
    --accent-dim: rgba(195,222,232,0.12);
    --accent-dim2: rgba(195,222,232,0.06);
    --red: #ff6b6b;
    --red-dim: rgba(255,107,107,0.12);
    --radius: 12px;
    --radius-sm: 8px;
    /* flashcard vars */
    --fc-accent: #e8c547;
    --fc-accent2: #5bc8af;
    --fc-green: #5bc87a;
    --fc-purple: #a78bfa;
    --fc-surface: #1a1a1e;
    --fc-surface2: #232328;
    --fc-border: #2e2e36;
    --fc-red: #e85454;
    --fc-muted: #7a7a8a;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    min-height: 100vh;
  }

  /* ── Tab Nav ──────────────────────────────────────────── */
  .app-nav {
    display: flex;
    align-items: center;
    gap: 0;
    background: var(--surface);
    border-bottom: 0.5px solid var(--border-strong);
    padding: 0 1.5rem;
    position: sticky;
    top: 0;
    z-index: 50;
  }

  .nav-brand {
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    color: var(--muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 1rem 1.25rem 1rem 0;
    border-right: 0.5px solid var(--border-strong);
    margin-right: 1rem;
    white-space: nowrap;
  }

  .nav-tab {
    background: transparent;
    border: none;
    border-bottom: 2px solid transparent;
    color: var(--muted);
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 1rem 1rem;
    cursor: pointer;
    transition: all 0.15s;
    white-space: nowrap;
    margin-bottom: -0.5px;
  }
  .nav-tab:hover { color: var(--text); }
  .nav-tab.active {
    color: var(--accent);
    border-bottom-color: var(--accent);
  }

  /* ── Pages ────────────────────────────────────────────── */
  .page { display: none; }
  .page.active { display: block; }

  /* ════════════════════════════════════════════════════════
     REVISION TRACKER PAGE
  ════════════════════════════════════════════════════════ */
  #page-tracker {
    padding: 2rem 1.5rem 4rem;
  }

  .mono { font-family: 'Space Mono', monospace; }

  .tracker-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 2.5rem;
    flex-wrap: wrap;
    gap: 1rem;
  }

  .header-left h1 { font-size: 1.6rem; font-weight: 600; letter-spacing: -0.02em; }
  .header-left p { font-size: 0.85rem; color: var(--muted); margin-top: 4px; font-family: 'Space Mono', monospace; }

  .header-btns { display: flex; gap: 0.5rem; flex-wrap: wrap; }

  .config-btn {
    background: var(--surface2);
    border: 0.5px solid var(--border-strong);
    color: var(--muted);
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    padding: 8px 14px;
    border-radius: var(--radius-sm);
    cursor: pointer;
    transition: all 0.15s;
    letter-spacing: 0.04em;
  }
  .config-btn:hover { color: var(--text); border-color: var(--accent); }

  .copy-btn {
    background: var(--accent-dim);
    border: 0.5px solid rgba(195,222,232,0.3);
    color: var(--accent);
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    padding: 8px 14px;
    border-radius: var(--radius-sm);
    cursor: pointer;
    transition: all 0.15s;
    letter-spacing: 0.04em;
    display: flex;
    align-items: center;
    gap: 6px;
  }
  .copy-btn:hover { background: rgba(195,222,232,0.2); }
  .copy-btn.copied {
    background: rgba(91,200,122,0.15);
    border-color: rgba(91,200,122,0.4);
    color: #5bc87a;
  }

  .today-total {
    background: var(--accent-dim2);
    border: 0.5px solid rgba(195,222,232,0.2);
    border-radius: var(--radius);
    padding: 1rem 1.5rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 2rem;
    flex-wrap: wrap;
    gap: 0.5rem;
  }
  .today-total span:first-child { font-size: 0.8rem; color: var(--muted); font-family: 'Space Mono', monospace; letter-spacing: 0.06em; text-transform: uppercase; }
  .total-time { font-family: 'Space Mono', monospace; font-size: 1.5rem; color: var(--accent); font-weight: 700; }

  .status-bar {
    background: var(--surface);
    border: 0.5px solid var(--border);
    border-radius: var(--radius-sm);
    padding: 0.75rem 1.25rem;
    display: flex;
    align-items: center;
    gap: 0.75rem;
    margin-bottom: 1.5rem;
    font-size: 0.8rem;
    color: var(--muted);
    font-family: 'Space Mono', monospace;
  }
  .status-dot { width: 7px; height: 7px; border-radius: 50%; background: var(--muted); flex-shrink: 0; transition: background 0.3s; }
  .status-dot.ok { background: var(--accent); box-shadow: 0 0 6px var(--accent); }
  .status-dot.err { background: var(--red); }
  .status-dot.loading { background: #aaa; animation: pulse 1s infinite; }
  @keyframes pulse { 0%,100%{opacity:1} 50%{opacity:0.3} }

  .section-label { font-size: 0.7rem; font-family: 'Space Mono', monospace; letter-spacing: 0.1em; text-transform: uppercase; color: var(--muted); margin-bottom: 0.75rem; padding-left: 2px; }

  .subjects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1rem;
    margin-bottom: 2rem;
  }

  .subject-card {
    background: var(--surface);
    border: 0.5px solid var(--border);
    border-radius: var(--radius);
    padding: 1.25rem 1.5rem;
    transition: border-color 0.2s;
    position: relative;
    overflow: hidden;
  }
  .subject-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: var(--subject-color, transparent);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .subject-card.active::before { opacity: 1; }
  .subject-card.active { border-color: var(--subject-color, var(--accent)); background: var(--surface2); }

  .subject-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 1rem; gap: 0.5rem; }
  .subject-name { font-size: 1rem; font-weight: 500; color: var(--text); }

  .btn-edit-subject {
    background: transparent;
    border: none;
    color: var(--muted);
    cursor: pointer;
    font-size: 0.75rem;
    padding: 2px 6px;
    border-radius: 4px;
    transition: color 0.15s;
    flex-shrink: 0;
  }
  .btn-edit-subject:hover { color: var(--text); }

  .timer-display {
    font-family: 'Space Mono', monospace;
    font-size: 2rem;
    font-weight: 700;
    color: var(--muted);
    margin-bottom: 1rem;
    letter-spacing: 0.05em;
    transition: color 0.2s;
  }
  .subject-card.active .timer-display { color: var(--subject-color, var(--accent)); }

  .session-info { font-size: 0.75rem; color: var(--muted); margin-bottom: 1rem; font-family: 'Space Mono', monospace; }

  .card-footer { display: flex; gap: 0.5rem; align-items: center; }

  .btn-timer {
    flex: 1;
    padding: 10px;
    border-radius: var(--radius-sm);
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem;
    font-weight: 700;
    letter-spacing: 0.06em;
    cursor: pointer;
    border: 0.5px solid var(--border-strong);
    transition: all 0.15s;
    text-transform: uppercase;
  }
  .btn-start { background: var(--accent-dim); color: var(--accent); border-color: rgba(195,222,232,0.3); }
  .btn-start:hover { background: rgba(195,222,232,0.2); }
  .btn-stop { background: var(--red-dim); color: var(--red); border-color: rgba(255,107,107,0.3); }
  .btn-stop:hover { background: rgba(255,107,107,0.2); }

  .btn-log {
    padding: 10px 14px;
    background: transparent;
    border: 0.5px solid var(--border-strong);
    border-radius: var(--radius-sm);
    color: var(--muted);
    font-family: 'Space Mono', monospace;
    font-size: 0.72rem;
    cursor: pointer;
    transition: all 0.15s;
    text-transform: uppercase;
    letter-spacing: 0.04em;
  }
  .btn-log:hover { color: var(--text); }
  .btn-log:disabled { opacity: 0.3; cursor: not-allowed; }

  /* Modals */
  .modal-overlay {
    display: none;
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.75);
    z-index: 100;
    align-items: center;
    justify-content: center;
    padding: 1rem;
  }
  .modal-overlay.open { display: flex; }

  .modal {
    background: var(--surface);
    border: 0.5px solid var(--border-strong);
    border-radius: var(--radius);
    padding: 1.75rem;
    width: 100%;
    max-width: 480px;
    max-height: 90vh;
    overflow-y: auto;
  }
  .modal h2 { font-size: 1rem; font-weight: 600; margin-bottom: 1.25rem; font-family: 'Space Mono', monospace; color: var(--text); letter-spacing: -0.01em; }

  .field { margin-bottom: 1rem; }
  .field label { display: block; font-size: 0.75rem; color: var(--muted); margin-bottom: 6px; font-family: 'Space Mono', monospace; letter-spacing: 0.04em; text-transform: uppercase; }
  .field input {
    width: 100%;
    background: var(--bg);
    border: 0.5px solid var(--border-strong);
    border-radius: var(--radius-sm);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    font-size: 0.82rem;
    padding: 10px 12px;
    outline: none;
    transition: border-color 0.15s;
  }
  .field input:focus { border-color: var(--accent); }

  .modal-note {
    font-size: 0.75rem;
    color: var(--muted);
    line-height: 1.6;
    margin-bottom: 1.25rem;
    padding: 0.75rem;
    background: var(--surface2);
    border-radius: var(--radius-sm);
    border-left: 2px solid rgba(195,222,232,0.4);
  }

  .modal-footer { display: flex; gap: 0.5rem; margin-top: 1.25rem; }

  .btn-save {
    flex: 1;
    background: var(--accent-dim);
    border: 0.5px solid rgba(195,222,232,0.4);
    color: var(--accent);
    font-family: 'Space Mono', monospace;
    font-size: 0.78rem;
    font-weight: 700;
    padding: 10px;
    border-radius: var(--radius-sm);
    cursor: pointer;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    transition: all 0.15s;
  }
  .btn-save:hover { background: rgba(195,222,232,0.22); }

  .btn-cancel {
    background: transparent;
    border: 0.5px solid var(--border-strong);
    color: var(--muted);
    font-family: 'Space Mono', monospace;
    font-size: 0.78rem;
    padding: 10px 18px;
    border-radius: var(--radius-sm);
    cursor: pointer;
    text-transform: uppercase;
    letter-spacing: 0.04em;
    transition: all 0.15s;
  }
  .btn-cancel:hover { color: var(--text); }

  .subject-list { display: flex; flex-direction: column; gap: 0.5rem; margin-bottom: 1.25rem; }

  .subject-list-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    background: var(--bg);
    border: 0.5px solid var(--border-strong);
    border-radius: var(--radius-sm);
    padding: 8px 10px;
  }

  .subject-list-item input {
    flex: 1;
    background: transparent;
    border: none;
    color: var(--text);
    font-family: 'Space Mono', monospace;
    font-size: 0.82rem;
    outline: none;
    padding: 2px 4px;
  }

  .color-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }

  .btn-delete {
    background: transparent;
    border: none;
    color: var(--muted);
    cursor: pointer;
    font-size: 0.9rem;
    padding: 2px 4px;
    transition: color 0.15s;
    line-height: 1;
  }
  .btn-delete:hover { color: var(--red); }

  .btn-add-subject {
    width: 100%;
    background: transparent;
    border: 0.5px dashed var(--border-strong);
    color: var(--muted);
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem;
    padding: 10px;
    border-radius: var(--radius-sm);
    cursor: pointer;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    transition: all 0.15s;
    margin-bottom: 1rem;
  }
  .btn-add-subject:hover { color: var(--accent); border-color: rgba(195,222,232,0.4); }

  .log-list { max-height: 200px; overflow-y: auto; border: 0.5px solid var(--border); border-radius: var(--radius-sm); margin-top: 1.5rem; }
  .log-item { display: flex; justify-content: space-between; padding: 8px 12px; font-size: 0.72rem; font-family: 'Space Mono', monospace; border-bottom: 0.5px solid var(--border); color: var(--muted); }
  .log-item:last-child { border-bottom: none; }
  .log-item strong { color: var(--text); }

  .toast {
    position: fixed;
    bottom: 1.5rem;
    right: 1.5rem;
    background: var(--surface2);
    border: 0.5px solid var(--border-strong);
    border-radius: var(--radius-sm);
    padding: 10px 16px;
    font-family: 'Space Mono', monospace;
    font-size: 0.75rem;
    color: var(--text);
    z-index: 200;
    opacity: 0;
    transform: translateY(8px);
    transition: all 0.2s;
    pointer-events: none;
    max-width: 280px;
  }
  .toast.show { opacity: 1; transform: translateY(0); }
  .toast.success { border-color: rgba(195,222,232,0.4); color: var(--accent); }
  .toast.error { border-color: rgba(255,107,107,0.4); color: var(--red); }

  /* ════════════════════════════════════════════════════════
     FLASHCARD PAGE
  ════════════════════════════════════════════════════════ */
  #page-flashcard {
    font-family: 'DM Mono', monospace;
    display: none;
    flex-direction: column;
    align-items: center;
    padding: 32px 16px 64px;
  }
  #page-flashcard.active { display: flex; }

  .fc-header {
    width: 100%;
    max-width: 680px;
    margin-bottom: 28px;
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    gap: 16px;
  }

  .fc-header h1 {
    font-family: 'Playfair Display', serif;
    font-size: 2rem;
    color: var(--fc-accent);
    letter-spacing: 0.02em;
    line-height: 1;
  }

  .fc-header h1 span {
    font-size: 0.85rem;
    font-family: 'DM Mono', monospace;
    color: var(--fc-muted);
    display: block;
    font-weight: 300;
    margin-top: 4px;
    letter-spacing: 0.08em;
  }

  .file-label {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: var(--fc-surface2);
    border: 1px solid var(--fc-border);
    border-radius: var(--radius);
    padding: 8px 14px;
    font-size: 0.75rem;
    color: var(--fc-muted);
    cursor: pointer;
    transition: border-color 0.2s, color 0.2s;
    white-space: nowrap;
  }
  .file-label:hover { border-color: var(--fc-accent); color: var(--fc-accent); }
  #fileInput { display: none; }

  .controls-row {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    flex-wrap: wrap;
    justify-content: flex-end;
  }

  .small-btn {
    background: var(--fc-surface2);
    color: var(--text);
    border: 1px solid var(--fc-border);
    border-radius: 10px;
    padding: 8px 10px;
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    cursor: pointer;
    transition: border-color 0.2s, color 0.2s;
  }
  .small-btn:hover { border-color: var(--fc-accent); color: var(--fc-accent); }

  #twoPartBtn {
    background: var(--fc-surface2);
    color: var(--fc-muted);
    border: 1px solid var(--fc-border);
    border-radius: 10px;
    padding: 8px 12px;
    font-family: 'DM Mono', monospace;
    font-size: 0.8rem;
    cursor: pointer;
    transition: border-color 0.2s, color 0.2s, background 0.2s;
    white-space: nowrap;
  }
  #twoPartBtn.active { background: #1e1530; border-color: var(--fc-purple); color: var(--fc-purple); }
  #twoPartBtn:hover { border-color: var(--fc-purple); color: var(--fc-purple); }

  .stats-bar {
    width: 100%;
    max-width: 680px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
    margin-bottom: 24px;
  }

  .stat-box {
    background: var(--fc-surface);
    border: 1px solid var(--fc-border);
    border-radius: var(--radius);
    padding: 12px 14px;
    text-align: center;
  }

  .stat-box .val {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem;
    color: var(--fc-accent);
    line-height: 1;
  }
  .stat-box .lbl {
    font-size: 0.65rem;
    color: var(--fc-muted);
    letter-spacing: 0.1em;
    text-transform: uppercase;
    margin-top: 4px;
  }

  .progress-wrap { width: 100%; max-width: 680px; margin-bottom: 24px; }
  .progress-track { height: 4px; background: var(--fc-border); border-radius: 99px; overflow: hidden; }
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--fc-accent2), var(--fc-accent));
    border-radius: 99px;
    transition: width 0.4s ease;
    width: 0%;
  }
  .progress-labels { display: flex; justify-content: space-between; font-size: 0.65rem; color: var(--fc-muted); margin-top: 6px; letter-spacing: 0.08em; }

  .window-indicator {
    width: 100%;
    max-width: 680px;
    margin-bottom: 16px;
    font-size: 0.7rem;
    color: var(--fc-muted);
    letter-spacing: 0.06em;
    display: flex;
    align-items: center;
    gap: 8px;
  }
  .window-indicator .dot {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: var(--fc-accent2);
    display: inline-block;
    animation: fc-pulse 1.6s infinite;
  }
  @keyframes fc-pulse { 0%,100%{ opacity:1; } 50%{ opacity:0.3; } }

  .two-part-banner {
    width: 100%;
    max-width: 680px;
    margin-bottom: 12px;
    background: #1e1530;
    border: 1px solid var(--fc-purple);
    border-radius: 8px;
    padding: 7px 14px;
    font-size: 0.72rem;
    color: var(--fc-purple);
    letter-spacing: 0.07em;
    display: none;
    align-items: center;
    gap: 8px;
  }
  .two-part-banner.visible { display: flex; }

  #flashcard {
    width: 100%;
    max-width: 680px;
    background: var(--fc-surface);
    border: 1px solid var(--fc-border);
    border-radius: 18px;
    padding: 36px 32px 28px;
    transition: background 0.35s, border-color 0.35s;
    position: relative;
    min-height: 200px;
  }
  #flashcard.correct { background: #1b2e21; border-color: var(--fc-green); }
  #flashcard.wrong   { background: #2e1b1b; border-color: var(--fc-red); }
  #flashcard.partial { background: #1e1530; border-color: var(--fc-purple); }

  .word-badge {
    display: inline-block;
    background: var(--fc-surface2);
    border: 1px solid var(--fc-border);
    border-radius: 6px;
    font-size: 0.65rem;
    color: var(--fc-muted);
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
    color: var(--fc-muted);
    letter-spacing: 0.06em;
  }
  .life { font-size: 1rem; transition: opacity 0.3s; }
  .life.dead { opacity: 0.2; }

  .input-row { display: flex; gap: 10px; margin-bottom: 14px; }

  .two-part-inputs { display: flex; flex-direction: column; gap: 10px; margin-bottom: 14px; }
  .two-part-input-group { display: flex; gap: 10px; align-items: center; }
  .two-part-label { font-size: 0.68rem; color: var(--fc-muted); letter-spacing: 0.08em; text-transform: uppercase; white-space: nowrap; min-width: 52px; }
  .part-status { font-size: 0.9rem; min-width: 20px; text-align: center; }

  input[type="text"] {
    flex: 1;
    background: var(--fc-surface2);
    border: 1px solid var(--fc-border);
    border-radius: var(--radius);
    padding: 12px 16px;
    color: var(--text);
    font-family: 'DM Mono', monospace;
    font-size: 0.95rem;
    outline: none;
    transition: border-color 0.2s;
  }
  input[type="text"]:focus { border-color: var(--fc-accent2); }
  input[type="text"].input-correct { border-color: var(--fc-green); background: #1b2e21; }
  input[type="text"].input-wrong  { border-color: var(--fc-red); }
  input[type="text"].input-purple { border-color: var(--fc-purple); }

  .btn {
    background: var(--fc-accent);
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
    background: var(--fc-surface2);
    color: var(--text);
    border: 1px solid var(--fc-border);
  }
  .btn.secondary:hover { border-color: var(--fc-accent); color: var(--fc-accent); background: var(--fc-surface2); }

  .answer-reveal {
    margin-top: 10px;
    padding: 12px 16px;
    background: #2e1b1b;
    border: 1px solid var(--fc-red);
    border-radius: var(--radius);
    font-size: 0.9rem;
    color: #f0a0a0;
    letter-spacing: 0.04em;
  }
  .answer-reveal strong { color: var(--fc-red); }
  .answer-reveal.partial-reveal { background: #1e1530; border-color: var(--fc-purple); color: #c4b5fd; }
  .answer-reveal.partial-reveal strong { color: var(--fc-purple); }

  .feedback-msg {
    margin-top: 10px;
    font-size: 0.85rem;
    letter-spacing: 0.05em;
    min-height: 22px;
    transition: color 0.3s;
  }
  .feedback-msg.ok { color: var(--fc-green); }
  .feedback-msg.bad { color: var(--fc-red); }
  .feedback-msg.partial { color: var(--fc-purple); }

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
    border: 1px solid var(--fc-border);
    border-radius: var(--radius);
    overflow: hidden;
  }
  table { width: 100%; border-collapse: collapse; }
  thead { background: var(--fc-surface2); }
  th { padding: 10px 14px; font-size: 0.7rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--fc-muted); text-align: left; }
  td { padding: 10px 14px; font-size: 0.85rem; border-top: 1px solid var(--fc-border); vertical-align: middle; }
  tr:hover td { background: var(--fc-surface2); }
  .badge-lives { display: flex; gap: 4px; }
  .pip { width: 8px; height: 8px; border-radius: 50%; background: var(--fc-border); }
  .pip.active { background: var(--fc-accent2); }
  .pip.done { background: var(--fc-green); }

  .empty-state { text-align: center; color: var(--fc-muted); padding: 40px 0; }
  .empty-state .icon { font-size: 2.5rem; margin-bottom: 10px; }
  .empty-state p { font-size: 0.85rem; letter-spacing: 0.05em; }

  #completionScreen {
    display: none;
    width: 100%;
    max-width: 680px;
    background: var(--fc-surface);
    border: 1px solid var(--fc-accent);
    border-radius: 18px;
    padding: 48px 32px;
    text-align: center;
  }
  #completionScreen h2 {
    font-family: 'Playfair Display', serif;
    font-size: 2.2rem;
    color: var(--fc-accent);
    margin-bottom: 10px;
  }
  #completionScreen p { color: var(--fc-muted); font-size: 0.85rem; margin-bottom: 24px; }
</style>
</head>
<body>

<!-- ── Navigation ── -->
<nav class="app-nav">
  <span class="nav-brand">// Dietz</span>
  <button class="nav-tab active" onclick="switchPage('tracker')" id="tab-tracker">Revision Tracker</button>
  <button class="nav-tab" onclick="switchPage('flashcard')" id="tab-flashcard">Word Checker</button>
</nav>

<!-- ════════════════════════════════════════════════════════
     PAGE 1 — REVISION TRACKER
════════════════════════════════════════════════════════ -->
<div class="page active" id="page-tracker">

  <header class="tracker-header">
    <div class="header-left">
      <h1>Revision Tracker</h1>
      <p id="today-date"></p>
    </div>
    <div class="header-btns">
      <button class="copy-btn" id="copy-excel-btn" onclick="copyToExcel()">
        <span id="copy-icon">⎘</span>
        <span id="copy-label">Copy for Excel</span>
      </button>
      <button class="config-btn" onclick="openSubjects()">✎ Subjects</button>
    </div>
  </header>

  <div class="today-total">
    <span>Today's total</span>
    <span class="total-time mono" id="total-display">00:00:00</span>
  </div>

  <p class="section-label">Subjects</p>
  <div class="subjects-grid" id="subjects-grid"></div>

  <div id="log-section" style="display:none;">
    <p class="section-label" style="margin-top:1.5rem;">Session log</p>
    <div class="log-list" id="log-list"></div>
  </div>


  <!-- Subject manager modal -->
  <div class="modal-overlay" id="subjects-modal">
    <div class="modal">
      <h2>// Manage Subjects</h2>
      <div class="subject-list" id="subject-list"></div>
      <button class="btn-add-subject" onclick="addSubjectRow()">+ Add subject</button>
      <div class="modal-footer">
        <button class="btn-cancel" onclick="closeSubjects()">Cancel</button>
        <button class="btn-save" onclick="saveSubjects()">Save</button>
      </div>
    </div>
  </div>

</div><!-- /page-tracker -->

<!-- ════════════════════════════════════════════════════════
     PAGE 2 — WORD CHECKER / FLASHCARDS
════════════════════════════════════════════════════════ -->
<div class="page" id="page-flashcard">

  <header class="fc-header">
    <h1>Flashcards<span>Choose # correct and mode</span></h1>
    <div class="controls-row">
      <label class="file-label" for="fileInput">
        ⬆ Upload .xlsx
        <input type="file" id="fileInput" accept=".xlsx">
      </label>
      <button id="randomiseBtn" class="small-btn" title="Shuffle card order">🔀 Randomise</button>
      <button id="twoPartBtn" title="Require both parts of the definition (split by ; or /)">✦ 2-Part Mode</button>
      <div style="display:inline-flex; align-items:center; gap:6px; color:var(--fc-muted); font-size:0.82rem;">
        <label style="display:inline-flex; align-items:center; gap:6px; color:var(--fc-muted);">
          <input type="radio" name="repeatChoice" id="repeat1" value="1"> 1
        </label>
        <label style="display:inline-flex; align-items:center; gap:6px; color:var(--fc-muted);">
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

</div><!-- /page-flashcard -->

<div class="toast" id="toast"></div>

<!-- XLSX for flashcard page -->
<script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.0/dist/xlsx.full.min.js"></script>

<script>
/* ══════════════════════════════════════════════════════════
   PAGE SWITCHING
══════════════════════════════════════════════════════════ */
function switchPage(name) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('page-' + name).classList.add('active');
  document.getElementById('tab-' + name).classList.add('active');
}

/* ══════════════════════════════════════════════════════════
   REVISION TRACKER
══════════════════════════════════════════════════════════ */
const COLORS = ['#c3dee8'];

const DEFAULT_SUBJECTS = [
  { name: 'Mathematics' }, { name: 'Physics' }, { name: 'Chemistry' },
  { name: 'Computing' }, { name: 'Aerospace' }, { name: 'Electrical' },
  { name: 'Mechanics' }, { name: 'Materials' },
];

function loadSubjects() {
  const saved = localStorage.getItem('rt_subjects');
  return saved ? JSON.parse(saved) : DEFAULT_SUBJECTS;
}
function saveSubjectData(list) { localStorage.setItem('rt_subjects', JSON.stringify(list)); }

let SUBJECTS = loadSubjects();

const state = {
  timers: [],
  config: JSON.parse(localStorage.getItem('rt_config') || 'null'),
  logs: [],
  tick: null,
};

function initTimers() {
  state.timers = SUBJECTS.map(() => ({ running: false, elapsed: 0, startedAt: null, todayTotal: 0 }));
}

function colorFor(i) { return COLORS[i % COLORS.length]; }

// ── Grid ──────────────────────────────────────────────
function buildGrid() {
  const grid = document.getElementById('subjects-grid');
  grid.innerHTML = '';
  SUBJECTS.forEach((s, i) => {
    const color = colorFor(i);
    const card = document.createElement('div');
    card.className = 'subject-card';
    card.id = `card-${i}`;
    card.style.setProperty('--subject-color', color);
    card.innerHTML = `
      <div class="subject-header">
        <span class="subject-name">${s.name}</span>
        <button class="btn-edit-subject" onclick="openSubjects()" title="Edit subjects">✎</button>
      </div>
      <div class="timer-display mono" id="timer-${i}">00:00:00</div>
      <div class="session-info">today &mdash; <span id="today-${i}">00:00:00</span></div>
      <div class="card-footer">
        <button class="btn-timer btn-start" id="btn-${i}" onclick="toggleTimer(${i})">▶ Start</button>
        <button class="btn-log" id="log-${i}" onclick="logSession(${i})" disabled>↑ Log</button>
      </div>
    `;
    grid.appendChild(card);
  });
}

// ── Timers ────────────────────────────────────────────
function toggleTimer(i) {
  const t = state.timers[i];
  if (!t.running) {
    state.timers.forEach((ot, oi) => { if (oi !== i && ot.running) stopTimer(oi); });
    t.running = true;
    t.startedAt = Date.now() - t.elapsed;
    document.getElementById(`card-${i}`).classList.add('active');
    document.getElementById(`btn-${i}`).textContent = '■ Stop';
    document.getElementById(`btn-${i}`).className = 'btn-timer btn-stop';
    if (!state.tick) state.tick = setInterval(tick, 500);
  } else {
    stopTimer(i);
  }
}

function stopTimer(i) {
  const t = state.timers[i];
  if (!t.running) return;
  t.elapsed = Date.now() - t.startedAt;
  t.running = false;
  document.getElementById(`card-${i}`).classList.remove('active');
  document.getElementById(`btn-${i}`).textContent = '▶ Start';
  document.getElementById(`btn-${i}`).className = 'btn-timer btn-start';
  document.getElementById(`log-${i}`).disabled = false;
  const anyRunning = state.timers.some(t => t.running);
  if (!anyRunning && state.tick) { clearInterval(state.tick); state.tick = null; }
}

function tick() {
  let total = 0;
  state.timers.forEach((t, i) => {
    const elapsed = t.running ? Date.now() - t.startedAt : t.elapsed;
    const el = document.getElementById(`timer-${i}`);
    if (el) el.textContent = fmtTime(elapsed);
    total += (t.todayTotal || 0) + elapsed;
  });
  document.getElementById('total-display').textContent = fmtTime(total);
}

// ── Logging ───────────────────────────────────────────
async function logSession(i) {
  const t = state.timers[i];
  if (t.elapsed < 1000) { showToast('No time to log!', 'error'); return; }
  const subject = SUBJECTS[i].name;
  const date = todayISO();
  const time = new Date().toLocaleTimeString('en-GB', { hour:'2-digit', minute:'2-digit' });
  const hours = fmtHours(t.elapsed);
  const duration = fmtTime(t.elapsed);

  addLog(subject, t.elapsed, date, time);
  await appendToSheet([date, time, subject, hours, duration]);

  t.todayTotal = (t.todayTotal || 0) + t.elapsed;
  t.elapsed = 0;
  t.startedAt = null;
  document.getElementById(`timer-${i}`).textContent = '00:00:00';
  document.getElementById(`today-${i}`).textContent = fmtTime(t.todayTotal);
  document.getElementById(`log-${i}`).disabled = true;
  tick();
}

function addLog(subject, ms, date, time) {
  state.logs.unshift({ subject, ms, date, time });
  const list = document.getElementById('log-list');
  const item = document.createElement('div');
  item.className = 'log-item';
  item.innerHTML = `<span><strong>${subject}</strong> &mdash; ${fmtTime(ms)}</span><span>${date} ${time}</span>`;
  list.prepend(item);
  document.getElementById('log-section').style.display = 'block';
}

// ── Copy to Excel ─────────────────────────────────────

function copyToExcel() {
  const date = todayISO();

  const values = SUBJECTS.map((s, i) => {
    const t = state.timers[i];
    const currentElapsed = t.running ? Date.now() - t.startedAt : t.elapsed;
    const totalMs = (t.todayTotal || 0) + currentElapsed;
    return totalMs > 0 ? parseFloat((totalMs / 3600000).toFixed(4)) : 0;
  });

  const grandTotalMs = state.timers.reduce((sum, t, i) => {
    const currentElapsed = t.running ? Date.now() - t.startedAt : t.elapsed;
    return sum + (t.todayTotal || 0) + currentElapsed;
  }, 0);

  const totalHours = parseFloat((grandTotalMs / 3600000).toFixed(4));

  // Row: Date | Total time | Subject1 | Subject2 | ...
  const row = [date, totalHours, ...values];
  const tsv = row.join('\t');

  navigator.clipboard.writeText(tsv).then(() => {
    const btn = document.getElementById('copy-excel-btn');
    const label = document.getElementById('copy-label');
    btn.classList.add('copied');
    label.textContent = 'Copied!';
    showToast('Copied — paste into Excel!', 'success');
    setTimeout(() => {
      btn.classList.remove('copied');
      label.textContent = 'Copy for Excel';
    }, 2500);
  }).catch(() => {
    showToast('Copy failed — try again', 'error');
  });
}

// ── Subject manager ───────────────────────────────────
let editBuffer = [];

function openSubjects() {
  editBuffer = SUBJECTS.map(s => ({ ...s }));
  renderSubjectList();
  document.getElementById('subjects-modal').classList.add('open');
}
function closeSubjects() { document.getElementById('subjects-modal').classList.remove('open'); }

function renderSubjectList() {
  const list = document.getElementById('subject-list');
  list.innerHTML = '';
  editBuffer.forEach((s, i) => {
    const row = document.createElement('div');
    row.className = 'subject-list-item';
    row.innerHTML = `
      <div class="color-dot" style="background:${colorFor(i)}"></div>
      <input type="text" value="${s.name}" placeholder="Subject name"
        oninput="editBuffer[${i}].name = this.value">
      <button class="btn-delete" onclick="removeSubjectRow(${i})" title="Remove">✕</button>
    `;
    list.appendChild(row);
  });
}

function addSubjectRow() {
  editBuffer.push({ name: '' });
  renderSubjectList();
  const inputs = document.querySelectorAll('#subject-list input');
  if (inputs.length) inputs[inputs.length - 1].focus();
}
function removeSubjectRow(i) { editBuffer.splice(i, 1); renderSubjectList(); }

function saveSubjects() {
  const cleaned = editBuffer.map(s => ({ name: s.name.trim() })).filter(s => s.name);
  if (!cleaned.length) { showToast('Add at least one subject', 'error'); return; }
  state.timers.forEach((_, i) => { if (state.timers[i].running) stopTimer(i); });
  SUBJECTS = cleaned;
  saveSubjectData(SUBJECTS);
  initTimers();
  buildGrid();
  closeSubjects();
  showToast('Subjects saved!', 'success');
}

// ── Helpers ───────────────────────────────────────────
function fmtTime(ms) {
  const s = Math.floor(ms / 1000);
  const h = Math.floor(s / 3600);
  const m = Math.floor((s % 3600) / 60);
  const sec = s % 60;
  return `${String(h).padStart(2,'0')}:${String(m).padStart(2,'0')}:${String(sec).padStart(2,'0')}`;
}
function fmtHours(ms) { return (ms / 3600000).toFixed(4); }

function todayStr() {
  return new Date().toLocaleDateString('en-GB', { weekday:'short', year:'numeric', month:'short', day:'numeric' });
}
function todayISO() {
  const d = new Date();
  return `${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
}

function setStatus(s, msg) {
  document.getElementById('status-dot').className = 'status-dot ' + s;
  document.getElementById('status-text').textContent = msg;
}

let toastTimer;
function showToast(msg, type='') {
  const toast = document.getElementById('toast');
  toast.textContent = msg;
  toast.className = 'toast show ' + type;
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => { toast.className = 'toast'; }, 3000);
}

function initTracker() {
  document.getElementById('today-date').textContent = todayStr();
  initTimers();
  buildGrid();
  setInterval(() => { if (state.timers.some(t => t.running)) tick(); }, 1000);
}

/* ══════════════════════════════════════════════════════════
   FLASHCARD / WORD CHECKER
══════════════════════════════════════════════════════════ */
let REQUIRED_CORRECT = 5;
const WINDOW_SIZE = 5;
let twoPartMode = false;
let allCards = [];
let windowStart = 0;
let currentCard = null;
let wrongShown = false;
let totalCorrect = 0;
let totalWrong = 0;
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

function toggleTwoPartMode() {
  twoPartMode = !twoPartMode;
  twoPartBtn.classList.toggle('active', twoPartMode);
  twoPartBanner.classList.toggle('visible', twoPartMode);
  if (currentCard) { wrongShown = false; part1Correct = false; part2Correct = false; renderCard(); }
}

function splitDefinition(def) {
  const bySemi = def.split(';');
  if (bySemi.length >= 2) return [bySemi[0].trim(), bySemi.slice(1).join(';').trim()];
  const bySlash = def.split('/');
  if (bySlash.length >= 2) return [bySlash[0].trim(), bySlash.slice(1).join('/').trim()];
  return [def.trim()];
}

function onRepeatChange() {
  const val = document.querySelector('input[name="repeatChoice"]:checked').value;
  REQUIRED_CORRECT = parseInt(val, 10) || 5;
  document.querySelector('.fc-header h1 span').textContent = `${REQUIRED_CORRECT} correct = mastered`;
  renderWordList();
  updateStats();
}

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
      allCards.push({ id: idCounter++, phrase: String(row[0]), definition: String(row[1]), correctCount: 0, done: false });
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

function startGame() {
  if (allCards.length === 0) { alert('Upload an Excel file first (with columns: Word, Definition).'); return; }
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
    if (windowStart + WINDOW_SIZE < allCards.length) { windowStart += WINDOW_SIZE; nextCard(); }
    else {
      if (allCards.every(c => c.done)) showCompletion();
      else { if (windowStart >= allCards.length) windowStart = 0; advanceWindow(); nextCard(); }
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
        <span style="font-size:0.72rem; color:var(--fc-muted); align-self:center; letter-spacing:0.05em;">Both parts must be correct</span>
      </div>`;
  } else {
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
    const input1 = document.getElementById('defGuess1');
    const input2 = document.getElementById('defGuess2');
    if (!input1 || !input2) return;

    if (!part1Correct) {
      const val1 = input1.value.trim();
      if (val1.toLowerCase() === parts[0].toLowerCase()) {
        part1Correct = true; input1.classList.add('input-correct'); input1.readOnly = true;
      } else if (val1.length > 0) {
        input1.classList.add('input-wrong'); setTimeout(() => input1.classList.remove('input-wrong'), 600);
      }
    }

    if (!part2Correct) {
      const val2 = input2.value.trim();
      if (val2.toLowerCase() === parts[1].toLowerCase()) {
        part2Correct = true; input2.classList.add('input-correct'); input2.readOnly = true;
      } else if (val2.length > 0) {
        input2.classList.add('input-wrong'); setTimeout(() => input2.classList.remove('input-wrong'), 600);
      }
    }

    if (part1Correct && part2Correct) {
      totalCorrect++;
      if (currentCard.correctCount < REQUIRED_CORRECT) currentCard.correctCount++;
      if (currentCard.correctCount >= REQUIRED_CORRECT) currentCard.done = true;
      fc.className = 'correct';
      if (msgDiv) { msgDiv.className = 'feedback-msg ok'; msgDiv.textContent = `✓ Both parts correct! (${currentCard.correctCount}/${REQUIRED_CORRECT} correct)`; }
      const existingReveal = fc.querySelector('.answer-reveal');
      if (existingReveal) existingReveal.remove();
      setTimeout(() => { fc.className = ''; nextCard(); }, 900);
    } else if (part1Correct || part2Correct) {
      fc.className = 'partial';
      const doneCount = (part1Correct ? 1 : 0) + (part2Correct ? 1 : 0);
      if (msgDiv) { msgDiv.className = 'feedback-msg partial'; msgDiv.textContent = `✦ ${doneCount}/2 parts correct — keep going!`; }
      if (!part1Correct && document.getElementById('defGuess1')) document.getElementById('defGuess1').focus();
      else if (!part2Correct && document.getElementById('defGuess2')) document.getElementById('defGuess2').focus();
    } else {
      totalWrong++;
      fc.className = 'wrong';
      if (msgDiv) { msgDiv.className = 'feedback-msg bad'; msgDiv.textContent = `✗ Try again — both parts needed.`; }
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
    const input = document.getElementById('defGuess');
    if (!input) return;
    const userAnswer = input.value.trim();
    const correctAnswer = currentCard.definition;

    if (userAnswer.toLowerCase() === correctAnswer.toLowerCase()) {
      totalCorrect++;
      if (currentCard.correctCount < REQUIRED_CORRECT) currentCard.correctCount++;
      if (currentCard.correctCount >= REQUIRED_CORRECT) currentCard.done = true;
      fc.className = 'correct';
      if (msgDiv) { msgDiv.className = 'feedback-msg ok'; msgDiv.textContent = `✓ Correct! (${currentCard.correctCount}/${REQUIRED_CORRECT} correct)`; }
      input.value = '';
      const existingReveal = fc.querySelector('.answer-reveal');
      if (existingReveal) existingReveal.remove();
      setTimeout(() => { fc.className = ''; nextCard(); }, 800);
    } else {
      totalWrong++;
      fc.className = 'wrong';
      if (msgDiv) { msgDiv.className = 'feedback-msg bad'; msgDiv.textContent = `✗ Try again.`; }
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
  document.getElementById('progressLabel').textContent = total > 0 ? `${mastered} of ${total} mastered (${REQUIRED_CORRECT} correct each)` : 'Upload a file to begin';
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
  windowStart = 0; totalCorrect = 0; totalWrong = 0;
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
    const rowStyle = card.done ? 'opacity:0.5' : (currentCard === card ? 'background:var(--fc-surface2)' : '');
    const parts = splitDefinition(card.definition);
    let defDisplay = escHtml(card.definition);
    if (twoPartMode && parts.length === 2) {
      defDisplay = `<span style="color:var(--fc-purple)">${escHtml(parts[0])}</span> <span style="color:var(--fc-muted)">·</span> <span style="color:var(--fc-accent2)">${escHtml(parts[1])}</span>`;
    }
    return `<tr style="${rowStyle}">
      <td style="color:var(--fc-muted);font-size:0.7rem">${idx + 1}</td>
      <td style="font-weight:500;">${escHtml(card.phrase)}</td>
      <td style="color:var(--fc-muted)">${defDisplay}</td>
      <td>${pipContainer} <span style="font-size:0.65rem; margin-left:6px;">${card.correctCount}/${REQUIRED_CORRECT}</span></td>
    </tr>`;
  }).join('');
  wordListTable.innerHTML = `
    <thead><tr>
      <th>#</th><th>Word</th>
      <th>Definition${twoPartMode ? ' (Part 1 · Part 2)' : ''}</th>
      <th>Progress (${REQUIRED_CORRECT}✔️)</th>
    </tr></thead>
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

/* ── Boot ── */
initTracker();
onRepeatChange();
</script>
</body>
</html>
