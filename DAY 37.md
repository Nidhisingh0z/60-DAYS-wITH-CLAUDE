Day 37
Build Task Compass
Learn How Work Flows Through Real Organizations

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Task Compass</title>
<style>
  :root{
    --bg:#0b0e14;
    --bg2:#0d1119;
    --panel: rgba(255,255,255,0.045);
    --panel-strong: rgba(255,255,255,0.075);
    --border: rgba(255,255,255,0.09);
    --text:#e9ecf4;
    --dim:#8b93a9;
    --dimmer:#5b6478;
    --accent:#2dd4bf;
    --accent2:#f59e0b;
    --good:#34d399;
    --fe:#6366f1; --be:#2dd4bf; --qa:#f59e0b; --pm:#ec4899;
    --ux:#a78bfa; --cs:#38bdf8; --em:#f87171; --ops:#34d399;
    --radius:18px;
    --font-d:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,sans-serif;
    --font-m:ui-monospace,"SF Mono",Menlo,Consolas,monospace;
  }
  *{box-sizing:border-box;}
  html,body{margin:0;padding:0;}
  body{
    min-height:100vh;
    background:
      radial-gradient(circle at 15% 8%, rgba(45,212,191,0.10), transparent 42%),
      radial-gradient(circle at 88% 78%, rgba(236,72,153,0.10), transparent 45%),
      linear-gradient(180deg, var(--bg) 0%, var(--bg2) 100%);
    color:var(--text);
    font-family:var(--font-d);
    -webkit-font-smoothing:antialiased;
    padding:28px 18px 60px;
  }
  .wrap{max-width:920px;margin:0 auto;}
  @media (prefers-reduced-motion: reduce){
    *{animation-duration:0.001ms !important; transition-duration:0.001ms !important;}
  }

  /* ---------- HEADER / COMPASS ---------- */
  header.top{display:flex;align-items:center;gap:18px;margin-bottom:26px;}
  .needle-wrap{
    width:64px;height:64px;flex:0 0 auto;position:relative;
    border-radius:50%;
    background:radial-gradient(circle at 35% 30%, rgba(255,255,255,0.08), rgba(255,255,255,0.01) 60%);
    border:1px solid var(--border);
  }
  .needle-wrap svg{position:absolute;inset:0;transition:transform 1.1s cubic-bezier(.34,1.4,.4,1);}
  .brand h1{
    margin:0; font-size:26px; font-weight:800; letter-spacing:-0.03em;
    background:linear-gradient(95deg,#fff, #9fd8d0 55%, var(--accent));
    -webkit-background-clip:text; background-clip:text; color:transparent;
  }
  .brand p{margin:2px 0 0; font-size:13px; color:var(--dim); letter-spacing:0.01em;}

  /* progress route */
  .route{display:flex;align-items:center;gap:0;margin-bottom:30px;}
  .route .stop{
    flex:1; text-align:center; position:relative; padding-bottom:14px;
  }
  .route .stop .label{font-size:11px; font-weight:700; letter-spacing:0.09em; text-transform:uppercase; color:var(--dimmer);}
  .route .stop.active .label{color:var(--accent);}
  .route .stop.done .label{color:var(--good);}
  .route .stop .dot{
    width:11px;height:11px;border-radius:50%;margin:6px auto 0;
    background:var(--dimmer); border:2px solid transparent;
  }
  .route .stop.active .dot{background:var(--accent); box-shadow:0 0 0 5px rgba(45,212,191,0.18);}
  .route .stop.done .dot{background:var(--good);}
  .route .stop:not(:last-child)::after{
    content:''; position:absolute; top:calc(50% + 3px); right:-50%; width:100%; height:2px;
    background:var(--dimmer); z-index:0; opacity:0.5;
  }
  .route .stop.done:not(:last-child)::after{background:var(--good); opacity:0.7;}

  .task-counter{font-family:var(--font-m); font-size:12px; color:var(--dim); text-align:right; margin-bottom:10px;}

  /* ---------- CARD PANELS ---------- */
  .panel{
    background:var(--panel);
    border:1px solid var(--border);
    border-radius:var(--radius);
    backdrop-filter:blur(14px);
    padding:26px;
    margin-bottom:20px;
    animation:rise .5s cubic-bezier(.2,.8,.3,1);
  }
  @keyframes rise{from{opacity:0; transform:translateY(14px);} to{opacity:1; transform:translateY(0);}}

  /* intro screen */
  .intro-grid{display:grid; grid-template-columns:repeat(auto-fill,minmax(230px,1fr)); gap:12px; margin-top:18px;}
  .wtype{
    padding:16px; border-radius:14px; border:1px solid var(--border); background:var(--panel-strong);
    cursor:pointer; font-size:14px; text-align:left; color:var(--text); transition:transform .18s ease, border-color .18s ease;
  }
  .wtype:hover{transform:translateY(-3px); border-color:var(--accent);}
  button.cta{
    background:linear-gradient(95deg, var(--accent), #22b8a2);
    color:#03211d; border:none; font-weight:800; letter-spacing:0.01em;
    padding:13px 22px; border-radius:12px; cursor:pointer; font-size:14.5px;
    transition:transform .15s ease, box-shadow .15s ease;
    box-shadow:0 8px 22px -8px rgba(45,212,191,0.6);
  }
  button.cta:hover{transform:translateY(-2px);}
  button.cta:disabled{opacity:0.35; cursor:not-allowed; transform:none; box-shadow:none;}
  button.ghost{
    background:transparent; border:1px solid var(--border); color:var(--dim);
    padding:10px 16px; border-radius:10px; cursor:pointer; font-size:13.5px;
  }
  button.ghost:hover{border-color:var(--accent); color:var(--text);}

  /* ---------- TICKET ---------- */
  .ticket{
    position:relative;
    background:linear-gradient(180deg, rgba(255,255,255,0.055), rgba(255,255,255,0.02));
    border:1px dashed rgba(255,255,255,0.22);
    border-radius:14px; padding:20px 24px; margin-bottom:22px;
  }
  .ticket::before, .ticket::after{
    content:''; position:absolute; width:20px; height:20px; border-radius:50%;
    background:var(--bg); top:50%; transform:translateY(-50%);
    box-shadow:0 0 0 1px rgba(255,255,255,0.08) inset;
  }
  .ticket::before{left:-10px;} .ticket::after{right:-10px;}
  .ticket .tid{font-family:var(--font-m); font-size:11.5px; color:var(--accent2); letter-spacing:0.05em;}
  .ticket .ttext{font-size:18px; font-weight:600; margin-top:8px; line-height:1.45;}
  .ticket .ttag{display:inline-block; font-size:10.5px; font-family:var(--font-m); color:var(--dim); border:1px solid var(--border); padding:2px 8px; border-radius:20px; margin-top:10px;}

  h2.stagehead{font-size:15px; text-transform:uppercase; letter-spacing:0.1em; color:var(--dim); margin:0 0 4px;}
  h3.stagesub{font-size:20px; margin:0 0 18px; font-weight:750; letter-spacing:-0.01em;}

  /* ---------- ROLE CARDS ---------- */
  .role-pool{display:flex; flex-wrap:wrap; gap:10px; margin:14px 0 20px;}
  .role-card{
    --c: var(--accent);
    display:flex; align-items:center; gap:9px;
    padding:11px 15px; border-radius:12px; cursor:grab;
    background:linear-gradient(145deg, color-mix(in srgb, var(--c) 20%, transparent), rgba(255,255,255,0.02));
    border:1px solid color-mix(in srgb, var(--c) 45%, var(--border));
    font-size:13.5px; font-weight:600; user-select:none;
    transition:transform .16s ease, box-shadow .16s ease, opacity .16s ease;
  }
  .role-card:hover{transform:translateY(-3px) scale(1.02); box-shadow:0 10px 20px -10px color-mix(in srgb, var(--c) 60%, transparent);}
  .role-card.selected{outline:2px solid var(--c); background:color-mix(in srgb, var(--c) 28%, transparent);}
  .role-card.placed{opacity:0.28; cursor:not-allowed; transform:none;}
  .role-card .ic{font-size:16px;}
  .role-card .swatch{width:8px;height:8px;border-radius:50%; background:var(--c);}

  /* stage1 drop slot */
  .slot{
    margin-top:6px; min-height:64px; border-radius:14px;
    border:2px dashed var(--border); display:flex; align-items:center; justify-content:center;
    color:var(--dimmer); font-size:13px; transition:border-color .18s ease, background .18s ease;
    gap:10px; padding:8px;
  }
  .slot.over{border-color:var(--accent); background:rgba(45,212,191,0.08);}
  .slot.filled{border-style:solid; border-color:var(--panel-border);}
  .slot .slot-label{position:absolute; font-size:10.5px;}

  /* stage2 route slots */
  .route2{display:flex; align-items:stretch; gap:8px; margin:16px 0 22px; flex-wrap:wrap;}
  .route2 .rs{
    flex:1; min-width:120px; min-height:70px; border-radius:12px; border:2px dashed var(--border);
    display:flex; flex-direction:column; align-items:center; justify-content:center; gap:4px;
    position:relative; transition:border-color .18s ease, background .18s ease; padding:8px;
  }
  .route2 .rs .n{position:absolute; top:5px; left:8px; font-family:var(--font-m); font-size:10px; color:var(--dimmer);}
  .route2 .rs.over{border-color:var(--accent); background:rgba(45,212,191,0.08);}
  .route2 .rs.filled{border-style:solid;}
  .route2 .arrow{align-self:center; color:var(--dimmer); font-size:16px;}

  /* stage3 selection */
  .role-card.multi.selected{transform:translateY(-2px);}
  .sel-counter{font-family:var(--font-m); font-size:12px; color:var(--dim); margin:4px 0 2px;}

  /* feedback panel */
  .feedback{border-left:3px solid var(--accent); padding-left:16px; margin-top:6px;}
  .feedback .row{margin-bottom:10px; font-size:14.5px; line-height:1.55;}
  .feedback .row b{color:var(--text);}
  .feedback .tag-row{display:flex; flex-wrap:wrap; gap:6px; margin:6px 0 10px;}
  .mini-chip{font-size:11.5px; font-weight:700; padding:3px 10px; border-radius:20px; display:inline-flex; align-items:center; gap:5px;}

  .actions{display:flex; justify-content:flex-end; gap:10px; margin-top:18px;}

  /* animated flow (stage2 reveal) */
  .flow-anim{display:flex; align-items:center; gap:6px; margin:18px 0; overflow-x:auto; padding-bottom:6px;}
  .flow-anim .fchip{
    font-size:12.5px; font-weight:700; padding:8px 13px; border-radius:20px; white-space:nowrap;
    opacity:0; transform:translateX(-14px); animation:flowin .5s ease forwards;
  }
  @keyframes flowin{to{opacity:1; transform:translateX(0);}}
  .flow-anim .farrow{color:var(--dimmer); opacity:0; animation:flowin .5s ease forwards;}

  /* radar chart + final */
  .final-grid{display:grid; grid-template-columns:1fr 1fr; gap:22px;}
  @media (max-width:680px){.final-grid{grid-template-columns:1fr;}}
  .score-list .srow{margin-bottom:14px;}
  .score-list .slabel{display:flex; justify-content:space-between; font-size:13px; margin-bottom:5px;}
  .score-list .sbar{height:8px; border-radius:6px; background:rgba(255,255,255,0.06); overflow:hidden;}
  .score-list .sbar i{display:block; height:100%; border-radius:6px; transition:width 1s cubic-bezier(.2,.8,.3,1);}

  .reflect-block{margin-bottom:14px;}
  .reflect-block .rl{font-size:11px; text-transform:uppercase; letter-spacing:0.09em; color:var(--dimmer); margin-bottom:4px;}
  .reflect-block .rt{font-size:14.5px; line-height:1.55;}

  .confetti-layer{position:fixed; inset:0; pointer-events:none; overflow:hidden; z-index:50;}
  .confetti-piece{position:absolute; top:-20px; width:8px; height:14px; opacity:0.9; border-radius:2px; animation:fall linear forwards;}
  @keyframes fall{to{transform:translateY(110vh) rotate(540deg); opacity:0.2;}}

  a.dl{color:var(--accent); font-size:12.5px; text-decoration:none; border-bottom:1px dashed var(--accent);}
  .sr-only{position:absolute; width:1px; height:1px; overflow:hidden; clip:rect(0 0 0 0);}
  :focus-visible{outline:2px solid var(--accent); outline-offset:2px;}
</style>
</head>
<body>
<div class="wrap" id="app"></div>
<div class="confetti-layer" id="confetti"></div>

<script>
(function(){

/* ================= DATA ================= */

const ROLES = [
  {id:'fe',  name:'Frontend Developer',  color:'var(--fe)',  icon:'💻'},
  {id:'be',  name:'Backend Developer',   color:'var(--be)',  icon:'🗄️'},
  {id:'qa',  name:'QA Engineer',         color:'var(--qa)',  icon:'🔍'},
  {id:'pm',  name:'Product Manager',     color:'var(--pm)',  icon:'🧭'},
  {id:'ux',  name:'UX Designer',         color:'var(--ux)',  icon:'🎨'},
  {id:'cs',  name:'Customer Support',    color:'var(--cs)',  icon:'💬'},
  {id:'em',  name:'Engineering Manager', color:'var(--em)',  icon:'🛠️'},
  {id:'ops', name:'DevOps / SRE',        color:'var(--ops)', icon:'⚙️'}
];
const R = Object.fromEntries(ROLES.map(r=>[r.id,r]));

const STAGE1 = [
  {tid:'TCK-1042', text:'A customer reports that payments fail only on iPhones.',
    owner:'fe', why:'The checkout UI is rendered and validated on the client, and iOS-only bugs are usually caused by how that interface behaves in Safari or an in-app WebView — so the person who owns that code path investigates first.',
    assist:[{id:'qa', why:'reproduces the bug on a real iPhone to confirm it and rule out a one-off device issue'},{id:'be', why:'checks whether the server is actually receiving and accepting the request correctly'},{id:'cs', why:'gathers device, OS version, and app version details from the customer'}]},
  {tid:'TCK-1088', text:'The database is returning stale data after every deploy.',
    owner:'be', why:'Backend Developer owns the data layer and the deploy scripts that touch it, so a stale-data pattern tied to deploys starts in their code and configuration.',
    assist:[{id:'ops', why:'checks whether a cache or CDN layer needs invalidating on deploy'},{id:'qa', why:'confirms exact reproduction steps and timing'},{id:'em', why:'unblocks the fix if it turns out to be a process gap, like a missing deploy step'}]},
  {tid:'TCK-1103', text:'Users say the signup form is confusing and drop off halfway through.',
    owner:'ux', why:'UX Designer owns how the flow is structured and how each step communicates what to do next, which is exactly what is breaking down here.',
    assist:[{id:'pm', why:'decides how urgently this should be prioritized against other work'},{id:'fe', why:'implements the redesigned flow once it is ready'},{id:'cs', why:'shares patterns of confusion seen directly in support tickets'}]},
  {tid:'TCK-1150', text:'A critical security vulnerability was found in a third-party library.',
    owner:'be', why:'The library is used inside the application code, so Backend Developer owns testing and shipping the patched version safely.',
    assist:[{id:'ops', why:'coordinates the emergency deployment once the fix is ready'},{id:'qa', why:'runs regression tests so the patch does not break anything else'},{id:'em', why:'prioritizes the fix and communicates urgency across the team'}]},
  {tid:'TCK-1167', text:'The support team is getting the same complaint fifty times a day this week.',
    owner:'pm', why:'Product Manager owns deciding whether a recurring complaint becomes a roadmap priority, since it is a pattern, not a one-off bug.',
    assist:[{id:'cs', why:'has already surfaced the pattern and keeps tracking how often it happens'},{id:'em', why:'staffs engineers on the fix once it is prioritized'},{id:'fe', why:'implements the change if the root cause lives in the interface'}]},
  {tid:'TCK-1179', text:'A new feature works, but no one on the team can agree on how it should look.',
    owner:'ux', why:'UX Designer owns visual and interaction decisions, and is the natural tie-breaker when opinions differ on how something should look and feel.',
    assist:[{id:'pm', why:'weighs in on priority and scope tradeoffs'},{id:'fe', why:'flags what is and is not technically feasible to build'},{id:'em', why:'helps resolve the disagreement if the team stays stuck'}]},
  {tid:'TCK-1201', text:'QA keeps finding the same category of bug before every release.',
    owner:'em', why:'A recurring pattern across releases is usually a team-practice problem — like thin code review or missing tests — which is Engineering Manager\u2019s territory to fix.',
    assist:[{id:'qa', why:'identifies exactly where the pattern keeps showing up'},{id:'be', why:'owns the area of code where the bugs usually originate'},{id:'pm', why:'adjusts the release timeline if extra hardening time is needed'}]},
  {tid:'TCK-1222', text:'A new hire does not know who to ask when they get blocked.',
    owner:'em', why:'Engineering Manager owns onboarding and making sure the team\u2019s structure and points of contact are clear to everyone, including someone brand new.',
    assist:[{id:'pm', why:'clarifies who owns which project so the new hire has an anchor'},{id:'be', why:'often acts as a technical mentor during onboarding'},{id:'fe', why:'can serve the same mentoring role depending on the new hire\u2019s team'}]},
  {tid:'TCK-1240', text:'The checkout page crashes only during flash sales with heavy traffic.',
    owner:'ops', why:'DevOps / SRE owns infrastructure capacity and resilience under load, and a crash that only appears under heavy traffic points to scaling, not a logic bug.',
    assist:[{id:'be', why:'optimizes the backend queries that are likely struggling under load'},{id:'fe', why:'adds graceful fallback behavior when the backend is under pressure'},{id:'qa', why:'runs load tests to confirm the fix holds before the next sale'}]}
];

const STAGE2 = [
  {tid:'RTE-2011', text:'A customer reports a bug through live chat.',
    order:['cs','qa','be','pm','cs'],
    why:'Support captures what the customer actually experienced, QA reproduces it to confirm it is real and not a one-off, Backend fixes the root cause, Product Manager decides how and when to communicate the fix, and Support closes the loop directly with the customer.'},
  {tid:'RTE-2033', text:'A new feature idea comes out of a customer survey.',
    order:['pm','ux','be','fe','qa'],
    why:'Product Manager validates that the idea is worth building, UX designs the experience around it, Backend builds the data and API it needs, Frontend builds the interface on top of that, and QA verifies everything works before it ships.'},
  {tid:'RTE-2050', text:'Production goes down at 2am.',
    order:['ops','be','qa','em','cs'],
    why:'DevOps / SRE gets paged and triages the outage first, Backend Developer diagnoses and fixes the root cause, QA confirms the fix actually holds, Engineering Manager runs communication and the post-incident review, and Support updates any affected customers.'},
  {tid:'RTE-2067', text:'Marketing wants a landing page ready for a launch next week.',
    order:['pm','ux','fe','qa'],
    why:'Product Manager scopes the page and locks the deadline, UX designs the layout and messaging flow, Frontend builds it, and QA checks it before it goes live under time pressure.'},
  {tid:'RTE-2081', text:'A customer requests a refund due to a billing error.',
    order:['cs','be','cs'],
    why:'Support receives and logs the request, Backend verifies the billing error and processes the correction, and Support confirms the resolution back to the customer.'},
  {tid:'RTE-2099', text:'An engineer proposes migrating to a new database technology.',
    order:['be','em','ops','qa'],
    why:'Backend proposes and prototypes the migration, Engineering Manager weighs the cost and risk before approving it, DevOps / SRE plans the infrastructure side of the move, and QA validates that no data integrity was lost.'},
  {tid:'RTE-2115', text:'A researcher discovers users do not understand a core feature.',
    order:['ux','pm','fe','qa'],
    why:'UX surfaces exactly where users get confused, Product Manager prioritizes a fix against everything else in flight, Frontend implements the clarified version, and QA verifies the usability fix did not break anything else.'}
];

const STAGE3 = [
  {tid:'SIT-3001', text:'Customer satisfaction suddenly drops across the board.',
    primary:'pm', support:['cs','ux','em'],
    why:{pm:'Product Manager owns tracking and prioritizing what is actually causing the drop across the whole product.', cs:'is the first to see the raw complaints coming in and can spot the pattern fastest.', ux:'investigates whether a recent change created friction in the experience.', em:'mobilizes engineers once the cause is identified.'},
    flow:'Support logs and aggregates the complaints \u2192 Product Manager analyzes the pattern and sets priorities \u2192 UX investigates specific points of friction \u2192 Engineering Manager allocates engineers to fix it, looping back to the Product Manager on progress.'},
  {tid:'SIT-3018', text:'Sales increase dramatically overnight.',
    primary:'ops', support:['be','em','pm'],
    why:{ops:'a sudden spike in demand threatens infrastructure capacity first, before anything else.', be:'scales and optimizes the services under the new load.', em:'reallocates the team to focus on stability during the surge.', pm:'decides whether this changes what gets built next.'},
    flow:'DevOps / SRE monitors capacity and raises the alarm \u2192 Backend scales and optimizes the services \u2192 Engineering Manager reallocates the team\u2019s focus \u2192 Product Manager communicates any customer-facing impact or new opportunity.'},
  {tid:'SIT-3034', text:'Negative reviews appear online about a recent update.',
    primary:'pm', support:['cs','ux','em'],
    why:{pm:'triages how serious the issue is and decides the response.', cs:'responds to reviews directly and gathers detail on what is going wrong.', ux:'assesses whether the update itself hurt usability.', em:'assigns engineers to resolve the root cause.'},
    flow:'Support surfaces themes across the reviews \u2192 Product Manager triages severity and decides a response \u2192 UX evaluates the root usability cause \u2192 Engineering Manager assigns engineers to fix it, and the Product Manager communicates back publicly.'},
  {tid:'SIT-3047', text:'A major feature is delayed.',
    primary:'em', support:['pm','be','cs'],
    why:{em:'owns assessing team capacity and deciding the realistic path forward.', pm:'renegotiates scope or timeline once the real picture is clear.', be:'reports exactly what is blocking progress.', cs:'prepares messaging for customers who are expecting the feature.'},
    flow:'Backend flags the blocker \u2192 Engineering Manager assesses capacity and options \u2192 Product Manager adjusts scope or timeline \u2192 Support is briefed on how to message the delay.'},
  {tid:'SIT-3055', text:'A key engineer unexpectedly quits mid-project.',
    primary:'em', support:['pm','be','qa'],
    why:{em:'owns reassigning responsibilities and stabilizing the team.', pm:'adjusts timeline expectations once the impact is clear.', be:'absorbs context and continues the technical work.', qa:'increases test coverage during the handoff to catch anything missed.'},
    flow:'Engineering Manager reassigns responsibilities \u2192 Product Manager adjusts timeline expectations \u2192 remaining engineers absorb the missing context \u2192 QA increases coverage during the transition.'},
  {tid:'SIT-3062', text:'A competitor launches a similar product at a much lower price.',
    primary:'pm', support:['ux','em','cs'],
    why:{pm:'owns analyzing the competitive gap and deciding how to respond.', ux:'explores where the experience can differentiate beyond price.', em:'evaluates what is actually feasible to build in response.', cs:'monitors customer sentiment and retention signals.'},
    flow:'Product Manager analyzes the competitive gap \u2192 UX explores differentiation opportunities \u2192 Engineering Manager evaluates what is feasible to build \u2192 Support monitors customer reactions and retention.'}
];

/* ================= STATE ================= */

let state = {
  screen:'intro',
  workplace:null,
  stage:1,
  idx:0,
  tasks:{s1:[],s2:[],s3:[]},
  current:{
    s1owner:null,
    s2order:[],
    s2pool:[],
    s3selected:[]
  },
  revealed:false,
  scores:{
    ownershipHits:0,
    workflowFracs:[],
    delegationHits:0,
    collabFracs:[],
    s3SelSizes:[],
    s3CorrectSizes:[]
  }
};

function shuffle(arr){
  const a = arr.slice();
  for(let i=a.length-1;i>0;i--){
    const j = Math.floor(Math.random()*(i+1));
    [a[i],a[j]]=[a[j],a[i]];
  }
  return a;
}
function pick3(arr){ return shuffle(arr).slice(0,3); }

const app = document.getElementById('app');

/* ================= RENDER ROUTER ================= */

function render(){
  if(state.screen==='intro') return renderIntro();
  if(state.screen==='play') return renderPlay();
  if(state.screen==='final') return renderFinal();
}

/* ---------------- INTRO ---------------- */

function renderIntro(){
  app.innerHTML = `
    <header class="top">
      <div class="needle-wrap">${compassSVG(0)}</div>
      <div class="brand">
        <h1>Task Compass</h1>
        <p>Learn how work flows through real organizations.</p>
      </div>
    </header>
    <div class="panel">
      <h2 class="stagehead">Setting</h2>
      <h3 class="stagesub">Exploring: Tech Company</h3>
      <p style="color:var(--dim); font-size:14.5px; line-height:1.6; margin-top:-8px;">
        You'll work through three stages: figuring out who owns a task, routing work through the
        right sequence of people, and coordinating a real cross-team response. There are no
        wrong-only or right-only answers &mdash; every choice comes with reasoning.
      </p>
      <div style="margin-top:20px; display:flex; justify-content:flex-end;">
        <button class="cta" id="startBtn">Start &rarr;</button>
      </div>
    </div>
  `;
  document.getElementById('startBtn').onclick = ()=>{
    state.workplace='Tech Company';
    state.tasks.s1 = pick3(STAGE1);
    state.tasks.s2 = pick3(STAGE2);
    state.tasks.s3 = pick3(STAGE3);
    state.screen='play'; state.stage=1; state.idx=0;
    resetCurrent();
    render();
  };
}

function resetCurrent(){
  state.current.s1owner=null;
  const t = state.tasks.s2[state.idx];
  state.current.s2order = t ? new Array(t.order.length).fill(null) : [];
  state.current.s2pool = t ? shuffle(t.order) : [];
  state.current.s3selected = [];
  state.revealed=false;
}

/* ---------------- ROUTE / PROGRESS ---------------- */

function routeHTML(){
  const stops = [
    {n:1,label:'Ownership'},
    {n:2,label:'Routing'},
    {n:3,label:'Collaboration'}
  ];
  return `<div class="route">${stops.map(s=>{
    let cls='';
    if(s.n<state.stage) cls='done';
    else if(s.n===state.stage) cls='active';
    return `<div class="stop ${cls}"><div class="label">${s.label}</div><div class="dot"></div></div>`;
  }).join('')}</div>`;
}

function compassSVG(angle){
  return `<svg viewBox="0 0 64 64" width="64" height="64">
    <circle cx="32" cy="32" r="26" fill="none" stroke="rgba(255,255,255,0.12)" stroke-width="1.5"/>
    <g style="transform:rotate(${angle}deg); transform-origin:32px 32px; transition:transform 1s ease;">
      <polygon points="32,10 37,32 32,30 27,32" fill="var(--accent)"/>
      <polygon points="32,54 37,32 32,34 27,32" fill="var(--dimmer)"/>
    </g>
    <circle cx="32" cy="32" r="3" fill="#fff"/>
  </svg>`;
}

/* ---------------- PLAY ROUTER ---------------- */

function renderPlay(){
  const angle = state.stage===1?0: state.stage===2?120:240;
  let body='';
  if(state.stage===1) body = renderStage1();
  else if(state.stage===2) body = renderStage2();
  else body = renderStage3();

  app.innerHTML = `
    <header class="top">
      <div class="needle-wrap">${compassSVG(angle)}</div>
      <div class="brand">
        <h1>Task Compass</h1>
        <p>Learn how work flows through real organizations.</p>
      </div>
    </header>
    ${routeHTML()}
    <div class="task-counter">TASK ${state.idx+1} OF 3 &mdash; STAGE ${state.stage}</div>
    ${body}
  `;
  wireStageEvents();
}

/* ---------------- STAGE 1 ---------------- */

function renderStage1(){
  const t = state.tasks.s1[state.idx];
  const placedId = state.current.s1owner;
  const poolHTML = ROLES.map(r=>{
    const isPlaced = placedId===r.id;
    return roleCardHTML(r, {draggable:!state.revealed && !isPlaced, extraClass:isPlaced?'placed':'', clickable:!state.revealed && !isPlaced});
  }).join('');

  let slotInner = placedId
    ? roleCardHTML(R[placedId], {draggable:false})
    : 'Drag or tap a role here &mdash; who owns this?';

  let feedback = '';
  if(state.revealed){
    const correct = placedId===t.owner;
    feedback = `
      <div class="feedback">
        <div class="row">${correct? '✓' : '↳'} <b>Primary Owner: ${R[t.owner].icon} ${R[t.owner].name}</b></div>
        <div class="row">${escapeHtml(t.why)}</div>
        <div class="row"><b>May also assist:</b></div>
        <div class="tag-row">
          ${t.assist.map(a=>chip(R[a.id])).join('')}
        </div>
        ${t.assist.map(a=>`<div class="row" style="font-size:13.5px; color:var(--dim);">${R[a.id].name} ${escapeHtml(a.why)}</div>`).join('')}
        ${!correct? `<div class="row" style="margin-top:10px;">You placed <b>${R[placedId] ? R[placedId].name : 'nothing'}</b>. That role might reasonably help, but the primary owner above is the one accountable for driving this to resolution.</div>`:''}
      </div>
    `;
  }

  return `
    <div class="panel">
      <h2 class="stagehead">Stage 1 &middot; Who Owns This?</h2>
      <div class="ticket">
        <div class="tid">${t.tid}</div>
        <div class="ttext">${escapeHtml(t.text)}</div>
        <span class="ttag">needs an owner</span>
      </div>
      <div style="font-size:13px; color:var(--dim); margin-bottom:6px;">Drag one role into the ownership slot:</div>
      <div class="role-pool" id="s1pool">${poolHTML}</div>
      <div class="slot ${placedId?'filled':''}" id="s1slot" data-role="ownership">${slotInner}</div>
      ${feedback}
      <div class="actions">
        ${!state.revealed
          ? `<button class="cta" id="submitBtn" ${!placedId?'disabled':''}>Reveal Ownership</button>`
          : `<button class="cta" id="nextBtn">Continue &rarr;</button>`}
      </div>
    </div>
  `;
}

/* ---------------- STAGE 2 ---------------- */

function renderStage2(){
  const t = state.tasks.s2[state.idx];
  const slots = state.current.s2order;
  const poolIds = state.current.s2pool.filter(id=>!slots.includes(id));

  const slotsHTML = slots.map((rid,i)=>{
    const filled = !!rid;
    return `<div class="rs ${filled?'filled':''}" data-slotidx="${i}">
      <span class="n">${i+1}</span>
      ${filled ? roleCardHTML(R[rid],{draggable:!state.revealed, extraClass:'placed-in-slot'}) : '<span style="color:var(--dimmer); font-size:12px;">drop here</span>'}
    </div>`;
  }).join(`<div class="arrow">&rarr;</div>`);

  const poolHTML = poolIds.map(rid=>roleCardHTML(R[rid],{draggable:!state.revealed, clickable:!state.revealed})).join('');

  const allFilled = slots.every(x=>x!==null);

  let feedback = '';
  if(state.revealed){
    feedback = `
      <div class="feedback">
        <div class="row"><b>Common routing:</b></div>
        <div class="flow-anim">${t.order.map((rid,i)=>`
          ${i>0?`<span class="farrow" style="animation-delay:${i*0.35+0.1}s">&rarr;</span>`:''}
          <span class="fchip" style="background:color-mix(in srgb, ${R[rid].color} 30%, transparent); color:#fff; animation-delay:${i*0.35}s;">${R[rid].icon} ${R[rid].name}</span>
        `).join('')}</div>
        <div class="row">${escapeHtml(t.why)}</div>
      </div>
    `;
  }

  return `
    <div class="panel">
      <h2 class="stagehead">Stage 2 &middot; Task Routing</h2>
      <div class="ticket">
        <div class="tid">${t.tid}</div>
        <div class="ttext">${escapeHtml(t.text)}</div>
        <span class="ttag">build the workflow</span>
      </div>
      <div style="font-size:13px; color:var(--dim); margin-bottom:6px;">Drag roles into order, step by step:</div>
      <div class="route2" id="s2slots">${slotsHTML}</div>
      <div class="role-pool" id="s2pool">${poolHTML}</div>
      ${feedback}
      <div class="actions">
        ${!state.revealed
          ? `<button class="cta" id="submitBtn" ${!allFilled?'disabled':''}>Reveal Routing</button>`
          : `<button class="cta" id="nextBtn">Continue &rarr;</button>`}
      </div>
    </div>
  `;
}

/* ---------------- STAGE 3 ---------------- */

function renderStage3(){
  const t = state.tasks.s3[state.idx];
  const sel = state.current.s3selected;
  const poolHTML = ROLES.map(r=>{
    const isSel = sel.includes(r.id);
    return roleCardHTML(r, {draggable:false, clickable:!state.revealed, extraClass:`multi ${isSel?'selected':''}`});
  }).join('');

  let feedback = '';
  if(state.revealed){
    const fullSet = [t.primary, ...t.support];
    feedback = `
      <div class="feedback">
        <div class="row"><b>Primary Owner:</b></div>
        <div class="tag-row">${chip(R[t.primary])}</div>
        <div class="row" style="font-size:13.5px; color:var(--dim);">${escapeHtml(t.why[t.primary])}</div>
        <div class="row" style="margin-top:8px;"><b>Supporting Teams:</b></div>
        <div class="tag-row">${t.support.map(id=>chip(R[id])).join('')}</div>
        ${t.support.map(id=>`<div class="row" style="font-size:13.5px; color:var(--dim);">${R[id].name} ${escapeHtml(t.why[id])}</div>`).join('')}
        <div class="row" style="margin-top:8px;"><b>Communication Flow:</b></div>
        <div class="row">${escapeHtml(t.flow)}</div>
      </div>
    `;
  }

  return `
    <div class="panel">
      <h2 class="stagehead">Stage 3 &middot; Collaboration Challenge</h2>
      <div class="ticket">
        <div class="tid">${t.tid}</div>
        <div class="ttext">${escapeHtml(t.text)}</div>
        <span class="ttag">complex &middot; needs a team</span>
      </div>
      <div style="font-size:13px; color:var(--dim); margin-bottom:6px;">Select up to four roles you'd bring in:</div>
      <div class="sel-counter">${sel.length} / 4 selected</div>
      <div class="role-pool" id="s3pool">${poolHTML}</div>
      ${feedback}
      <div class="actions">
        ${!state.revealed
          ? `<button class="cta" id="submitBtn" ${sel.length===0?'disabled':''}>Reveal Response</button>`
          : `<button class="cta" id="nextBtn">Continue &rarr;</button>`}
      </div>
    </div>
  `;
}

/* ---------------- SHARED ROLE CARD HTML ---------------- */

function roleCardHTML(role, opts){
  opts = opts||{};
  return `<div class="role-card ${opts.extraClass||''}" data-role="${role.id}"
      style="--c:${role.color};" ${opts.draggable?'draggable="true"':''}>
    <span class="ic">${role.icon}</span><span>${role.name}</span>
  </div>`;
}
function chip(role){
  return `<span class="mini-chip" style="background:color-mix(in srgb, ${role.color} 35%, transparent); color:#fff;">${role.icon} ${role.name}</span>`;
}
function escapeHtml(s){
  const d=document.createElement('div'); d.textContent=s; return d.innerHTML;
}

/* ---------------- EVENT WIRING ---------------- */

function wireStageEvents(){
  if(state.stage===1) wireStage1();
  if(state.stage===2) wireStage2();
  if(state.stage===3) wireStage3();

  const submitBtn = document.getElementById('submitBtn');
  if(submitBtn) submitBtn.onclick = handleSubmit;
  const nextBtn = document.getElementById('nextBtn');
  if(nextBtn) nextBtn.onclick = handleNext;
}

function handleSubmit(){
  if(state.stage===1){
    const t = state.tasks.s1[state.idx];
    if(state.current.s1owner===t.owner) state.scores.ownershipHits++;
  } else if(state.stage===2){
    const t = state.tasks.s2[state.idx];
    let correctCount=0;
    state.current.s2order.forEach((rid,i)=>{ if(rid===t.order[i]) correctCount++; });
    state.scores.workflowFracs.push(correctCount/t.order.length);
  } else if(state.stage===3){
    const t = state.tasks.s3[state.idx];
    const sel = state.current.s3selected;
    const fullSet = [t.primary, ...t.support];
    if(sel.includes(t.primary)) state.scores.delegationHits++;
    const overlap = sel.filter(id=>fullSet.includes(id)).length;
    state.scores.collabFracs.push(overlap/fullSet.length);
    state.scores.s3SelSizes.push(sel.length);
    state.scores.s3CorrectSizes.push(fullSet.length);
  }
  state.revealed=true;
  render();
}

function handleNext(){
  if(state.idx<2){
    state.idx++;
    resetCurrent();
    render();
  } else if(state.stage<3){
    state.stage++;
    state.idx=0;
    resetCurrent();
    render();
  } else {
    state.screen='final';
    render();
  }
}

/* --- stage 1 wiring: click-to-place + native drag --- */
function wireStage1(){
  const pool = document.getElementById('s1pool');
  const slot = document.getElementById('s1slot');
  if(!pool||!slot) return;

  pool.querySelectorAll('.role-card').forEach(card=>{
    card.addEventListener('dragstart', e=>{
      e.dataTransfer.setData('text/plain', card.dataset.role);
    });
    card.addEventListener('click', ()=>{
      if(state.revealed || card.classList.contains('placed')) return;
      state.current.s1owner = card.dataset.role;
      render();
    });
  });
  slot.addEventListener('dragover', e=>{ e.preventDefault(); slot.classList.add('over'); });
  slot.addEventListener('dragleave', ()=> slot.classList.remove('over'));
  slot.addEventListener('drop', e=>{
    e.preventDefault(); slot.classList.remove('over');
    const rid = e.dataTransfer.getData('text/plain');
    if(rid && !state.revealed){ state.current.s1owner = rid; render(); }
  });
  slot.addEventListener('click', ()=>{
    if(!state.revealed && state.current.s1owner){ state.current.s1owner=null; render(); }
  });
}

/* --- stage 2 wiring: click-to-append + native drag + click-to-remove --- */
function wireStage2(){
  const pool = document.getElementById('s2pool');
  const slotsWrap = document.getElementById('s2slots');
  if(!pool||!slotsWrap) return;

  function firstEmptyIdx(){ return state.current.s2order.findIndex(x=>x===null); }

  pool.querySelectorAll('.role-card').forEach(card=>{
    card.addEventListener('dragstart', e=>{
      e.dataTransfer.setData('text/plain', card.dataset.role);
    });
    card.addEventListener('click', ()=>{
      if(state.revealed) return;
      const i = firstEmptyIdx();
      if(i===-1) return;
      state.current.s2order[i] = card.dataset.role;
      render();
    });
  });

  slotsWrap.querySelectorAll('.rs').forEach(rs=>{
    const idx = parseInt(rs.dataset.slotidx,10);
    rs.addEventListener('dragover', e=>{ e.preventDefault(); rs.classList.add('over'); });
    rs.addEventListener('dragleave', ()=> rs.classList.remove('over'));
    rs.addEventListener('drop', e=>{
      e.preventDefault(); rs.classList.remove('over');
      const rid = e.dataTransfer.getData('text/plain');
      if(rid && !state.revealed){ state.current.s2order[idx]=rid; render(); }
    });
    rs.addEventListener('click', ()=>{
      if(!state.revealed && state.current.s2order[idx]){
        state.current.s2order[idx]=null; render();
      }
    });
  });
}

/* --- stage 3 wiring: click toggle up to 4 --- */
function wireStage3(){
  const pool = document.getElementById('s3pool');
  if(!pool) return;
  pool.querySelectorAll('.role-card').forEach(card=>{
    card.addEventListener('click', ()=>{
      if(state.revealed) return;
      const rid = card.dataset.role;
      const sel = state.current.s3selected;
      const i = sel.indexOf(rid);
      if(i>-1){ sel.splice(i,1); }
      else { if(sel.length>=4) return; sel.push(rid); }
      render();
    });
  });
}

/* ================= FINAL SCREEN ================= */

function computeScores(){
  const ownership = Math.round((state.scores.ownershipHits/3)*100);
  const workflow = Math.round(avg(state.scores.workflowFracs)*100);
  const delegation = Math.round((state.scores.delegationHits/3)*100);
  const collaboration = Math.round(avg(state.scores.collabFracs)*100);
  return {ownership, workflow, delegation, collaboration};
}
function avg(arr){ return arr.length? arr.reduce((a,b)=>a+b,0)/arr.length : 0; }

function renderFinal(){
  const s = computeScores();
  const cats = [
    {key:'ownership', label:'Ownership', color:'var(--fe)', val:s.ownership},
    {key:'delegation', label:'Delegation', color:'var(--pm)', val:s.delegation},
    {key:'collaboration', label:'Collaboration', color:'var(--cs)', val:s.collaboration},
    {key:'workflow', label:'Workflow Thinking', color:'var(--ops)', val:s.workflow}
  ];

  const avgSel = avg(state.scores.s3SelSizes);
  const avgCorrect = avg(state.scores.s3CorrectSizes);
  const overAssign = avgSel > avgCorrect + 0.5;
  const underCollab = avgSel < avgCorrect - 0.5;

  const best = cats.reduce((a,b)=> b.val>a.val? b:a, cats[0]);
  const understoodWell = {
    ownership: "You consistently identified who is actually accountable for a task, not just who could plausibly touch it &mdash; a strong instinct for clear ownership.",
    delegation: "When situations got messy, you reliably pointed to the right person to lead the response, even without a single obvious owner.",
    collaboration: "You picked up quickly on how many different people a real problem touches, and assembled sensible groups around it.",
    workflow: "You had a clear sense of the order work actually moves through a team, not just who is involved."
  }[best.key];

  const overText = overAssign
    ? "In the collaboration stage, you tended to pull in more people than a situation actually needed. Wide nets feel safe, but every extra person added is another handoff and another chance for something to get lost."
    : "You stayed fairly disciplined about who to bring in, rarely spreading responsibility across more people than a situation called for.";

  const underText = underCollab
    ? "You sometimes treated multi-team situations as if one person could fully own them. Complex problems &mdash; a sales spike, a wave of bad reviews &mdash; usually need more than one function moving at once."
    : "You recognized early that complex, cross-cutting problems usually pull in more than one team, rather than resting on a single owner.";

  const insights = [
    "Many real workplace problems are solved by teams rather than individuals.",
    "Clear ownership and heavy collaboration aren't opposites &mdash; the best-run teams have both.",
    "The order work moves through an organization often matters as much as who's involved in it.",
    "Escalation isn't a failure of ownership; it's often the fastest path back to clarity."
  ];
  const insight = insights[Math.floor(Math.random()*insights.length)];

  app.innerHTML = `
    <header class="top">
      <div class="needle-wrap">${compassSVG(240)}</div>
      <div class="brand">
        <h1>Task Compass</h1>
        <p>Learn how work flows through real organizations.</p>
      </div>
    </header>
    ${routeHTML()}
    <div class="panel">
      <h2 class="stagehead">Debrief</h2>
      <h3 class="stagesub">How you navigated the org chart</h3>
      <div class="final-grid">
        <div>
          ${radarSVG(cats)}
        </div>
        <div class="score-list">
          ${cats.map(c=>`
            <div class="srow">
              <div class="slabel"><span>${c.label}</span><span style="color:var(--dim);">${c.val}%</span></div>
              <div class="sbar"><i id="bar-${c.key}" style="width:0%; background:${c.color};"></i></div>
            </div>
          `).join('')}
        </div>
      </div>
    </div>
    <div class="panel">
      <h2 class="stagehead">Reflection</h2>
      <div class="reflect-block">
        <div class="rl">What you understood well</div>
        <div class="rt">${understoodWell}</div>
      </div>
      <div class="reflect-block">
        <div class="rl">Where you tended to over-assign responsibility</div>
        <div class="rt">${overText}</div>
      </div>
      <div class="reflect-block">
        <div class="rl">Where you underestimated collaboration</div>
        <div class="rt">${underText}</div>
      </div>
      <div class="reflect-block">
        <div class="rl">One insight</div>
        <div class="rt">"${insight}"</div>
      </div>
      <div class="actions">
        <button class="ghost" id="restartBtn">Play Again</button>
      </div>
    </div>
  `;

  requestAnimationFrame(()=>{
    cats.forEach(c=>{
      const el = document.getElementById('bar-'+c.key);
      if(el) el.style.width = c.val+'%';
    });
  });

  document.getElementById('restartBtn').onclick = ()=>{
    state = {
      screen:'intro', workplace:null, stage:1, idx:0,
      tasks:{s1:[],s2:[],s3:[]},
      current:{s1owner:null,s2order:[],s2pool:[],s3selected:[]},
      revealed:false,
      scores:{ownershipHits:0, workflowFracs:[], delegationHits:0, collabFracs:[], s3SelSizes:[], s3CorrectSizes:[]}
    };
    render();
  };

  launchConfetti();
}

function radarSVG(cats){
  const n = cats.length;
  const cx=110, cy=110, R=88;
  const angleFor = i => (Math.PI*2*i/n) - Math.PI/2;
  const pt = (i,val)=>{
    const r = R*(val/100);
    const a = angleFor(i);
    return [cx+r*Math.cos(a), cy+r*Math.sin(a)];
  };
  const ringPts = f => cats.map((c,i)=>{
    const a=angleFor(i); const r=R*f;
    return `${cx+r*Math.cos(a)},${cy+r*Math.sin(a)}`;
  }).join(' ');
  const dataPts = cats.map((c,i)=> pt(i,c.val).join(',')).join(' ');
  const labels = cats.map((c,i)=>{
    const a=angleFor(i);
    const lx = cx+(R+26)*Math.cos(a);
    const ly = cy+(R+26)*Math.sin(a);
    return `<text x="${lx}" y="${ly}" text-anchor="middle" font-size="10.5" fill="var(--dim)" font-family="var(--font-d)">${c.label}</text>`;
  }).join('');

  return `<svg viewBox="0 0 220 230" width="100%" height="auto" style="max-width:280px;">
    ${[0.25,0.5,0.75,1].map(f=>`<polygon points="${ringPts(f)}" fill="none" stroke="rgba(255,255,255,0.08)" stroke-width="1"/>`).join('')}
    ${cats.map((c,i)=>{ const [x,y]=pt(i,100); return `<line x1="${cx}" y1="${cy}" x2="${x}" y2="${y}" stroke="rgba(255,255,255,0.07)"/>`; }).join('')}
    <polygon points="${dataPts}" fill="rgba(45,212,191,0.22)" stroke="var(--accent)" stroke-width="2"/>
    ${cats.map((c,i)=>{ const [x,y]=pt(i,c.val); return `<circle cx="${x}" cy="${y}" r="3.5" fill="${c.color}"/>`; }).join('')}
    ${labels}
  </svg>`;
}

function launchConfetti(){
  const layer = document.getElementById('confetti');
  const colors = ['#6366f1','#2dd4bf','#f59e0b','#ec4899','#a78bfa','#38bdf8'];
  for(let i=0;i<60;i++){
    const p = document.createElement('div');
    p.className='confetti-piece';
    p.style.left = Math.random()*100+'vw';
    p.style.background = colors[Math.floor(Math.random()*colors.length)];
    p.style.animationDuration = (2.2+Math.random()*1.8)+'s';
    p.style.animationDelay = (Math.random()*0.6)+'s';
    layer.appendChild(p);
    setTimeout(()=>p.remove(), 5000);
  }
}

render();
})();
</script>
</body>
</html>
