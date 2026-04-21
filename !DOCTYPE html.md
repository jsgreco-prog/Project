# <!DOCTYPE html>  
  
<!DOCTYPE html>  
<html lang="en">  
<head>  
  <meta charset="UTF-8" />  
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>  
  <title>Arc Flash Job Record</title>  
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@400;500;700&display=swap" rel="stylesheet"/>  
  <style>  
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }  
  
    :root {  
      --orange: #f5a623;  
      --green: #008000;  
      --yellow: #ffff00;  
      --cyan: #00ffff;  
      --magenta: #ff00ff;  
      --blue: #4169e1;  
      --red: #e8380d;  
      --bg: #0f0d0b;  
      --card: rgba(255,255,255,0.03);  
      --border: rgba(255,255,255,0.08);  
      --text: #ffffff;  
      --muted: rgba(255,255,255,0.45);  
      --dim: rgba(255,255,255,0.25);  
      --dark: #1a1008;  
    }  
  
    body {  
      background: var(--bg);  
      background-image:  
        radial-gradient(ellipse at 20% 0%, rgba(232,56,13,0.12) 0%, transparent 60%),  
        radial-gradient(ellipse at 80% 100%, rgba(245,166,35,0.08) 0%, transparent 60%);  
      font-family: 'Syne', sans-serif;  
      color: var(--text);  
      min-height: 100vh;  
      display: flex;  
      flex-direction: column;  
      align-items: center;  
      padding: 40px 16px 80px;  
    }  
  
    ::-webkit-scrollbar { width: 4px; }  
    ::-webkit-scrollbar-track { background: transparent; }  
    ::-webkit-scrollbar-thumb { background: rgba(245,166,35,0.3); border-radius: 4px; }  
  
    @keyframes fadeIn {  
      from { opacity: 0; transform: translateY(10px); }  
      to   { opacity: 1; transform: translateY(0); }  
    }  
    @keyframes slideIn {  
      from { opacity: 0; transform: translateY(6px); }  
      to   { opacity: 1; transform: translateY(0); }  
    }  
  
    /* ── Header ── */  
    .header {  
      width: 100%; max-width: 620px; margin-bottom: 40px;  
      animation: fadeIn 0.4s ease;  
    }  
    .header-inner { display: flex; align-items: center; gap: 14px; }  
    .header-icon {  
      width: 40px; height: 40px; border-radius: 10px; flex-shrink: 0;  
      background: linear-gradient(135deg, var(--red), var(--blue));  
      display: flex; align-items: center; justify-content: center; font-size: 20px;  
    }  
    .header-title { font-weight: 800; font-size: 20px; letter-spacing: -0.02em; }  
    .header-sub {  
      font-family: 'DM Mono', monospace; font-size: 10px;  
      color: rgba(255,255,255,0.3); letter-spacing: 0.12em; text-transform: uppercase;  
      margin-top: 3px;  
    }  
  
    /* ── Card ── */  
    .card {  
      width: 100%; max-width: 620px;  
      background: var(--card);  
      border: 1px solid var(--border);  
      border-radius: 20px;  
      padding: 36px 32px;  
      animation: fadeIn 0.4s ease;  
    }  
  
    /* ── Step Indicator ── */  
    .step-indicator {  
      display: flex; align-items: center; margin-bottom: 36px;  
    }  
    .step-item {  
      display: flex; flex-direction: column; align-items: center; gap: 6px; flex-shrink: 0;  
    }  
    .step-circle {  
      width: 36px; height: 36px; border-radius: 50%;  
      display: flex; align-items: center; justify-content: center;  
      font-family: 'DM Mono', monospace; font-size: 13px; font-weight: 700;  
      border: 2px solid rgba(255,255,255,0.15);  
      background: rgba(255,255,255,0.08);  
      color: rgba(255,255,255,0.4);  
      transition: all 0.3s;  
    }  
    .step-circle.done   { background: var(--orange); border-color: var(--orange); color: var(--dark); }  
    .step-circle.active { background: var(--red);    border-color: var(--orange); color: var(--dark); }  
    .step-label {  
      font-family: 'DM Mono', monospace; font-size: 10px; font-weight: 600;  
      letter-spacing: 0.08em; text-transform: uppercase;  
      color: rgba(255,255,255,0.3); white-space: nowrap; transition: color 0.3s;  
    }  
    .step-label.done   { color: rgba(245,166,35,0.8); }  
    .step-label.active { color: var(--orange); }  
    .step-line {  
      flex: 1; height: 2px; margin: 0 8px; margin-bottom: 22px;  
      background: rgba(255,255,255,0.1); transition: background 0.3s;  
    }  
    .step-line.done { background: var(--orange); }  
  
    /* ── Section Label ── */  
    .section-label {  
      font-family: 'DM Mono', monospace; font-size: 10px; font-weight: 700;  
      letter-spacing: 0.15em; text-transform: uppercase;  
      color: var(--orange); margin-bottom: 12px;  
      display: flex; align-items: center; gap: 8px;  
    }  
    .section-label::before {  
      content: ''; display: inline-block; width: 24px; height: 1px; background: var(--orange);  
    }  
  
    /* ── Description text ── */  
    .desc { color: var(--muted); font-size: 13.5px; margin-bottom: 20px; line-height: 1.5; }  
  
    /* ── Input ── */  
    .text-input {  
      width: 100%; padding: 16px 20px;  
      background: rgba(255,255,255,0.05);  
      border: 1px solid rgba(255,255,255,0.12);  
      border-radius: 10px; color: var(--text);  
      font-family: 'Syne', sans-serif; font-size: 16px;  
      outline: none; transition: border-color 0.2s;  
    }  
    .text-input:focus { border-color: var(--orange); }  
    .text-input::placeholder { color: rgba(255,255,255,0.25); }  
  
    textarea.text-input { resize: vertical; line-height: 1.6; }  
  
    /* ── Timestamp ── */  
    .timestamp {  
      margin-top: 12px; font-family: 'DM Mono', monospace;  
      font-size: 11px; color: rgba(255,255,255,0.25);  
    }  
  
    /* ── Buttons ── */  
    .btn {  
      padding: 14px 20px; border-radius: 10px; border: none;  
      font-family: 'DM Mono', monospace; font-size: 13px; font-weight: 700;  
      letter-spacing: 0.1em; text-transform: uppercase; cursor: pointer;  
      transition: all 0.2s;  
    }  
    .btn-primary {  
      background: linear-gradient(135deg, var(--red), var(--blue));  
      color: var(--dark);  
    }  
    .btn-primary:disabled {  
      background: rgba(255,255,255,0.07);  
      color: rgba(255,255,255,0.25); cursor: not-allowed;  
    }  
    .btn-secondary {  
      background: rgba(255,255,255,0.06);  
      border: 1px solid rgba(255,255,255,0.1);  
      color: rgba(255,255,255,0.5);  
      font-size: 12px;  
    }  
    .btn-success {  
      background: linear-gradient(135deg, #27ae60, #2ecc71);  
      color: #0a2010;  
    }  
    .btn-success:disabled {  
      background: rgba(255,255,255,0.07);  
      color: rgba(255,255,255,0.25); cursor: not-allowed;  
    }  
    .btn-row { display: flex; gap: 12px; margin-top: 32px; }  
    .btn-row .btn { flex: 1; }  
    .btn-row .btn-primary,  
    .btn-row .btn-success { flex: 2; }  
    .btn-full { width: 100%; margin-top: 32px; }  
  
    /* ── Radio Card ── */  
    .radio-card {  
      padding: 14px 18px; border-radius: 10px; cursor: pointer;  
      background: rgba(255,255,255,0.03);  
      border: 1px solid rgba(255,255,255,0.08);  
      color: rgba(255,255,255,0.55);  
      font-size: 14px;  
      display: flex; align-items: center; gap: 12px;  
      transition: all 0.2s; user-select: none; margin-bottom: 8px;  
    }  
    .radio-card.selected {  
      background: rgba(232,56,13,0.15);  
      border-color: var(--red);  
      color: var(--text);  
    }  
    .radio-dot {  
      width: 16px; height: 16px; border-radius: 50%; flex-shrink: 0;  
      border: 2px solid rgba(255,255,255,0.25);  
      background: transparent; transition: all 0.2s;  
    }  
    .radio-card.selected .radio-dot {  
      border-color: var(--red); background: var(--red);  
    }  
  
    /* ── Checkbox ── */  
    .check-item {  
      display: flex; align-items: flex-start; gap: 12px; cursor: pointer;  
      padding: 10px 14px; border-radius: 8px;  
      background: rgba(255,255,255,0.03);  
      border: 1px solid rgba(255,255,255,0.07);  
      transition: all 0.2s; user-select: none; margin-bottom: 8px;  
    }  
    .check-item.checked {  
      background: rgba(245,166,35,0.10);  
      border-color: rgba(245,166,35,0.4);  
    }  
    .check-box {  
      width: 18px; height: 18px; border-radius: 4px; flex-shrink: 0; margin-top: 1px;  
      border: 2px solid rgba(255,255,255,0.2);  
      background: transparent;  
      display: flex; align-items: center; justify-content: center;  
      transition: all 0.2s; font-size: 11px; font-weight: 900; color: var(--dark);  
    }  
    .check-item.checked .check-box {  
      background: var(--orange); border-color: var(--orange);  
    }  
    .check-label {  
      font-size: 13.5px; color: rgba(255,255,255,0.6);  
      line-height: 1.4; transition: color 0.2s;  
    }  
    .check-item.checked .check-label { color: var(--text); }  
  
    /* ── Grid ── */  
    .grid-2 { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-bottom: 32px; }  
    .grid-2 .check-item { margin-bottom: 0; }  
  
    /* ── Scrollable list ── */  
    .scroll-list { max-height: 400px; overflow-y: auto; padding-right: 4px; }  
  
    /* ── Alert boxes ── */  
    .alert-problem {  
      padding: 20px; border-radius: 12px;  
      background: rgba(232,56,13,0.08); border: 1px solid rgba(232,56,13,0.2);  
      margin-bottom: 28px;  
    }  
    .alert-problem-title { font-weight: 700; font-size: 15px; margin-bottom: 16px; }  
    .alert-success {  
      padding: 16px 20px; border-radius: 10px;  
      background: rgba(80,220,100,0.08); border: 1px solid rgba(80,220,100,0.2);  
      color: #7edfaa; font-size: 14px;  
      display: flex; align-items: center; gap: 12px;  
    }  
    .alert-icon { font-size: 20px; }  
  
    /* ── Problem section ── */  
    #problem-section { animation: slideIn 0.25s ease; }  
  
    /* ── Submitted screen ── */  
    .submitted { text-align: center; padding: 20px 0; animation: fadeIn 0.4s ease; }  
    .submitted-icon {  
      width: 72px; height: 72px; border-radius: 50%; margin: 0 auto 24px;  
      background: linear-gradient(135deg, #27ae60, #2ecc71);  
      display: flex; align-items: center; justify-content: center; font-size: 32px;  
    }  
    .submitted-title { font-size: 24px; font-weight: 800; margin-bottom: 8px; }  
    .submitted-time {  
      font-family: 'DM Mono', monospace; font-size: 12px;  
      color: rgba(255,255,255,0.35); margin-bottom: 32px;  
    }  
    .summary-card {  
      background: rgba(255,255,255,0.04); border-radius: 12px;  
      border: 1px solid rgba(255,255,255,0.08);  
      padding: 20px; text-align: left; margin-bottom: 32px;  
    }  
    .summary-row {  
      display: flex; gap: 12px; padding: 10px 0;  
      border-bottom: 1px solid rgba(255,255,255,0.06);  
    }  
    .summary-row:last-child { border-bottom: none; }  
    .summary-key {  
      font-family: 'DM Mono', monospace; font-size: 11px;  
      color: var(--orange); min-width: 110px; padding-top: 1px;  
    }  
    .summary-val { font-size: 13.5px; color: rgba(255,255,255,0.7); line-height: 1.4; }  
  
    /* ── Footer ── */  
    .footer {  
      margin-top: 24px; font-family: 'DM Mono', monospace;  
      font-size: 10px; color: rgba(255,255,255,0.15); letter-spacing: 0.08em;  
    }  
  
    /* ── Steps visibility ── */  
    .step-panel { display: none; }  
    .step-panel.active { display: block; animation: slideIn 0.25s ease; }  
  
    @media (max-width: 500px) {  
      .card { padding: 24px 18px; }  
      .grid-2 { grid-template-columns: 1fr; }  
      .step-label { font-size: 9px; }  
    }  
  </style>  
</head>  
<body>  
  
  <!-- Header -->  
  <div class="header">  
    <div class="header-inner">  
      <div class="header-icon">⚡</div>  
      <div>  
        <div class="header-title">Meter Task Record</div>  
        <div class="header-sub">Electrical / Utility Safety System</div>  
      </div>  
    </div>  
  </div>  
  
  <!-- Card -->  
  <div class="card" id="main-card">  
  
    <!-- Step Indicator -->  
    <div class="step-indicator" id="step-indicator">  
      <div class="step-item">  
        <div class="step-circle active" id="sc-0">1</div>  
        <div class="step-label active" id="sl-0">Worker</div>  
      </div>  
      <div class="step-line" id="line-0"></div>  
      <div class="step-item">  
        <div class="step-circle" id="sc-1">2</div>  
        <div class="step-label" id="sl-1">Task</div>  
      </div>  
       <div class="step-line" id="line-1"></div>  
       <div class="step-item">  
          <div class="step-circle" id="sc-2">3</div>  
          <div class="step-label" id="sl-2">Service Voltage</div>  
      </div>  
  
      <div class="step-line" id="line-2"></div>  
      <div class="step-item">  
        <div class="step-circle" id="sc-3">4</div>  
        <div class="step-label" id="sl-3">Boundary & PPE</div>  
      </div>  
      <div class="step-line" id="line-3"></div>  
      <div class="step-item">  
        <div class="step-circle" id="sc-4">5</div>  
        <div class="step-label" id="sl-4">Completion</div>  
      </div>  
    </div>  
  
    <!-- ── STEP 0: Worker ── -->  
    <div class="step-panel active" id="panel-0">  
      <div class="section-label">Worker Identification</div>  
      <p class="desc">Enter your name or employee ID to begin the job task record.</p>  
      <input class="text-input" id="worker-name" type="text" placeholder="Full name or Employee ID…" oninput="validateWorker()" />  
      <div class="timestamp" id="timestamp"></div>  
      <button class="btn btn-primary btn-full" id="btn-0" onclick="goTo(1)" disabled>Continue →</button>  
    </div>  
  
    <!-- ── STEP 1: Task ── -->  
    <div class="step-panel" id="panel-1">  
      <div class="section-label">Job Task Selection</div>  
      <p class="desc">Select the task you are about to perform.</p>  
      <div class="scroll-list" id="task-list"></div>  
      <div class="btn-row">  
        <button class="btn btn-secondary" onclick="goTo(0)">← Back</button>  
        <button class="btn btn-primary" id="btn-1" onclick="goTo(2)" disabled>Continue →</button>  
      </div>  
    </div>  
  
    <!-- ── STEP 2: Boundary & PPE ── -->  
    <div class="step-panel" id="panel-2">  
      <div class="section-label">Arc Flash Boundary</div>  
      <p class="desc">Select all applicable arc flash boundary distances for this task.</p>  
      <div class="grid-2" id="boundary-list"></div>  
  
      <div class="section-label">PPE Being Worn</div>  
      <p class="desc">Check every item of PPE you are currently wearing.</p>  
      <div id="ppe-list"></div>  
  
      <div class="btn-row">  
        <button class="btn btn-secondary" onclick="goTo(1)">← Back</button>  
        <button class="btn btn-primary" id="btn-2" onclick="goTo(3)" disabled>Job Complete — Report →</button>  
      </div>  
    </div>  
  
    <!-- ── STEP 2: Boundary & PPE ── -->  
    <div class="step-panel" id="panel-2">  
      <div class="section-label">Arc Flash Boundary</div>  
      <p class="desc">Select all applicable arc flash boundary distances for this task.</p>  
      <div class="grid-2" id="boundary-list"></div>  
  
      <div class="section-label">PPE Being Worn</div>  
      <p class="desc">Check every item of PPE you are currently wearing.</p>  
      <div id="ppe-list"></div>  
  
      <div class="btn-row">  
        <button class="btn btn-secondary" onclick="goTo(1)">← Back</button>  
        <button class="btn btn-primary" id="btn-2" onclick="goTo(3)" disabled>Job Complete — Report →</button>  
      </div>  
    </div>  
  
    <!-- ── STEP 3: Completion ── -->  
    <div class="step-panel" id="panel-3">  
      <div class="section-label">Job Completion Report</div>  
      <p class="desc">Answer the following after completing your task.</p>  
  
      <div class="alert-problem">  
        <div class="alert-problem-title">Was a problem found during this task?</div>  
        <div id="problem-radio">  
          <div class="radio-card" id="rc-yes" onclick="setProblem(true)">  
            <div class="radio-dot"></div>Yes — Problem Found  
          </div>  
          <div class="radio-card" id="rc-no" onclick="setProblem(false)">  
            <div class="radio-dot"></div>No — All Clear  
          </div>  
        </div>  
      </div>  
  
      <div id="problem-section" style="display:none;">  
        <div class="section-label">Problem Type(s) Identified</div>  
        <p class="desc">Select all problems encountered.</p>  
        <div id="problem-list"></div>  
  
        <div class="section-label" style="margin-top:24px;">Problem Description / Notes</div>  
        <textarea class="text-input" id="problem-notes" rows="5"  
          placeholder="Describe the problem in detail, actions taken, and any follow-up required…"></textarea>  
      </div>  
  
      <div id="all-clear-msg" style="display:none;" class="alert-success">  
        <span class="alert-icon">✓</span>  
        Task completed with no issues. Ready to submit.  
      </div>  
  
      <div class="btn-row">  
        <button class="btn btn-secondary" onclick="goTo(2)">← Back</button>  
        <button class="btn btn-success" id="btn-3" onclick="submitForm()" disabled>Submit Report ✓</button>  
      </div>  
    </div>  
  
    <!-- ── Submitted ── -->  
    <div id="submitted-screen" style="display:none;" class="submitted">  
      <div class="submitted-icon">✓</div>  
      <div class="submitted-title">Report Submitted</div>  
      <div class="submitted-time" id="submitted-time"></div>  
      <div class="summary-card" id="summary-card"></div>  
      <button class="btn btn-primary btn-full" onclick="resetForm()">Start New Record</button>  
    </div>  
  
  </div>  
  
  <div class="footer">NFPA 70E COMPLIANT RECORD SYSTEM</div>  
  
<script>  
  // ── Data ──────────────────────────────────────────────────────────────────  
  
    const JOB_TASKS = [  
    "Verification / Read",  
    "Transformer Inspection",  
    "Switchgear Inspection / Maintenance",  
    "Meter Change",  
    "Meter Test",  
    "Current Transformer Instalation",  
    "Meter Installation / Replace",  
    "Voltage Stabalizer Installation",  
    "Battery System Maintenance",  
    "Generator Inspection / Maintenance",  
    "Primary Inspection",  
    "Grounding & Bonding",  
    "Hot-Stick / Live-Line Work",  
    "Meter Adapter Installation",  
    "Custom (see notes)",  
  ];   
  
  const ARC_FLASH_BOUNDARIES = [  
    "Restricted Approach",  
    "Prohibited Approach",  
    "2 ft 0 in",  
    "2 ft 3 in",  
    "3 ft 0 in",  
    "5 ft 6 in",  
    "8 ft 0 in",  
    "15 ft 0 in",  
    "26 ft 0 in",  
    "0 ft 0 in",  
    "Custom (see notes)",  
  ];  
  
  const PPE_ITEMS = [  
    "Arc Flash Suit (full body)",  
    "Arc-Rated Face Shield",  
    "Arc-Rated Balaclava / Hood",  
    "Arc-Rated Gloves (rubber insulating)",  
    "Arc-Rated Gloves (leather protectors)",  
    "Arc-Rated Jacket / Shirt",  
    "Arc-Rated Pants / Coveralls",  
    "Hard Hat (Class E)",  
    "Safety Glasses / Goggles",  
    "Hearing Protection",  
    "Leather Safety Boots",  
    "Flame-Resistant (FR) Clothing",  
    "High-Visibility Vest (arc-rated)",  
    "Voltage-Rated Tools",  
    "Insulated Blankets / Barriers",  
    "Ground Fault Circuit Interrupter (GFCI)",  
  ];  
  
  const PROBLEM_TYPES = [  
    "Unexpected Energized Component",  
    "Equipment Lockout / Tagout Failure",  
    "Arc Flash Event / Near Miss",  
    "PPE Damage or Failure",  
    "Improper Grounding Found",  
    "Overcurrent / Fault Condition",  
    "Insulation Failure",  
    "Conductor Damage",  
    "Equipment Malfunction",  
    "Environmental Hazard (water, debris)",  
    "Inadequate Clearances",  
    "Missing or Incorrect Labels / Signage",  
    "Unauthorized Personnel in Area",  
    "Communication Failure",  
    "Other (describe in notes)",  
  ];  
  
  // ── State ─────────────────────────────────────────────────────────────────  
  
  let state = {  
    step: 0,  
    name: "",  
    task: "",  
    boundaries: new Set(),  
    ppe: new Set(),  
    problemFound: null,  
    problemTypes: new Set(),  
  };  
  
  // ── Init ──────────────────────────────────────────────────────────────────  
  
  document.getElementById('timestamp').textContent =  
    'DATE / TIME: ' + new Date().toLocaleString();  
  
  // Build task list  
  const taskList = document.getElementById('task-list');  
  JOB_TASKS.forEach(t => {  
    const el = document.createElement('div');  
    el.className = 'radio-card';  
    el.dataset.value = t;  
    el.innerHTML = `<div class="radio-dot"></div>${t}`;  
    el.addEventListener('click', () => selectTask(t, el));  
    taskList.appendChild(el);  
  });  
  
  // Build boundary checkboxes  
  const boundaryList = document.getElementById('boundary-list');  
  ARC_FLASH_BOUNDARIES.forEach(b => {  
    boundaryList.appendChild(makeCheckbox(b, 'boundaries'));  
  });  
  
  // Build PPE checkboxes  
  const ppeList = document.getElementById('ppe-list');  
  PPE_ITEMS.forEach(p => {  
    ppeList.appendChild(makeCheckbox(p, 'ppe'));  
  });  
  
  // Build problem type checkboxes  
  const problemList = document.getElementById('problem-list');  
  PROBLEM_TYPES.forEach(p => {  
    problemList.appendChild(makeCheckbox(p, 'problemTypes'));  
  });  
  
  // ── Helpers ───────────────────────────────────────────────────────────────  
  
  function makeCheckbox(label, setKey) {  
    const el = document.createElement('div');  
    el.className = 'check-item';  
    el.dataset.value = label;  
    el.dataset.setKey = setKey;  
    el.innerHTML = `<div class="check-box"></div><span class="check-label">${label}</span>`;  
    el.addEventListener('click', () => toggleCheck(el, label, setKey));  
    return el;  
  }  
  
  function toggleCheck(el, label, setKey) {  
    if (state[setKey].has(label)) {  
      state[setKey].delete(label);  
      el.classList.remove('checked');  
      el.querySelector('.check-box').textContent = '';  
    } else {  
      state[setKey].add(label);  
      el.classList.add('checked');  
      el.querySelector('.check-box').textContent = '✓';  
    }  
    validateBoundaryPPE();  
    validateCompletion();  
  }  
  
  function selectTask(value, el) {  
    state.task = value;  
    document.querySelectorAll('#task-list .radio-card').forEach(c => c.classList.remove('selected'));  
    el.classList.add('selected');  
    document.getElementById('btn-1').disabled = false;  
  }  
  
  function setProblem(found) {  
    state.problemFound = found;  
    document.getElementById('rc-yes').classList.toggle('selected', found === true);  
    document.getElementById('rc-no').classList.toggle('selected', found === false);  
    document.getElementById('problem-section').style.display = found ? 'block' : 'none';  
    document.getElementById('all-clear-msg').style.display  = found ? 'none'  : 'flex';  
    validateCompletion();  
  }  
  
  // ── Validation ────────────────────────────────────────────────────────────  
  
  function validateWorker() {  
    const val = document.getElementById('worker-name').value.trim();  
    state.name = val;  
    document.getElementById('btn-0').disabled = val.length < 2;  
  }  
  
  function validateBoundaryPPE() {  
    document.getElementById('btn-2').disabled =  
      state.boundaries.size === 0 || state.ppe.size === 0;  
  }  
  
  function validateCompletion() {  
    const ok = state.problemFound !== null &&  
      (state.problemFound === false || state.problemTypes.size > 0);  
    document.getElementById('btn-3').disabled = !ok;  
  }  
  
  // ── Navigation ────────────────────────────────────────────────────────────  
  
  function goTo(step) {  
    document.getElementById('panel-' + state.step).classList.remove('active');  
    state.step = step;  
    document.getElementById('panel-' + step).classList.add('active');  
    updateStepIndicator(step);  
    window.scrollTo({ top: 0, behavior: 'smooth' });  
  }  
  
  function updateStepIndicator(current) {  
    for (let i = 0; i < 4; i++) {  
      const circle = document.getElementById('sc-' + i);  
      const label  = document.getElementById('sl-' + i);  
      circle.className = 'step-circle' + (i < current ? ' done' : i === current ? ' active' : '');  
      circle.textContent = i < current ? '✓' : (i + 1);  
      label.className = 'step-label' + (i < current ? ' done' : i === current ? ' active' : '');  
      if (i < 3) {  
        document.getElementById('line-' + i).className = 'step-line' + (i < current ? ' done' : '');  
      }  
    }  
  }  
  
  // ── Submit ────────────────────────────────────────────────────────────────  
  
  function submitForm() {  
    // Build submission payload — hook your backend fetch() here  
    const payload = {  
      timestamp: new Date().toISOString(),  
      worker: state.name,  
      task: state.task,  
      arcFlashBoundaries: [...state.boundaries],  
      ppeWorn: [...state.ppe],  
      problemFound: state.problemFound,  
      problemTypes: [...state.problemTypes],  
      problemNotes: document.getElementById('problem-notes').value,  
    };  
    console.log('SUBMIT PAYLOAD:', payload);  
  
    // Show submitted screen  
    document.getElementById('step-indicator').style.display = 'none';  
    for (let i = 0; i < 4; i++) {  
      document.getElementById('panel-' + i).classList.remove('active');  
    }  
    document.getElementById('submitted-time').textContent = new Date().toLocaleString();  
  
    // Build summary  
    const rows = [  
      ['Worker',       payload.worker],  
      ['Task',         payload.task],  
      ['Boundaries',   payload.arcFlashBoundaries.join(', ') || '—'],  
      ['PPE Items',    payload.ppeWorn.length + ' items selected'],  
      ['Problem Found', payload.problemFound ? 'YES' : 'No'],  
    ];  
    if (payload.problemFound) {  
      rows.push(['Problem Types', payload.problemTypes.join(', ') || '—']);  
      if (payload.problemNotes) rows.push(['Notes', payload.problemNotes]);  
    }  
  
    const card = document.getElementById('summary-card');  
    card.innerHTML = rows.map(([k, v]) =>  
      `<div class="summary-row">  
         <span class="summary-key">${k.toUpperCase()}</span>  
         <span class="summary-val">${v}</span>  
       </div>`  
    ).join('');  
  
    document.getElementById('submitted-screen').style.display = 'block';  
    window.scrollTo({ top: 0, behavior: 'smooth' });  
  }  
  
  function resetForm() {  
    state = {  
      step: 0, name: '', task: '',  
      boundaries: new Set(), ppe: new Set(),  
      problemFound: null, problemTypes: new Set(),  
    };  
  
    document.getElementById('worker-name').value = '';  
    document.getElementById('btn-0').disabled = true;  
    document.getElementById('btn-1').disabled = true;  
    document.getElementById('btn-2').disabled = true;  
    document.getElementById('btn-3').disabled = true;  
    document.getElementById('problem-notes').value = '';  
    document.getElementById('problem-section').style.display = 'none';  
    document.getElementById('all-clear-msg').style.display = 'none';  
    document.getElementById('rc-yes').classList.remove('selected');  
    document.getElementById('rc-no').classList.remove('selected');  
    document.getElementById('submitted-screen').style.display = 'none';  
    document.getElementById('step-indicator').style.display = 'flex';  
    document.getElementById('timestamp').textContent = 'DATE / TIME: ' + new Date().toLocaleString();  
  
    document.querySelectorAll('.radio-card').forEach(el => el.classList.remove('selected'));  
    document.querySelectorAll('.check-item').forEach(el => {  
      el.classList.remove('checked');  
      el.querySelector('.check-box').textContent = '';  
    });  
  
    goTo(0);  
  }  
</script>  
</body>  
</html>  
