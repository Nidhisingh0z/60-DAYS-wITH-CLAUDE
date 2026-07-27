<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Operation Lifeline: Supply Chain Crisis Lab</title>
<script src="https://unpkg.com/react@18/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<style>
  :root{
    --bg:#080b14;
    --bg2:#0d1220;
    --card:#121a2c;
    --card-hover:#182238;
    --border:#232c44;
    --border-light:#2e3a58;
    --accent:#4f7fff;
    --accent2:#22d3ee;
    --accent3:#a855f7;
    --good:#22c55e;
    --warn:#f59e0b;
    --bad:#ef4444;
    --text:#e6ebf5;
    --muted:#8a97b3;
    --muted-dim:#5c6785;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    background:
      radial-gradient(circle at 10% 0%, rgba(79,127,255,0.12), transparent 40%),
      radial-gradient(circle at 90% 10%, rgba(168,85,247,0.10), transparent 40%),
      radial-gradient(circle at 50% 100%, rgba(34,211,238,0.08), transparent 45%),
      var(--bg);
    color:var(--text);
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    min-height:100vh;
  }
  #root{min-height:100vh;}
  .app-shell{
    max-width:1180px;
    margin:0 auto;
    padding:28px 20px 80px;
  }
  h1,h2,h3,h4{margin:0;}
  .fade-in{ animation: fadeInUp 0.55s ease both; }
  @keyframes fadeInUp{
    from{ opacity:0; transform: translateY(14px); }
    to{ opacity:1; transform: translateY(0); }
  }
  .stagger > *{ animation: fadeInUp 0.5s ease both; }
  .stagger > *:nth-child(1){animation-delay:.02s;}
  .stagger > *:nth-child(2){animation-delay:.08s;}
  .stagger > *:nth-child(3){animation-delay:.14s;}
  .stagger > *:nth-child(4){animation-delay:.20s;}
  .stagger > *:nth-child(5){animation-delay:.26s;}
  .stagger > *:nth-child(6){animation-delay:.32s;}

  /* Top bar */
  .topbar{
    display:flex; align-items:center; justify-content:space-between;
    margin-bottom: 22px;
  }
  .brand{ display:flex; align-items:center; gap:10px; }
  .brand-badge{
    width:38px; height:38px; border-radius:10px;
    background: linear-gradient(135deg, var(--accent), var(--accent3));
    display:flex; align-items:center; justify-content:center;
    font-size:18px; flex-shrink:0;
  }
  .brand-name{ font-weight:700; font-size:15px; letter-spacing:0.2px; }
  .brand-sub{ font-size:11px; color:var(--muted); }

  /* Stepper */
  .stepper{
    display:flex; gap:6px; flex-wrap:wrap; margin-bottom:26px;
  }
  .step-pill{
    padding:7px 12px; border-radius:999px; font-size:11.5px; font-weight:600;
    background: var(--card); border:1px solid var(--border); color:var(--muted-dim);
    white-space:nowrap; transition: all .3s ease;
  }
  .step-pill.active{
    background: linear-gradient(135deg, rgba(79,127,255,0.25), rgba(168,85,247,0.2));
    border-color: var(--accent); color:var(--text);
  }
  .step-pill.done{ color:var(--accent2); border-color: rgba(34,211,238,0.35); }

  /* Cards */
  .card{
    background: linear-gradient(180deg, var(--card), var(--bg2));
    border:1px solid var(--border);
    border-radius:16px;
    padding:20px;
    transition: transform .25s ease, border-color .25s ease, box-shadow .25s ease;
  }
  .card:hover{
    transform: translateY(-3px);
    border-color: var(--border-light);
    box-shadow: 0 10px 30px rgba(0,0,0,0.35);
  }
  .grid{
    display:grid; gap:16px;
    grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
  }
  .grid2{
    display:grid; gap:16px;
    grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  }

  .info-box{
    background: rgba(79,127,255,0.08);
    border:1px solid rgba(79,127,255,0.25);
    border-radius:14px;
    padding:16px 18px;
    margin-bottom:22px;
    font-size:13.5px;
    line-height:1.55;
    color:#c7d2ea;
  }
  .info-box b{ color: var(--accent2); }
  .info-label{
    font-size:11px; text-transform:uppercase; letter-spacing:0.8px;
    color: var(--accent2); font-weight:700; margin-bottom:6px; display:block;
  }

  /* Buttons */
  .btn{
    cursor:pointer; border:none; border-radius:12px;
    padding:13px 24px; font-size:14.5px; font-weight:700;
    transition: transform .15s ease, box-shadow .2s ease, opacity .2s ease;
    font-family: inherit;
  }
  .btn:active{ transform: scale(0.97); }
  .btn:disabled{ opacity:0.4; cursor:not-allowed; }
  .btn-primary{
    background: linear-gradient(135deg, var(--accent), var(--accent3));
    color:white; box-shadow: 0 6px 20px rgba(79,127,255,0.35);
  }
  .btn-primary:hover:not(:disabled){ box-shadow: 0 8px 26px rgba(79,127,255,0.5); }
  .btn-ghost{
    background: var(--card); color:var(--text); border:1px solid var(--border-light);
  }
  .btn-ghost:hover:not(:disabled){ background: var(--card-hover); }
  .btn-row{ display:flex; gap:12px; flex-wrap:wrap; margin-top:18px; }

  /* Welcome */
  .welcome-wrap{
    min-height: 76vh; display:flex; flex-direction:column; align-items:center; justify-content:center; text-align:center;
    padding: 40px 16px;
  }
  .welcome-title{
    font-size: clamp(32px, 5.5vw, 56px); font-weight:800; letter-spacing:-1px;
    background: linear-gradient(135deg, #ffffff, var(--accent2) 60%, var(--accent3));
    -webkit-background-clip:text; background-clip:text; color:transparent;
    margin-bottom:14px;
  }
  .welcome-sub{
    font-size:16px; color:var(--muted); max-width:620px; line-height:1.6; margin-bottom:34px;
  }
  .feature-strip{
    display:flex; gap:14px; flex-wrap:wrap; justify-content:center; margin-bottom:36px;
  }
  .feature-chip{
    background: var(--card); border:1px solid var(--border); border-radius:12px;
    padding:10px 16px; font-size:12.5px; color:var(--muted); display:flex; align-items:center; gap:8px;
  }

  /* Metric bars */
  .metric{ margin-bottom:16px; }
  .metric-label{
    display:flex; justify-content:space-between; font-size:13px; margin-bottom:6px; color:var(--muted);
    font-weight:600;
  }
  .metric-label span:last-child{ color: var(--text); font-weight:700; }
  .metric-track{
    height:10px; border-radius:999px; background: rgba(255,255,255,0.06); overflow:hidden;
    border:1px solid var(--border);
  }
  .metric-fill{
    height:100%; border-radius:999px; transition: width 1s cubic-bezier(.4,0,.2,1);
  }

  /* Company cards */
  .stat-card{
    background: var(--card); border:1px solid var(--border); border-radius:14px; padding:16px;
    transition: all .25s ease;
  }
  .stat-card:hover{ border-color: var(--accent); }
  .stat-label{ font-size:11px; color:var(--muted); text-transform:uppercase; letter-spacing:0.6px; margin-bottom:6px; }
  .stat-value{ font-size:20px; font-weight:800; }
  .stat-icon{ font-size:22px; margin-bottom:8px; }

  .badge{
    display:inline-block; padding:4px 12px; border-radius:999px; font-size:11.5px; font-weight:700;
    letter-spacing:0.4px;
  }
  .badge-critical{ background: rgba(239,68,68,0.15); color:#fca5a5; border:1px solid rgba(239,68,68,0.4); }
  .badge-high{ background: rgba(245,158,11,0.15); color:#fcd34d; border:1px solid rgba(245,158,11,0.4); }
  .badge-moderate{ background: rgba(34,211,238,0.15); color:#67e8f9; border:1px solid rgba(34,211,238,0.4); }

  /* Choice cards */
  .choice-card{
    background: var(--card); border:2px solid var(--border); border-radius:14px; padding:16px;
    cursor:pointer; transition: all .2s ease; text-align:left;
  }
  .choice-card:hover{ border-color: var(--border-light); background: var(--card-hover); }
  .choice-card.selected{
    border-color: var(--accent); background: linear-gradient(135deg, rgba(79,127,255,0.12), rgba(168,85,247,0.08));
  }
  .choice-card.disabled{ opacity:0.4; cursor:not-allowed; }
  .choice-title{ font-weight:700; font-size:15px; margin-bottom:6px; }
  .choice-desc{ font-size:12.5px; color:var(--muted); line-height:1.5; margin-bottom:8px; }
  .choice-hint{ font-size:11.5px; color: var(--accent2); font-style:italic; }
  .check-dot{
    width:20px; height:20px; border-radius:6px; border:2px solid var(--border-light);
    display:inline-flex; align-items:center; justify-content:center; font-size:12px; margin-right:8px; flex-shrink:0;
  }
  .choice-card.selected .check-dot{ background: var(--accent); border-color: var(--accent); }

  /* Negotiation */
  .dialogue-box{
    background: linear-gradient(135deg, rgba(168,85,247,0.10), rgba(79,127,255,0.06));
    border:1px solid var(--border-light); border-radius:16px; padding:20px; margin-bottom:20px;
  }
  .option-btn{
    display:block; width:100%; text-align:left; background: var(--card); border:1px solid var(--border);
    border-radius:12px; padding:14px 16px; margin-bottom:10px; cursor:pointer; color:var(--text);
    font-family:inherit; font-size:14px; transition: all .2s ease;
  }
  .option-btn:hover{ border-color: var(--accent); background: var(--card-hover); transform: translateX(3px); }
  .option-note{ font-size:12px; color:var(--muted); margin-top:4px; }

  .feedback-box{
    border-radius:12px; padding:14px 16px; margin-top:14px; font-size:13.5px; line-height:1.5;
    background: rgba(34,211,238,0.08); border:1px solid rgba(34,211,238,0.3);
  }

  /* Dashboard */
  .score-hero{
    text-align:center; padding: 30px 20px; border-radius:20px; margin-bottom:26px;
    background: radial-gradient(circle at 50% 0%, rgba(79,127,255,0.18), transparent 70%), var(--card);
    border:1px solid var(--border-light);
  }
  .score-ring{
    font-size:64px; font-weight:800;
    background: linear-gradient(135deg, var(--accent2), var(--accent));
    -webkit-background-clip:text; background-clip:text; color:transparent;
  }
  .lesson-item{
    display:flex; gap:10px; padding:10px 0; border-bottom:1px solid var(--border); font-size:13.5px; color:#cdd6ea;
  }
  .lesson-item:last-child{ border-bottom:none; }

  ::-webkit-scrollbar{ width:8px; }
  ::-webkit-scrollbar-thumb{ background: var(--border-light); border-radius:8px; }

  @media (max-width: 640px){
    .welcome-title{ font-size:30px; }
    .score-ring{ font-size:48px; }
  }
</style>
</head>
<body>
<div id="root"></div>

<script type="text/babel">
const { useState, useEffect } = React;

/* ---------------- utility ---------------- */
const rand = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;
const pick = (arr) => arr[Math.floor(Math.random() * arr.length)];
const pickN = (arr, n) => {
  const copy = [...arr];
  const out = [];
  for (let i = 0; i < n && copy.length; i++) {
    const idx = Math.floor(Math.random() * copy.length);
    out.push(copy.splice(idx, 1)[0]);
  }
  return out;
};
const clamp = (v, min = 0, max = 100) => Math.max(min, Math.min(max, v));

/* ---------------- data ---------------- */
const INDUSTRIES = ['Consumer Electronics','Automotive Parts','Pharmaceuticals','Fashion & Apparel','Food & Beverage','Industrial Machinery','Semiconductors','Home Appliances','Toys & Games','Renewable Energy Components'];
const NAME_PREFIX = ['Nova','Atlas','Zenith','Orion','Vertex','Summit','Pioneer','Meridian','Horizon','Titan','Quantum','Apex','Falcon','Sterling','Northstar','Vantage','Cobalt'];
const NAME_SUFFIX = ['Industries','Global','Corp','Holdings','Group','Manufacturing','Dynamics','Enterprises','Systems','Works'];
const COUNTRIES = ['USA','Germany','China','Vietnam','Mexico','India','Poland','Brazil','South Korea','Japan','Indonesia','Turkey','Bangladesh','Czech Republic','Thailand'];

function generateCompany(){
  const revenueM = rand(200, 5000);
  return {
    name: `${pick(NAME_PREFIX)} ${pick(NAME_SUFFIX)}`,
    industry: pick(INDUSTRIES),
    revenue: revenueM >= 1000 ? `$${(revenueM/1000).toFixed(1)}B` : `$${revenueM}M`,
    factories: rand(2,12),
    warehouses: rand(3,20),
    suppliers: rand(10,150),
    inventoryDays: rand(15,60),
    leadTime: rand(5,45),
    countries: pickN(COUNTRIES, rand(3,6))
  };
}

const CRISIS_TYPES = [
  { type:'Factory Fire', icon:'🔥', desc:'A major fire has damaged production lines at one of your primary manufacturing facilities, halting output indefinitely.', impact:{cost:-20, inventory:-25, profit:-15, deliverySpeed:-20, customerSatisfaction:-10} },
  { type:'Supplier Bankruptcy', icon:'💼', desc:'One of your critical component suppliers has filed for bankruptcy without warning, cutting off a key input overnight.', impact:{cost:-15, inventory:-30, profit:-10, deliverySpeed:-15, customerSatisfaction:-10} },
  { type:'Port Strike', icon:'🚢', desc:'Dockworkers at a major shipping port have gone on strike, freezing container movement for your imports and exports.', impact:{cost:-10, inventory:-15, profit:-10, deliverySpeed:-30, customerSatisfaction:-15} },
  { type:'Cyberattack', icon:'🛡️', desc:'A ransomware attack has taken down your supply chain management systems, blinding planners to real-time inventory.', impact:{cost:-25, inventory:-10, profit:-20, deliverySpeed:-15, customerSatisfaction:-20} },
  { type:'Flood', icon:'🌊', desc:'Severe flooding has disrupted transport routes and damaged stored inventory at a regional distribution hub.', impact:{cost:-15, inventory:-25, profit:-10, deliverySpeed:-20, customerSatisfaction:-10} },
  { type:'Raw Material Shortage', icon:'⛏️', desc:'A global shortage of a key raw material is driving up input costs and forcing production slowdowns.', impact:{cost:-25, inventory:-20, profit:-15, deliverySpeed:-10, customerSatisfaction:-5} },
  { type:'Political Conflict', icon:'⚠️', desc:'Escalating political tension in a major sourcing region threatens trade routes, tariffs, and border crossings.', impact:{cost:-20, inventory:-10, profit:-15, deliverySpeed:-15, customerSatisfaction:-10} },
  { type:'Shipping Delay', icon:'📦', desc:'Ocean vessel delays have pushed lead times far beyond plan, leaving shelves and production lines waiting.', impact:{cost:-10, inventory:-15, profit:-5, deliverySpeed:-30, customerSatisfaction:-15} },
];
const URGENCY = [
  {label:'Moderate', mult:0.7, className:'badge-moderate'},
  {label:'High', mult:1.0, className:'badge-high'},
  {label:'Critical', mult:1.3, className:'badge-critical'},
];

function generateCrisis(){
  const base = pick(CRISIS_TYPES);
  const urgency = pick(URGENCY);
  return {
    ...base,
    urgency: urgency.label,
    urgencyClass: urgency.className,
    mult: urgency.mult,
    financialImpact: Math.round(rand(5,150) * urgency.mult),
    delayDays: Math.round(rand(3,45) * urgency.mult),
    affectedPercent: Math.round(rand(10,70) * urgency.mult > 100 ? 95 : rand(10,70) * urgency.mult),
  };
}

const WAR_ROOM_ACTIONS = [
  { id:'air', title:'Expedite Air Freight', icon:'✈️', desc:'Fly critical components in instead of waiting on ocean freight.',
    hint:'Fast, but expensive. Great when speed matters more than margin.',
    effects:{cost:-15, inventory:5, profit:-5, deliverySpeed:22, customerSatisfaction:8}, resilience:5, riskManagement:0 },
  { id:'backup', title:'Activate Backup Suppliers', icon:'🔗', desc:'Bring pre-vetted secondary suppliers online to fill the gap.',
    hint:'Builds long-term resilience, though onboarding costs a little now.',
    effects:{cost:-8, inventory:18, profit:-4, deliverySpeed:6, customerSatisfaction:5}, resilience:20, riskManagement:15 },
  { id:'ration', title:'Ration Inventory to Key Accounts', icon:'⚖️', desc:'Protect your highest-value customers first; let smaller orders wait.',
    hint:'Protects revenue concentration, but frustrates smaller customers.',
    effects:{cost:5, inventory:10, profit:10, deliverySpeed:-5, customerSatisfaction:-15}, resilience:0, riskManagement:5 },
  { id:'emergency', title:'Sign Emergency Contracts', icon:'📝', desc:'Pay premium rates to lock in short-term supply guarantees.',
    hint:'Solves the immediate gap fast, at a real cost to margin.',
    effects:{cost:-20, inventory:12, profit:-12, deliverySpeed:12, customerSatisfaction:6}, resilience:5, riskManagement:10 },
  { id:'stock', title:'Increase Safety Stock via Financing', icon:'🏦', desc:'Borrow short-term capital to build a larger buffer of inventory.',
    hint:'Cushions future shocks, but interest and carrying cost bite profit.',
    effects:{cost:-15, inventory:25, profit:-15, deliverySpeed:3, customerSatisfaction:4}, resilience:15, riskManagement:5 },
  { id:'comm', title:'Communicate Transparently with Customers', icon:'📣', desc:'Proactively notify customers of delays and set honest expectations.',
    hint:'Cheap and builds trust — rarely a wrong move, but it does not fix supply.',
    effects:{cost:-3, inventory:0, profit:0, deliverySpeed:0, customerSatisfaction:20}, resilience:5, riskManagement:5 },
];

const NEGOTIATION_ROUNDS = [
  {
    prompt:"Round 1 — Your key supplier, hit hard by the crisis, opens with a demand for a 20% price increase to keep supplying you at all.",
    why:"Why this matters: how you open a negotiation sets the tone for trust and price for every round that follows.",
    options:[
      { text:'Accept the increase immediately to guarantee supply.', trust:15, price:20, leadTime:-5, note:'Fast relief, but you just signaled you will pay anything.' },
      { text:'Counter with data showing market rates are lower.', trust:5, price:8, leadTime:0, note:'Firm but fair — keeps the relationship professional.' },
      { text:'Propose a longer-term contract in exchange for a smaller increase.', trust:20, price:10, leadTime:-8, note:'Trades short-term pain for long-term stability on both sides.' },
      { text:'Threaten to move volume to a competitor immediately.', trust:-15, price:-5, leadTime:15, note:'May shrink the price hike, but trust takes a real hit.' },
    ]
  },
  {
    prompt:"Round 2 — Citing their own cash flow crunch, the supplier asks for 50% payment upfront before shipping anything.",
    why:"Why this matters: cash terms affect your working capital and signal how much financial risk you're willing to absorb for them.",
    options:[
      { text:'Agree to the upfront payment to keep things moving.', trust:12, price:5, leadTime:-6, note:'Improves goodwill, but ties up your own cash.' },
      { text:'Offer 20% upfront with the rest on delivery.', trust:6, price:2, leadTime:-2, note:'A balanced middle ground both sides can usually live with.' },
      { text:'Refuse upfront payment entirely, citing standard terms.', trust:-8, price:3, leadTime:10, note:'Protects your cash position but slows the relationship.' },
      { text:'Offer a small early-payment discount instead of full upfront cash.', trust:8, price:-4, leadTime:-3, note:'Creative structuring — often a smart way to build goodwill cheaply.' },
    ]
  },
  {
    prompt:"Round 3 — The supplier offers to expedite your shipment for an extra rush fee, or run it on the normal (slower) schedule.",
    why:"Why this matters: speed and cost are almost always a trade-off — this round tests your read on that balance.",
    options:[
      { text:'Pay the rush fee — speed matters more right now.', trust:5, price:12, leadTime:-15, note:'Gets product moving fast, at a real cost premium.' },
      { text:'Decline the rush fee and accept the normal timeline.', trust:2, price:0, leadTime:8, note:'Saves money but stretches your recovery timeline.' },
      { text:'Ask them to split the rush fee 50/50.', trust:10, price:6, leadTime:-10, note:'Shows good faith while sharing the financial burden.' },
      { text:'Request expedited shipping only for your top SKUs.', trust:7, price:4, leadTime:-8, note:'A smart, targeted compromise that protects your best sellers.' },
    ]
  },
  {
    prompt:"Round 4 — Final terms. The supplier is ready to sign — but the exact language around price, volume, and lead time is still open.",
    why:"Why this matters: the final round locks in the numbers you'll live with for the length of the contract.",
    options:[
      { text:'Push hard for the best possible terms across the board.', trust:-10, price:-10, leadTime:-5, note:'Could win big, but risks souring the deal at the last moment.' },
      { text:'Accept fair terms that reflect the conversation so far.', trust:15, price:0, leadTime:-5, note:'A balanced close that preserves the relationship.' },
      { text:'Lock in price certainty, trading away some lead-time flexibility.', trust:8, price:-8, leadTime:8, note:'Protects your margin, at the cost of some schedule flexibility.' },
      { text:'Lock in speed certainty, accepting a slightly higher price.', trust:8, price:8, leadTime:-12, note:'Protects your delivery promise, at the cost of some margin.' },
    ]
  },
];

const BOARDROOM_QUESTIONS = [
  {
    q:"Your CFO wants to cut marketing spend mid-crisis to preserve cash, right as customers grow anxious about delays.",
    why:"Why this matters: leaders are judged on how they balance short-term cash needs against long-term brand trust.",
    options:[
      { text:'Cut marketing spend fully as the CFO suggests.', points:3, feedback:'Protects cash, but leaves anxious customers with no reassurance.' },
      { text:'Keep marketing spend flat and redirect it toward proactive customer communication.', points:9, feedback:'Smart reallocation — the same budget now builds trust instead of driving sales.' },
      { text:'Increase marketing spend to reassure the market.', points:5, feedback:'Bold, but risks looking tone-deaf if cash is genuinely tight.' },
      { text:'Let the CFO and marketing lead fight it out without your input.', points:1, feedback:'Avoiding the decision leaves the company directionless at a critical moment.' },
    ]
  },
  {
    q:"A journalist requests an on-record statement about the crisis's impact on your supply chain.",
    why:"Why this matters: what a CEO says publicly during a crisis shapes customer, investor, and employee confidence for months.",
    options:[
      { text:'Decline to comment entirely.', points:3, feedback:'Silence often reads as evasive and can fuel speculation.' },
      { text:'Give a short, honest statement acknowledging the issue and your response plan.', points:9, feedback:'Transparency paired with a plan is the gold standard in crisis communication.' },
      { text:'Downplay the severity of the situation publicly.', points:2, feedback:'Risky — if the truth emerges later, credibility takes a bigger hit.' },
      { text:'Overpromise a fast, full recovery to sound confident.', points:4, feedback:'Confidence helps, but overpromising can backfire if timelines slip.' },
    ]
  },
  {
    q:"Your operations team says pushing through the crisis this way will require costly overtime pay.",
    why:"Why this matters: leaders constantly weigh short-term budget discipline against operational continuity.",
    options:[
      { text:'Approve the overtime without question to keep operations moving.', points:6, feedback:'Keeps things running, but unchecked costs can spiral quickly.' },
      { text:'Approve overtime only for the most critical production lines.', points:9, feedback:'A targeted approach — protects the essentials while controlling cost.' },
      { text:'Deny the overtime request to protect the budget.', points:2, feedback:'Saves money now, but risks deepening delays and customer frustration.' },
      { text:'Ask the team to find volunteers for overtime instead of mandating it.', points:5, feedback:'Respects morale, but may not guarantee the coverage you need.' },
    ]
  },
  {
    q:"An employee flags a shortcut that bends a minor safety protocol but would meaningfully speed up recovery.",
    why:"Why this matters: crises tempt leaders to cut corners — how you respond signals your real priorities.",
    options:[
      { text:'Approve the shortcut — speed matters most right now.', points:1, feedback:'Risky precedent — safety shortcuts can create far bigger problems later.' },
      { text:'Reject the shortcut and look for a compliant way to speed things up.', points:9, feedback:'Protects the company and its people while still pushing for pace.' },
      { text:'Approve it quietly just this once, without telling anyone.', points:0, feedback:'Hidden corner-cutting is one of the riskiest choices a leader can make.' },
      { text:'Escalate the idea to a safety review board before deciding.', points:7, feedback:'A measured approach, though it may cost you some valuable time.' },
    ]
  },
  {
    q:"Post-crisis, you have unexpected savings from the response effort. Reinvest in resilience, or return it to shareholders?",
    why:"Why this matters: this decision reveals whether leadership is playing for the next quarter or the next decade.",
    options:[
      { text:'Return all of it to shareholders as a special dividend.', points:3, feedback:'Popular short-term, but leaves the company just as exposed to the next shock.' },
      { text:'Invest the majority into supply chain resilience and risk monitoring.', points:9, feedback:'A forward-looking move that reduces the odds of repeating this crisis.' },
      { text:'Split it evenly between shareholders and resilience investment.', points:7, feedback:'A reasonable balance between rewarding investors and building strength.' },
      { text:'Sit on the cash and decide later.', points:2, feedback:'Indecision here wastes a rare opportunity to convert crisis into capability.' },
    ]
  },
];

const AI_INVESTMENTS = [
  { id:'demand', name:'Demand Forecasting', icon:'📈', desc:'Machine learning models that predict customer demand before it happens.',
    impact:'Reduces stockouts and overproduction by anticipating shifts in demand.',
    resilience:15, costControl:5, riskManagement:10, customerSatisfaction:10 },
  { id:'inventory', name:'Inventory Optimization', icon:'📦', desc:'Algorithms that right-size stock levels across every warehouse.',
    impact:'Frees up cash trapped in excess inventory while avoiding shortages.',
    resilience:10, costControl:20, riskManagement:5, customerSatisfaction:5 },
  { id:'supplierrisk', name:'Supplier Risk Monitoring', icon:'🧭', desc:'Continuous scanning of supplier financial health, geopolitics, and news signals.',
    impact:'Flags the next supplier bankruptcy or disruption weeks before it hits.',
    resilience:15, costControl:0, riskManagement:25, customerSatisfaction:0 },
  { id:'warehouse', name:'Warehouse Vision', icon:'🎥', desc:'Computer vision systems that track inventory accuracy and safety in real time.',
    impact:'Cuts picking errors and mis-ships that quietly erode customer trust.',
    resilience:5, costControl:10, riskManagement:5, customerSatisfaction:15 },
  { id:'procurement', name:'Procurement Copilot', icon:'🤝', desc:'An AI assistant that drafts contracts, benchmarks pricing, and flags risky clauses.',
    impact:'Speeds up negotiations and keeps buyers from overpaying under pressure.',
    resilience:10, costControl:15, riskManagement:10, customerSatisfaction:0 },
];

/* ---------------- reusable bits ---------------- */
function MetricBar({ label, value, color }) {
  const [width, setWidth] = useState(0);
  useEffect(() => {
    const t = setTimeout(() => setWidth(value), 80);
    return () => clearTimeout(t);
  }, [value]);
  return (
    <div className="metric">
      <div className="metric-label"><span>{label}</span><span>{Math.round(value)}%</span></div>
      <div className="metric-track">
        <div className="metric-fill" style={{ width: width + '%', background: color }}></div>
      </div>
    </div>
  );
}

const STEPS = ['Welcome','Company','Crisis','War Room','Negotiation','Boardroom','AI Strategy','Dashboard'];

function Stepper({ current }) {
  return (
    <div className="stepper">
      {STEPS.map((s, i) => (
        <div key={s} className={'step-pill ' + (i === current ? 'active' : i < current ? 'done' : '')}>
          {i < current ? '✓ ' : ''}{s}
        </div>
      ))}
    </div>
  );
}

function TopBar() {
  return (
    <div className="topbar">
      <div className="brand">
        <div className="brand-badge">🧭</div>
        <div>
          <div className="brand-name">Operation Lifeline</div>
          <div className="brand-sub">Supply Chain Crisis Lab</div>
        </div>
      </div>
    </div>
  );
}

/* ---------------- screens ---------------- */

function Welcome({ onStart }) {
  return (
    <div className="welcome-wrap fade-in">
      <div style={{fontSize:'52px', marginBottom:'10px'}}>🧭</div>
      <div className="welcome-title">Operation Lifeline</div>
      <div className="welcome-sub">
        Supply Chain Crisis Lab — step into the shoes of a Chief Supply Chain Officer.
        A random company, a random crisis, and a full day of high-stakes decisions:
        war room triage, supplier negotiation, boardroom leadership, and AI strategy.
        Every playthrough is different. Every decision has a consequence.
      </div>
      <div className="feature-strip">
        <div className="feature-chip">🏭 Random Company</div>
        <div className="feature-chip">🔥 Random Crisis</div>
        <div className="feature-chip">📊 Live Metrics</div>
        <div className="feature-chip">🤝 Branching Negotiation</div>
        <div className="feature-chip">🧠 Leadership Scoring</div>
      </div>
      <button className="btn btn-primary" onClick={onStart} style={{fontSize:'16px', padding:'16px 34px'}}>
        Start Simulation →
      </button>
    </div>
  );
}

function CompanyReveal({ company, onNext }) {
  const stats = [
    { label:'Industry', value: company.industry, icon:'🏷️' },
    { label:'Annual Revenue', value: company.revenue, icon:'💰' },
    { label:'Factories', value: company.factories, icon:'🏭' },
    { label:'Warehouses', value: company.warehouses, icon:'🏬' },
    { label:'Active Suppliers', value: company.suppliers, icon:'🔗' },
    { label:'Inventory Days on Hand', value: company.inventoryDays + ' days', icon:'📦' },
    { label:'Avg. Supplier Lead Time', value: company.leadTime + ' days', icon:'⏱️' },
    { label:'Sourcing Countries', value: company.countries.length, icon:'🌍' },
  ];
  return (
    <div className="fade-in">
      <div className="info-box">
        <span className="info-label">Why this matters</span>
        Every supply chain decision only makes sense in context. Before you can respond to a crisis,
        you need to understand the shape of the business you're running — how big it is, how lean its
        inventory buffers are, and how spread out its supplier network is. Study the profile below.
      </div>
      <h2 style={{fontSize:'26px', marginBottom:'4px'}}>{company.name}</h2>
      <div style={{color:'var(--muted)', marginBottom:'20px', fontSize:'14px'}}>
        Sourcing from: {company.countries.join(', ')}
      </div>
      <div className="grid stagger">
        {stats.map((s) => (
          <div className="stat-card" key={s.label}>
            <div className="stat-icon">{s.icon}</div>
            <div className="stat-label">{s.label}</div>
            <div className="stat-value">{s.value}</div>
          </div>
        ))}
      </div>
      <div className="btn-row">
        <button className="btn btn-primary" onClick={onNext}>Continue to Crisis Briefing →</button>
      </div>
    </div>
  );
}

function CrisisReveal({ crisis, company, onNext }) {
  return (
    <div className="fade-in">
      <div className="info-box">
        <span className="info-label">Why this matters</span>
        Every crisis has a different shape — some hit your inventory hardest, others hit delivery
        speed or customer trust. Reading the briefing carefully will help you choose the right
        response actions in the War Room next.
      </div>
      <div className="card" style={{padding:'28px'}}>
        <div style={{display:'flex', alignItems:'center', gap:'14px', marginBottom:'14px', flexWrap:'wrap'}}>
          <div style={{fontSize:'40px'}}>{crisis.icon}</div>
          <div>
            <h2 style={{fontSize:'24px'}}>{crisis.type}</h2>
            <span className={'badge ' + crisis.urgencyClass}>{crisis.urgency} Urgency</span>
          </div>
        </div>
        <p style={{fontSize:'15px', lineHeight:'1.6', color:'#d3dcf0', marginBottom:'20px'}}>
          {crisis.desc} This is unfolding right now at <b>{company.name}</b>, a {company.industry.toLowerCase()} business.
        </p>
        <div className="grid">
          <div className="stat-card">
            <div className="stat-label">Estimated Financial Impact</div>
            <div className="stat-value" style={{color:'var(--bad)'}}>${crisis.financialImpact}M</div>
          </div>
          <div className="stat-card">
            <div className="stat-label">Projected Delay</div>
            <div className="stat-value" style={{color:'var(--warn)'}}>{crisis.delayDays} days</div>
          </div>
          <div className="stat-card">
            <div className="stat-label">Network Affected</div>
            <div className="stat-value">{crisis.affectedPercent}%</div>
          </div>
        </div>
      </div>
      <div className="btn-row">
        <button className="btn btn-primary" onClick={onNext}>Enter the War Room →</button>
      </div>
    </div>
  );
}

function WarRoom({ crisis, metrics, setMetrics, warRoomChoices, setWarRoomChoices, onNext }) {
  const [simulated, setSimulated] = useState(false);

  const toggle = (id) => {
    if (simulated) return;
    setWarRoomChoices((prev) => {
      if (prev.includes(id)) return prev.filter((x) => x !== id);
      if (prev.length >= 3) return prev;
      return [...prev, id];
    });
  };

  const simulate = () => {
    let m = { ...metrics };
    warRoomChoices.forEach((id) => {
      const action = WAR_ROOM_ACTIONS.find((a) => a.id === id);
      Object.keys(action.effects).forEach((k) => {
        m[k] = clamp(m[k] + action.effects[k]);
      });
    });
    setMetrics(m);
    setSimulated(true);
  };

  const colorFor = (key) => ({
    cost: 'linear-gradient(90deg,#f59e0b,#fbbf24)',
    inventory: 'linear-gradient(90deg,#22d3ee,#4f7fff)',
    profit: 'linear-gradient(90deg,#22c55e,#4ade80)',
    deliverySpeed: 'linear-gradient(90deg,#a855f7,#c084fc)',
    customerSatisfaction: 'linear-gradient(90deg,#4f7fff,#22d3ee)',
  }[key]);

  return (
    <div className="fade-in">
      <div className="info-box">
        <span className="info-label">Why this matters</span>
        In a real crisis you never get to do everything — budget, time, and people are limited.
        Choose exactly <b>3 of the 6</b> response actions below. Each one trades something for
        something else: watch how Cost, Inventory, Profit, Delivery Speed, and Customer Satisfaction
        shift once you simulate your response.
      </div>

      <h3 style={{marginBottom:'12px'}}>Choose 3 Response Actions ({warRoomChoices.length}/3 selected)</h3>
      <div className="grid2 stagger" style={{marginBottom:'24px'}}>
        {WAR_ROOM_ACTIONS.map((a) => {
          const selected = warRoomChoices.includes(a.id);
          const disabled = simulated || (!selected && warRoomChoices.length >= 3);
          return (
            <div
              key={a.id}
              className={'choice-card' + (selected ? ' selected' : '') + (disabled && !selected ? ' disabled' : '')}
              onClick={() => toggle(a.id)}
            >
              <div style={{display:'flex', alignItems:'center', marginBottom:'8px'}}>
                <span className="check-dot">{selected ? '✓' : ''}</span>
                <span className="choice-title">{a.icon} {a.title}</span>
              </div>
              <div className="choice-desc">{a.desc}</div>
              <div className="choice-hint">{a.hint}</div>
            </div>
          );
        })}
      </div>

      <h3 style={{marginBottom:'12px'}}>Live Business Metrics</h3>
      <div className="card">
        <MetricBar label="Cost" value={metrics.cost} color={colorFor('cost')} />
        <MetricBar label="Inventory" value={metrics.inventory} color={colorFor('inventory')} />
        <MetricBar label="Profit" value={metrics.profit} color={colorFor('profit')} />
        <MetricBar label="Delivery Speed" value={metrics.deliverySpeed} color={colorFor('deliverySpeed')} />
        <MetricBar label="Customer Satisfaction" value={metrics.customerSatisfaction} color={colorFor('customerSatisfaction')} />
      </div>

      <div className="btn-row">
        {!simulated ? (
          <button className="btn btn-primary" disabled={warRoomChoices.length !== 3} onClick={simulate}>
            Simulate Response →
          </button>
        ) : (
          <button className="btn btn-primary" onClick={onNext}>Continue to Negotiation →</button>
        )}
      </div>
    </div>
  );
}

function Negotiation({ negotiation, setNegotiation, onNext }) {
  const { round, trust, log } = negotiation;
  const finished = round >= NEGOTIATION_ROUNDS.length;

  const choose = (opt) => {
    setNegotiation((prev) => ({
      ...prev,
      trust: clamp(prev.trust + opt.trust),
      price: prev.price + opt.price,
      leadTime: prev.leadTime + opt.leadTime,
      round: prev.round + 1,
      log: [...prev.log, { roundPrompt: NEGOTIATION_ROUNDS[prev.round].prompt, choice: opt.text, note: opt.note }],
    }));
  };

  const negotiationScore = clamp(Math.round(trust - negotiation.price * 0.8 - negotiation.leadTime * 0.6));

  return (
    <div className="fade-in">
      <div className="info-box">
        <span className="info-label">Why this matters</span>
        Supplier negotiations are rarely one-shot. Trust built (or burned) in early rounds shapes
        what's possible later. Watch how Trust, Price, and Lead Time shift with every choice across
        these four rounds.
      </div>

      <div className="grid" style={{marginBottom:'20px'}}>
        <div className="stat-card">
          <div className="stat-label">Supplier Trust</div>
          <div className="stat-value">{Math.round(trust)}/100</div>
        </div>
        <div className="stat-card">
          <div className="stat-label">Cumulative Price Change</div>
          <div className="stat-value" style={{color: negotiation.price > 0 ? 'var(--bad)' : 'var(--good)'}}>
            {negotiation.price > 0 ? '+' : ''}{negotiation.price}%
          </div>
        </div>
        <div className="stat-card">
          <div className="stat-label">Cumulative Lead Time Change</div>
          <div className="stat-value" style={{color: negotiation.leadTime > 0 ? 'var(--bad)' : 'var(--good)'}}>
            {negotiation.leadTime > 0 ? '+' : ''}{negotiation.leadTime} days
          </div>
        </div>
      </div>

      {!finished ? (
        <div className="dialogue-box">
          <div style={{fontSize:'11px', color:'var(--accent2)', fontWeight:700, marginBottom:'8px', textTransform:'uppercase'}}>
            Round {round + 1} of {NEGOTIATION_ROUNDS.length}
          </div>
          <p style={{fontSize:'15px', lineHeight:'1.6', marginBottom:'8px'}}>{NEGOTIATION_ROUNDS[round].prompt}</p>
          <p style={{fontSize:'12.5px', color:'var(--muted)', marginBottom:'18px', fontStyle:'italic'}}>{NEGOTIATION_ROUNDS[round].why}</p>
          {NEGOTIATION_ROUNDS[round].options.map((opt, i) => (
            <button key={i} className="option-btn" onClick={() => choose(opt)}>
              {opt.text}
            </button>
          ))}
        </div>
      ) : (
        <div className="card">
          <h3 style={{marginBottom:'10px'}}>Negotiation Complete</h3>
          <div className="feedback-box">
            Final Negotiation Score: <b>{negotiationScore}/100</b>
          </div>
          <div style={{marginTop:'16px'}}>
            {log.map((l, i) => (
              <div key={i} className="lesson-item">
                <span>🗒️</span>
                <span><b>Round {i+1}:</b> {l.choice} <br/><span style={{color:'var(--muted)'}}>{l.note}</span></span>
              </div>
            ))}
          </div>
        </div>
      )}

      {finished && (
        <div className="btn-row">
          <button className="btn btn-primary" onClick={onNext}>Continue to Boardroom →</button>
        </div>
      )}
    </div>
  );
}

function Boardroom({ boardroomIndex, setBoardroomIndex, boardroomScore, setBoardroomScore, onNext }) {
  const [answered, setAnswered] = useState(null);
  const finished = boardroomIndex >= BOARDROOM_QUESTIONS.length;
  const current = !finished ? BOARDROOM_QUESTIONS[boardroomIndex] : null;

  const choose = (opt) => {
    if (answered) return;
    setAnswered(opt);
    setBoardroomScore((s) => s + opt.points);
  };

  const next = () => {
    setAnswered(null);
    setBoardroomIndex((i) => i + 1);
  };

  return (
    <div className="fade-in">
      <div className="info-box">
        <span className="info-label">Why this matters</span>
        The best supply chain strategy in the world falls apart without steady leadership.
        These five questions test how you balance cost, honesty, safety, and long-term thinking
        under pressure.
      </div>

      {!finished ? (
        <div className="dialogue-box">
          <div style={{fontSize:'11px', color:'var(--accent2)', fontWeight:700, marginBottom:'8px', textTransform:'uppercase'}}>
            Question {boardroomIndex + 1} of {BOARDROOM_QUESTIONS.length}
          </div>
          <p style={{fontSize:'15px', lineHeight:'1.6', marginBottom:'8px'}}>{current.q}</p>
          <p style={{fontSize:'12.5px', color:'var(--muted)', marginBottom:'18px', fontStyle:'italic'}}>{current.why}</p>
          {current.options.map((opt, i) => (
            <div key={i}>
              <button
                className="option-btn"
                onClick={() => choose(opt)}
                style={answered === opt ? { borderColor:'var(--accent)', background:'var(--card-hover)' } : {}}
                disabled={!!answered && answered !== opt}
              >
                {opt.text}
              </button>
            </div>
          ))}
          {answered && (
            <div className="feedback-box">{answered.feedback}</div>
          )}
          {answered && (
            <div className="btn-row">
              <button className="btn btn-primary" onClick={next}>
                {boardroomIndex === BOARDROOM_QUESTIONS.length - 1 ? 'See Leadership Summary →' : 'Next Question →'}
              </button>
            </div>
          )}
        </div>
      ) : (
        <div className="card">
          <h3 style={{marginBottom:'10px'}}>Boardroom Complete</h3>
          <div className="feedback-box">
            Leadership Score: <b>{Math.round(boardroomScore / (BOARDROOM_QUESTIONS.length * 10) * 100)}/100</b>
          </div>
          <div className="btn-row">
            <button className="btn btn-primary" onClick={onNext}>Continue to AI Strategy →</button>
          </div>
        </div>
      )}
    </div>
  );
}

function AIStrategy({ aiChoices, setAiChoices, onNext }) {
  const toggle = (id) => {
    setAiChoices((prev) => {
      if (prev.includes(id)) return prev.filter((x) => x !== id);
      if (prev.length >= 2) return prev;
      return [...prev, id];
    });
  };

  return (
    <div className="fade-in">
      <div className="info-box">
        <span className="info-label">Why this matters</span>
        No company can fund every AI initiative at once. Choose the <b>2 investments</b> you believe
        will build the most resilience for the future — each one improves different parts of the
        business in different ways.
      </div>

      <h3 style={{marginBottom:'12px'}}>Choose 2 AI Investments ({aiChoices.length}/2 selected)</h3>
      <div className="grid2 stagger">
        {AI_INVESTMENTS.map((a) => {
          const selected = aiChoices.includes(a.id);
          const disabled = !selected && aiChoices.length >= 2;
          return (
            <div
              key={a.id}
              className={'choice-card' + (selected ? ' selected' : '') + (disabled ? ' disabled' : '')}
              onClick={() => !disabled && toggle(a.id)}
            >
              <div style={{display:'flex', alignItems:'center', marginBottom:'8px'}}>
                <span className="check-dot">{selected ? '✓' : ''}</span>
                <span className="choice-title">{a.icon} {a.name}</span>
              </div>
              <div className="choice-desc">{a.desc}</div>
              <div className="choice-hint">Expected impact: {a.impact}</div>
            </div>
          );
        })}
      </div>

      <div className="btn-row">
        <button className="btn btn-primary" disabled={aiChoices.length !== 2} onClick={onNext}>
          Continue to Final Dashboard →
        </button>
      </div>
    </div>
  );
}

function FinalDashboard({ company, crisis, metrics, warRoomChoices, negotiation, boardroomScore, aiChoices, onReplay }) {
  // Leadership
  const leadership = clamp(Math.round(boardroomScore / (BOARDROOM_QUESTIONS.length * 10) * 100));

  // Negotiation
  const negotiationScore = clamp(Math.round(negotiation.trust - negotiation.price * 0.8 - negotiation.leadTime * 0.6));

  // Aggregate AI contributions
  const aiTotals = { resilience:0, costControl:0, riskManagement:0, customerSatisfaction:0 };
  aiChoices.forEach((id) => {
    const inv = AI_INVESTMENTS.find((a) => a.id === id);
    aiTotals.resilience += inv.resilience;
    aiTotals.costControl += inv.costControl;
    aiTotals.riskManagement += inv.riskManagement;
    aiTotals.customerSatisfaction += inv.customerSatisfaction;
  });

  // Aggregate war room contributions
  const warTotals = { resilience:0, riskManagement:0 };
  warRoomChoices.forEach((id) => {
    const a = WAR_ROOM_ACTIONS.find((x) => x.id === id);
    warTotals.resilience += a.resilience;
    warTotals.riskManagement += a.riskManagement;
  });

  const resilience = clamp(Math.round(30 + warTotals.resilience + aiTotals.resilience + (metrics.deliverySpeed - 50) * 0.2));
  const costControl = clamp(Math.round(metrics.cost * 0.7 + aiTotals.costControl * 1.2));
  const riskManagement = clamp(Math.round(25 + warTotals.riskManagement + aiTotals.riskManagement + (negotiationScore - 50) * 0.2));
  const customerSatisfaction = clamp(Math.round(metrics.customerSatisfaction * 0.7 + aiTotals.customerSatisfaction * 1.3));

  const overall = clamp(Math.round(
    leadership * 0.2 +
    negotiationScore * 0.15 +
    resilience * 0.2 +
    costControl * 0.15 +
    riskManagement * 0.15 +
    customerSatisfaction * 0.15
  ));

  const categories = [
    { key:'Leadership', value: leadership },
    { key:'Negotiation', value: negotiationScore },
    { key:'Resilience', value: resilience },
    { key:'Cost Control', value: costControl },
    { key:'Risk Management', value: riskManagement },
    { key:'Customer Satisfaction', value: customerSatisfaction },
  ];
  const best = categories.reduce((a, b) => (b.value > a.value ? b : a));
  const worst = categories.reduce((a, b) => (b.value < a.value ? b : a));

  let verdict, verdictColor;
  if (overall >= 85) { verdict = "Exceptional crisis leadership. You navigated disruption like a seasoned CSCO."; verdictColor = 'var(--good)'; }
  else if (overall >= 70) { verdict = "Strong performance overall, with a few areas that could still be sharpened."; verdictColor = 'var(--accent2)'; }
  else if (overall >= 50) { verdict = "A workable outcome, but the crisis exposed real gaps in your response."; verdictColor = 'var(--warn)'; }
  else { verdict = "This crisis hit harder than your response could absorb. There's a lot to learn here."; verdictColor = 'var(--bad)'; }

  const recommendationMap = {
    'Leadership': 'Invest in decision-making frameworks and crisis communication training for your executive team.',
    'Negotiation': 'Build stronger supplier relationships during calm periods, not just during a crisis — trust is cheaper to build early.',
    'Resilience': 'Diversify your supplier base and pre-qualify backups before the next disruption hits.',
    'Cost Control': 'Introduce tighter scenario-based budgeting so emergency spend doesn\'t quietly erode margin.',
    'Risk Management': 'Deploy continuous supplier and geopolitical risk monitoring so early warning signs surface sooner.',
    'Customer Satisfaction': 'Formalize a proactive customer communication playbook for the next disruption.',
  };

  const lessonsPool = [
    "Speed and cost are almost always in tension — the fastest fix is rarely the cheapest one.",
    "Trust built with suppliers before a crisis pays dividends when you need flexibility most.",
    "Transparent communication with customers costs little and protects long-term loyalty.",
    "Diversified sourcing reduces how hard any single disruption can hit your operations.",
    "Leadership decisions made under pressure often matter more than the crisis itself.",
    "AI-driven visibility turns reactive firefighting into proactive risk management.",
    "Cash discipline during a crisis prevents a second, financial crisis from following the first.",
  ];
  const lessons = pickN(lessonsPool, 4);

  return (
    <div className="fade-in">
      <div className="score-hero">
        <div style={{fontSize:'13px', color:'var(--muted)', marginBottom:'6px', textTransform:'uppercase', letterSpacing:'1px'}}>
          Overall Crisis Score
        </div>
        <div className="score-ring">{overall}</div>
        <div style={{color: verdictColor, fontWeight:700, marginTop:'10px', fontSize:'15px'}}>{verdict}</div>
      </div>

      <div className="card" style={{marginBottom:'20px'}}>
        <h3 style={{marginBottom:'14px'}}>Performance Breakdown</h3>
        <MetricBar label="Leadership" value={leadership} color="linear-gradient(90deg,#4f7fff,#a855f7)" />
        <MetricBar label="Negotiation" value={negotiationScore} color="linear-gradient(90deg,#22d3ee,#4f7fff)" />
        <MetricBar label="Resilience" value={resilience} color="linear-gradient(90deg,#22c55e,#4ade80)" />
        <MetricBar label="Cost Control" value={costControl} color="linear-gradient(90deg,#f59e0b,#fbbf24)" />
        <MetricBar label="Risk Management" value={riskManagement} color="linear-gradient(90deg,#a855f7,#c084fc)" />
        <MetricBar label="Customer Satisfaction" value={customerSatisfaction} color="linear-gradient(90deg,#4f7fff,#22d3ee)" />
      </div>

      <div className="grid2" style={{marginBottom:'20px'}}>
        <div className="card">
          <h4 style={{marginBottom:'10px', color:'var(--bad)'}}>⚠️ Biggest Weak Spot</h4>
          <p style={{fontSize:'14px', lineHeight:'1.6', color:'#d3dcf0'}}>
            <b>{worst.key}</b> scored lowest at {worst.value}/100. During the {crisis.type.toLowerCase()} at {company.name}, this
            is the area that held your overall response back the most.
          </p>
        </div>
        <div className="card">
          <h4 style={{marginBottom:'10px', color:'var(--good)'}}>✅ Best Decision Area</h4>
          <p style={{fontSize:'14px', lineHeight:'1.6', color:'#d3dcf0'}}>
            <b>{best.key}</b> scored highest at {best.value}/100 — this was the strongest part of how you
            handled the crisis.
          </p>
        </div>
      </div>

      <div className="card" style={{marginBottom:'20px'}}>
        <h4 style={{marginBottom:'10px', color:'var(--accent2)'}}>🎯 Expert Recommendation</h4>
        <p style={{fontSize:'14px', lineHeight:'1.6', color:'#d3dcf0'}}>{recommendationMap[worst.key]}</p>
      </div>

      <div className="card" style={{marginBottom:'26px'}}>
        <h4 style={{marginBottom:'6px'}}>📚 Lessons Learned</h4>
        {lessons.map((l, i) => (
          <div key={i} className="lesson-item"><span>💡</span><span>{l}</span></div>
        ))}
      </div>

      <div className="btn-row">
        <button className="btn btn-primary" onClick={onReplay}>🔁 Replay Simulation</button>
      </div>
    </div>
  );
}

/* ---------------- app root ---------------- */

const initialMetrics = () => ({ cost:65, inventory:65, profit:65, deliverySpeed:65, customerSatisfaction:65 });

function App() {
  const [screen, setScreen] = useState('welcome');
  const [company, setCompany] = useState(null);
  const [crisis, setCrisis] = useState(null);
  const [metrics, setMetrics] = useState(initialMetrics());
  const [warRoomChoices, setWarRoomChoices] = useState([]);
  const [negotiation, setNegotiation] = useState({ trust:50, price:0, leadTime:0, round:0, log:[] });
  const [boardroomIndex, setBoardroomIndex] = useState(0);
  const [boardroomScore, setBoardroomScore] = useState(0);
  const [aiChoices, setAiChoices] = useState([]);

  const startSimulation = () => {
    const c = generateCompany();
    const cr = generateCrisis();
    let m = initialMetrics();
    Object.keys(cr.impact).forEach((k) => { m[k] = clamp(m[k] + cr.impact[k] * cr.mult); });
    setCompany(c);
    setCrisis(cr);
    setMetrics(m);
    setScreen('company');
  };

  const resetGame = () => {
    setScreen('welcome');
    setCompany(null);
    setCrisis(null);
    setMetrics(initialMetrics());
    setWarRoomChoices([]);
    setNegotiation({ trust:50, price:0, leadTime:0, round:0, log:[] });
    setBoardroomIndex(0);
    setBoardroomScore(0);
    setAiChoices([]);
  };

  const stepIndex = STEPS.indexOf({
    welcome:'Welcome', company:'Company', crisis:'Crisis', warroom:'War Room',
    negotiation:'Negotiation', boardroom:'Boardroom', aistrategy:'AI Strategy', dashboard:'Dashboard'
  }[screen]);

  return (
    <div className="app-shell">
      <TopBar />
      {screen !== 'welcome' && <Stepper current={stepIndex} />}

      {screen === 'welcome' && <Welcome onStart={startSimulation} />}

      {screen === 'company' && company && (
        <CompanyReveal company={company} onNext={() => setScreen('crisis')} />
      )}

      {screen === 'crisis' && crisis && (
        <CrisisReveal crisis={crisis} company={company} onNext={() => setScreen('warroom')} />
      )}

      {screen === 'warroom' && (
        <WarRoom
          crisis={crisis}
          metrics={metrics}
          setMetrics={setMetrics}
          warRoomChoices={warRoomChoices}
          setWarRoomChoices={setWarRoomChoices}
          onNext={() => setScreen('negotiation')}
        />
      )}

      {screen === 'negotiation' && (
        <Negotiation
          negotiation={negotiation}
          setNegotiation={setNegotiation}
          onNext={() => setScreen('boardroom')}
        />
      )}

      {screen === 'boardroom' && (
        <Boardroom
          boardroomIndex={boardroomIndex}
          setBoardroomIndex={setBoardroomIndex}
          boardroomScore={boardroomScore}
          setBoardroomScore={setBoardroomScore}
          onNext={() => setScreen('aistrategy')}
        />
      )}

      {screen === 'aistrategy' && (
        <AIStrategy
          aiChoices={aiChoices}
          setAiChoices={setAiChoices}
          onNext={() => setScreen('dashboard')}
        />
      )}

      {screen === 'dashboard' && (
        <FinalDashboard
          company={company}
          crisis={crisis}
          metrics={metrics}
          warRoomChoices={warRoomChoices}
          negotiation={negotiation}
          boardroomScore={boardroomScore}
          aiChoices={aiChoices}
          onReplay={resetGame}
        />
      )}
    </div>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
</script>
</body>
</html>

SCREENSHOTS:<img width="1853" height="1001" alt="Screenshot 2026-07-27 111246" src="https://github.com/user-attachments/assets/2ca4b4a2-79dc-4582-a14d-2101e71997c1" />
<img width="1777" height="951" alt="Screenshot 2026-07-27 111304" src="https://github.com/user-attachments/assets/c50e2cbf-d29a-4e66-85b4-8e2071ac3187" />

