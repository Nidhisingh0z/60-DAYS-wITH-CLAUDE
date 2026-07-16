<style>
  :root{
    --bg: #0d1220;
    --bg-2: #0a0e1a;
    --card: #141a2a;
    --card-2: #191f33;
    --line: rgba(255,255,255,0.08);
    --text: #e8ecf6;
    --text-dim: #8b93ab;
    --text-faint: #5c6480;
    --blue: #5b8cff;
    --blue-soft: rgba(91,140,255,0.14);
    --amber: #f2b134;
    --amber-soft: rgba(242,177,52,0.14);
    --red: #ef4444;
    --red-soft: rgba(239,68,68,0.14);
    --orange: #f5893a;
    --orange-soft: rgba(245,137,58,0.14);
    --green: #34d399;
    --green-soft: rgba(52,211,153,0.14);
    --purple: #a78bfa;
    --purple-soft: rgba(167,139,250,0.14);
    --font-ui: -apple-system, BlinkMacSystemFont, "Segoe UI", Inter, Roboto, Helvetica, Arial, sans-serif;
    --font-mono: ui-monospace, "SF Mono", "Cascadia Code", Menlo, Consolas, monospace;
  }

  *{ box-sizing:border-box; }

  html,body{
    margin:0; padding:0;
    background:
      radial-gradient(circle at 12% 0%, rgba(91,140,255,0.10), transparent 40%),
      radial-gradient(circle at 88% 8%, rgba(167,139,250,0.08), transparent 45%),
      var(--bg);
    color: var(--text);
    font-family: var(--font-ui);
    -webkit-font-smoothing: antialiased;
  }

  .wrap{ max-width: 1180px; margin: 0 auto; padding: 28px 20px 80px; }

  /* ---------- Header ---------- */
  .top-bar{
    display:flex; justify-content:space-between; align-items:flex-start;
    flex-wrap:wrap; gap:16px; margin-bottom: 26px;
  }
  .top-bar .eyebrow{
    font-family: var(--font-mono); font-size:11px; letter-spacing:0.2em;
    text-transform:uppercase; color: var(--blue); margin:0 0 6px;
  }
  .top-bar h1{ margin:0; font-size: 26px; font-weight:700; letter-spacing:-0.01em; }
  .top-bar p{ margin:6px 0 0; color:var(--text-dim); font-size:13.5px; max-width:560px; line-height:1.5; }

  .disclaimer-chip{
    font-family: var(--font-mono); font-size:11px; color: var(--text-dim);
    background: var(--card); border:1px solid var(--line); border-radius:10px;
    padding:10px 14px; max-width:280px; line-height:1.5;
  }
  .disclaimer-chip b{ color:var(--amber); }

  /* ---------- Tag chips ---------- */
  .tag{
    display:inline-flex; align-items:center; gap:5px;
    font-family: var(--font-mono); font-size:10px; letter-spacing:0.06em;
    text-transform:uppercase; padding:3px 8px; border-radius:6px; font-weight:600;
  }
  .tag-fact{ background: var(--blue-soft); color: var(--blue); }
  .tag-estimate{ background: var(--amber-soft); color: var(--amber); }

  /* ---------- Score row ---------- */
  .score-row{
    display:grid; grid-template-columns: repeat(4, 1fr); gap:14px; margin-bottom:18px;
  }
  @media (max-width: 900px){ .score-row{ grid-template-columns: repeat(2, 1fr); } }

  .score-card{
    background: var(--card); border:1px solid var(--line); border-radius:16px;
    padding:18px; position:relative; overflow:hidden;
  }
  .score-card .lbl{
    font-family: var(--font-mono); font-size:10.5px; letter-spacing:0.1em;
    text-transform:uppercase; color: var(--text-dim); margin:0 0 10px;
  }
  .score-card .big{
    font-size: 34px; font-weight:800; letter-spacing:-0.02em; line-height:1;
    display:flex; align-items:baseline; gap:6px;
  }
  .score-card .big small{ font-size:14px; color:var(--text-faint); font-weight:600; }
  .score-card .status{
    margin-top:8px; display:inline-flex; align-items:center; gap:6px;
    font-size:12px; font-weight:700; padding:4px 10px; border-radius:999px;
  }
  .status-minimal{ background: var(--green-soft); color: var(--green); }
  .status-moderate{ background: var(--amber-soft); color: var(--amber); }
  .status-significant{ background: var(--orange-soft); color: var(--orange); }
  .status-extensive{ background: var(--red-soft); color: var(--red); }
  .status-weak{ background: var(--red-soft); color: var(--red); }
  .status-fair{ background: var(--orange-soft); color: var(--orange); }
  .status-good{ background: var(--amber-soft); color: var(--amber); }
  .status-strong{ background: var(--green-soft); color: var(--green); }

  .bar-track{ height:6px; border-radius:4px; background: rgba(255,255,255,0.06); margin-top:12px; overflow:hidden; }
  .bar-fill{ height:100%; border-radius:4px; }

  .meta-row{
    display:grid; grid-template-columns: repeat(4,1fr); gap:14px; margin-bottom:32px;
  }
  @media (max-width: 900px){ .meta-row{ grid-template-columns: repeat(2,1fr); } }
  .meta-card{
    background: var(--card-2); border:1px solid var(--line); border-radius:14px;
    padding:14px 16px;
  }
  .meta-card .num{ font-family:var(--font-mono); font-size:22px; font-weight:700; }
  .meta-card .lbl{ font-size:11.5px; color:var(--text-dim); margin-top:4px; }

  /* ---------- Sections ---------- */
  section{ margin-bottom: 34px; }
  .sec-head{
    display:flex; align-items:center; justify-content:space-between; gap:12px;
    margin-bottom:14px; flex-wrap:wrap;
  }
  .sec-head h2{ margin:0; font-size:17px; font-weight:700; display:flex; align-items:center; gap:10px; }
  .sec-head h2 .idx{
    font-family:var(--font-mono); font-size:11px; color:var(--text-faint);
    border:1px solid var(--line); border-radius:6px; padding:2px 7px;
  }
  .sec-head p.sub{ margin:0; font-size:12.5px; color:var(--text-dim); max-width:640px; }

  .panel{
    background: var(--card); border:1px solid var(--line); border-radius:16px; padding:20px;
  }

  /* ---------- Heatmap ---------- */
  .heatmap-grid{
    display:grid; grid-template-columns: repeat(4, 1fr); gap:10px;
  }
  @media (max-width: 700px){ .heatmap-grid{ grid-template-columns: repeat(2, 1fr); } }
  .heat-cell{
    border-radius:12px; padding:14px; border:1px solid var(--line);
    display:flex; flex-direction:column; gap:6px; min-height:88px; justify-content:space-between;
  }
  .heat-cell .cat{ font-size:13px; font-weight:700; }
  .heat-cell .apps{ font-size:11px; color:rgba(255,255,255,0.7); }
  .heat-low{ background: linear-gradient(135deg, rgba(52,211,153,0.22), rgba(52,211,153,0.06)); }
  .heat-med{ background: linear-gradient(135deg, rgba(242,177,52,0.24), rgba(242,177,52,0.07)); }
  .heat-high{ background: linear-gradient(135deg, rgba(245,137,58,0.28), rgba(245,137,58,0.08)); }
  .heat-vhigh{ background: linear-gradient(135deg, rgba(239,68,68,0.30), rgba(239,68,68,0.08)); }

  /* ---------- Company ranking ---------- */
  .rank-row{ display:flex; align-items:center; gap:12px; margin-bottom:12px; }
  .rank-row:last-child{ margin-bottom:0; }
  .rank-pos{ font-family:var(--font-mono); font-size:12px; color:var(--text-faint); width:20px; flex-shrink:0; }
  .rank-name{ width:130px; flex-shrink:0; font-size:13px; font-weight:600; }
  .rank-track{ flex:1; height:10px; border-radius:6px; background: rgba(255,255,255,0.05); overflow:hidden; }
  .rank-fill{ height:100%; border-radius:6px; background: linear-gradient(90deg, var(--blue), var(--purple)); }
  .rank-val{ font-family:var(--font-mono); font-size:12px; color:var(--text-dim); width:36px; text-align:right; flex-shrink:0; }

  /* ---------- Data collection matrix ---------- */
  .matrix-scroll{ overflow-x:auto; }
  table.matrix{ border-collapse:collapse; width:100%; min-width:760px; }
  table.matrix th, table.matrix td{ padding:9px 10px; text-align:center; font-size:11.5px; border-bottom:1px solid var(--line); }
  table.matrix th{ font-family:var(--font-mono); font-weight:600; color:var(--text-dim); font-size:10.5px; letter-spacing:0.03em; }
  table.matrix td.rowlabel, table.matrix th.rowlabel{ text-align:left; font-weight:600; color:var(--text); white-space:nowrap; }
  .dot{ display:inline-block; width:9px; height:9px; border-radius:50%; }
  .dot-0{ background: rgba(255,255,255,0.10); }
  .dot-1{ background: var(--green); opacity:0.8; }
  .dot-2{ background: var(--amber); }
  .dot-3{ background: var(--red); }
  .matrix-legend{ display:flex; gap:16px; margin-top:14px; flex-wrap:wrap; font-size:11.5px; color:var(--text-dim); align-items:center; }
  .matrix-legend span{ display:inline-flex; align-items:center; gap:6px; }

  /* ---------- Risk radar ---------- */
  .radar-wrap{ display:flex; gap:26px; flex-wrap:wrap; align-items:center; }
  .radar-list{ flex:1; min-width:220px; }
  .radar-item{ display:flex; justify-content:space-between; font-size:12.5px; padding:7px 0; border-bottom:1px solid var(--line); }
  .radar-item:last-child{ border-bottom:none; }
  .radar-item .v{ font-family:var(--font-mono); color:var(--amber); font-weight:700; }

  /* ---------- Digital twin ---------- */
  .twin-grid{ display:grid; grid-template-columns: 1fr 1fr; gap:14px; }
  @media (max-width:700px){ .twin-grid{ grid-template-columns:1fr; } }
  .twin-trait{
    background: var(--card-2); border:1px solid var(--line); border-radius:12px; padding:13px 15px;
  }
  .twin-trait .t-head{ display:flex; justify-content:space-between; align-items:center; margin-bottom:6px; }
  .twin-trait .t-title{ font-size:12.5px; font-weight:700; }
  .twin-trait .t-body{ font-size:12px; color:var(--text-dim); line-height:1.5; }

  /* ---------- WOW insights ---------- */
  .wow-grid{ display:grid; grid-template-columns: repeat(3, 1fr); gap:14px; }
  @media (max-width:900px){ .wow-grid{ grid-template-columns:1fr; } }
  .wow-card{
    background: linear-gradient(160deg, var(--card-2), var(--card));
    border:1px solid var(--line); border-radius:14px; padding:15px;
  }
  .wow-card .icon{ font-size:20px; margin-bottom:8px; display:block; }
  .wow-card p{ font-size:12.5px; color:var(--text-dim); line-height:1.55; margin:0; }
  .wow-card p b{ color:var(--text); }

  /* ---------- Data assets ---------- */
  .asset-row{
    display:flex; align-items:center; gap:14px; padding:12px 0; border-bottom:1px solid var(--line);
  }
  .asset-row:last-child{ border-bottom:none; }
  .asset-rank{
    font-family:var(--font-mono); font-weight:800; font-size:15px; color:var(--purple);
    width:26px; flex-shrink:0;
  }
  .asset-name{ font-weight:700; font-size:13.5px; margin-bottom:2px; }
  .asset-desc{ font-size:11.5px; color:var(--text-dim); line-height:1.4; }
  .asset-value{
    font-family:var(--font-mono); font-size:11px; color:var(--text-dim);
    background: rgba(255,255,255,0.05); padding:4px 9px; border-radius:8px; flex-shrink:0;
  }

  /* ---------- Simulator ---------- */
  .sim-grid{ display:grid; grid-template-columns: 1.3fr 1fr; gap:20px; }
  @media (max-width:900px){ .sim-grid{ grid-template-columns:1fr; } }
  .sim-item{
    display:flex; align-items:flex-start; gap:10px; padding:10px 0; border-bottom:1px solid var(--line);
  }
  .sim-item:last-child{ border-bottom:none; }
  .sim-item input{ margin-top:3px; width:16px; height:16px; accent-color: var(--blue); flex-shrink:0; }
  .sim-item label{ font-size:12.5px; line-height:1.5; color:var(--text); cursor:pointer; }
  .sim-item .pts{ font-family:var(--font-mono); font-size:11px; color:var(--green); margin-left:6px; }
  .sim-result{
    background: var(--card-2); border:1px solid var(--line); border-radius:14px; padding:18px;
    text-align:center; position:sticky; top:16px;
  }
  .sim-result .lbl{ font-family:var(--font-mono); font-size:10.5px; color:var(--text-dim); letter-spacing:0.1em; text-transform:uppercase; }
  .sim-result .val{ font-size:40px; font-weight:800; margin:8px 0; }
  .sim-result .status{ display:inline-block; }
  .sim-result .note{ font-size:11px; color:var(--text-faint); margin-top:12px; line-height:1.5; }

  /* ---------- Final verdict ---------- */
  .verdict{
    background: linear-gradient(135deg, rgba(91,140,255,0.10), rgba(167,139,250,0.06));
    border:1px solid rgba(91,140,255,0.25); border-radius:18px; padding:24px;
  }
  .verdict h2{ margin:0 0 10px; font-size:18px; }
  .verdict p{ font-size:13.5px; color:var(--text-dim); line-height:1.65; margin:0 0 10px; }
  .verdict p:last-child{ margin-bottom:0; }
  .verdict .verdict-tags{ display:flex; gap:8px; flex-wrap:wrap; margin-top:14px; }

  footer.foot{
    text-align:center; font-size:11px; color:var(--text-faint); margin-top:40px; line-height:1.6;
    font-family: var(--font-mono);
  }
</style>

<div class="wrap">

  <div class="top-bar">
    <div>
      <p class="eyebrow">Digital Footprint &amp; Privacy Analysis</p>
      <h1>Your Exposure Dashboard</h1>
      <p>Built from 15 reported services across 11 inferred parent companies. Scores below combine confirmed usage <span class="tag tag-fact">Fact</span> with modeled behavioral inference <span class="tag tag-estimate">Estimate</span> — never certainty, never private data access.</p>
    </div>
    <div class="disclaimer-chip">
      <b>No private databases accessed.</b> All estimates are directional modeling based on publicly known data-collection practices of each platform, not verified facts about you.
    </div>
  </div>

  <!-- SCORE ROW -->
  <div class="score-row">
    <div class="score-card">
      <p class="lbl">Digital Footprint Score</p>
      <div class="big" id="footprintScoreDisplay">74<small>/ 100</small></div>
      <span class="status status-significant">🟠 Significant</span>
      <div class="bar-track"><div class="bar-fill" style="width:74%; background:linear-gradient(90deg,#f5893a,#ef4444);"></div></div>
    </div>
    <div class="score-card">
      <p class="lbl">Privacy Score</p>
      <div class="big" id="privacyScoreDisplay">44<small>/ 100</small></div>
      <span class="status status-fair" id="privacyStatusChip">🟠 Fair</span>
      <div class="bar-track"><div class="bar-fill" id="privacyBar" style="width:44%; background:linear-gradient(90deg,#ef4444,#f2b134);"></div></div>
    </div>
    <div class="score-card">
      <p class="lbl">Ecosystem Concentration</p>
      <div class="big">64<small>/ 100</small></div>
      <span class="status status-significant">🟠 Moderate–High</span>
      <div class="bar-track"><div class="bar-fill" style="width:64%; background:linear-gradient(90deg,#5b8cff,#a78bfa);"></div></div>
    </div>
    <div class="score-card">
      <p class="lbl">Estimated Tracking Surface</p>
      <div class="big" style="font-size:26px;">High <span class="tag tag-estimate" style="margin-left:6px;">Estimate</span></div>
      <span class="status status-significant">🟠 Broad, multi-platform</span>
      <div class="bar-track"><div class="bar-fill" style="width:78%; background:linear-gradient(90deg,#f5893a,#ef4444);"></div></div>
    </div>
  </div>

  <div class="meta-row">
    <div class="meta-card"><div class="num">15</div><div class="lbl">Total Services Used <span class="tag tag-fact">Fact</span></div></div>
    <div class="meta-card"><div class="num">11</div><div class="lbl">Parent Companies <span class="tag tag-fact">Fact</span></div></div>
    <div class="meta-card"><div class="num">27%</div><div class="lbl">Largest Single-Company Share (Google) <span class="tag tag-fact">Fact</span></div></div>
    <div class="meta-card"><div class="num">9</div><div class="lbl">Data Categories Touched <span class="tag tag-estimate">Estimate</span></div></div>
  </div>

  <!-- EXPOSURE HEATMAP -->
  <section>
    <div class="sec-head">
      <h2><span class="idx">01</span> Exposure Heatmap</h2>
      <p class="sub">Category-level intensity, modeled from the number and nature of apps used per category. <span class="tag tag-estimate">Estimate</span></p>
    </div>
    <div class="panel">
      <div class="heatmap-grid">
        <div class="heat-cell heat-vhigh"><div class="cat">Social Media</div><div class="apps">Instagram, Snapchat, TikTok</div></div>
        <div class="heat-cell heat-high"><div class="cat">Messaging</div><div class="apps">WhatsApp, iMessage, Discord</div></div>
        <div class="heat-cell heat-vhigh"><div class="cat">Video &amp; Streaming</div><div class="apps">YouTube, TikTok</div></div>
        <div class="heat-cell heat-med"><div class="cat">Music &amp; Audio</div><div class="apps">Spotify</div></div>
        <div class="heat-cell heat-high"><div class="cat">Gaming</div><div class="apps">Roblox, PUBG Mobile</div></div>
        <div class="heat-cell heat-vhigh"><div class="cat">Shopping &amp; Commerce</div><div class="apps">Amazon, Meesho</div></div>
        <div class="heat-cell heat-high"><div class="cat">Payments &amp; Finance</div><div class="apps">Google Pay</div></div>
        <div class="heat-cell heat-high"><div class="cat">Search &amp; Cloud/Photos</div><div class="apps">Google Search, Google Photos</div></div>
      </div>
    </div>
  </section>

  <!-- COMPANY EXPOSURE RANKING -->
  <section>
    <div class="sec-head">
      <h2><span class="idx">02</span> Company Exposure Ranking</h2>
      <p class="sub">Composite index combining number of services used and typical data breadth per company. <span class="tag tag-estimate">Estimate</span></p>
    </div>
    <div class="panel" id="companyRanking"></div>
  </section>

  <!-- DATA COLLECTION MATRIX -->
  <section>
    <div class="sec-head">
      <h2><span class="idx">03</span> Data Collection Matrix</h2>
      <p class="sub">Likely data types collected per company, based on each platform's known/typical practices — not confirmed for this specific account. <span class="tag tag-estimate">Estimate</span></p>
    </div>
    <div class="panel">
      <div class="matrix-scroll">
        <table class="matrix" id="matrixTable"></table>
      </div>
      <div class="matrix-legend">
        <span><span class="dot dot-0"></span> None / Minimal</span>
        <span><span class="dot dot-1"></span> Low</span>
        <span><span class="dot dot-2"></span> Medium</span>
        <span><span class="dot dot-3"></span> High</span>
      </div>
    </div>
  </section>

  <!-- RISK RADAR -->
  <section>
    <div class="sec-head">
      <h2><span class="idx">04</span> Risk Radar</h2>
      <p class="sub">Six-axis exposure profile modeled from your service mix. <span class="tag tag-estimate">Estimate</span></p>
    </div>
    <div class="panel radar-wrap">
      <svg viewBox="0 0 300 300" width="280" height="280" style="flex-shrink:0;">
        <g id="radarGrid" stroke="rgba(255,255,255,0.10)" fill="none"></g>
        <polygon id="radarPolygon" fill="rgba(91,140,255,0.22)" stroke="#5b8cff" stroke-width="2"></polygon>
        <g id="radarLabels" fill="#8b93ab" font-size="10" font-family="ui-monospace, monospace"></g>
      </svg>
      <div class="radar-list">
        <div class="radar-item"><span>Behavioral / Ad Profiling</span><span class="v">85</span></div>
        <div class="radar-item"><span>Social Graph Exposure</span><span class="v">80</span></div>
        <div class="radar-item"><span>Financial Exposure</span><span class="v">70</span></div>
        <div class="radar-item"><span>Location Tracking Likelihood</span><span class="v">65</span></div>
        <div class="radar-item"><span>Youth / Minor Exposure Risk</span><span class="v">60</span></div>
        <div class="radar-item"><span>Communication Privacy Risk</span><span class="v">55</span></div>
      </div>
    </div>
  </section>

  <!-- DIGITAL TWIN PROFILE -->
  <section>
    <div class="sec-head">
      <h2><span class="idx">05</span> Digital Twin Profile</h2>
      <p class="sub">A modeled persona of the kind of user this footprint typically represents. This is inferred behavior modeling, not a verified identity. <span class="tag tag-estimate">Estimate</span></p>
    </div>
    <div class="panel twin-grid">
      <div class="twin-trait">
        <div class="t-head"><span class="t-title">Lifestyle Pattern</span><span class="tag tag-estimate">Estimate</span></div>
        <div class="t-body">Mobile-first, social, and entertainment-heavy usage (Instagram, Snapchat, TikTok, YouTube, Spotify) alongside active gaming (Roblox, PUBG Mobile) suggests a highly engaged, always-connected digital lifestyle.</div>
      </div>
      <div class="twin-trait">
        <div class="t-head"><span class="t-title">Shopping Behavior</span><span class="tag tag-estimate">Estimate</span></div>
        <div class="t-body">Presence of both Amazon and Meesho suggests price comparison across a premium and a value/budget marketplace — possibly cost-conscious, deal-driven purchasing habits.</div>
      </div>
      <div class="twin-trait">
        <div class="t-head"><span class="t-title">Regional Signal</span><span class="tag tag-estimate">Estimate</span></div>
        <div class="t-body">Google Pay and Meesho are both strongly associated with the Indian digital market, suggesting the user is likely based in or transacting within India.</div>
      </div>
      <div class="twin-trait">
        <div class="t-head"><span class="t-title">Age Range Signal</span><span class="tag tag-estimate">Estimate</span></div>
        <div class="t-body">Roblox and PUBG Mobile skew toward younger and teen audiences industry-wide, which may (not conclusively) suggest a younger user profile.</div>
      </div>
      <div class="twin-trait">
        <div class="t-head"><span class="t-title">Communication Style</span><span class="tag tag-estimate">Estimate</span></div>
        <div class="t-body">A mix of WhatsApp, iMessage, and Discord suggests cross-platform communication across personal, family, and community/gaming contexts.</div>
      </div>
      <div class="twin-trait">
        <div class="t-head"><span class="t-title">Content Consumption</span><span class="tag tag-estimate">Estimate</span></div>
        <div class="t-body">Heavy short-form and streaming presence (TikTok, YouTube, Snapchat) points toward high video/media consumption as a primary entertainment mode.</div>
      </div>
    </div>
  </section>

  <!-- WOW INSIGHTS -->
  <section>
    <div class="sec-head">
      <h2><span class="idx">06</span> WOW Insights</h2>
      <p class="sub">Notable cross-connections in the data. Structural findings are facts; interpretations are estimates.</p>
    </div>
    <div class="wow-grid">
      <div class="wow-card">
        <span class="icon">🔗</span>
        <p><b>4 of your 15 services (27%) funnel through a single company — Google.</b> <span class="tag tag-fact">Fact</span> That's the single largest concentration point in your entire footprint.</p>
      </div>
      <div class="wow-card">
        <span class="icon">💳</span>
        <p><b>Google Pay, Amazon, and Meesho together</b> mean at least 3 of your services likely process financial or purchase-related data. <span class="tag tag-estimate">Estimate</span></p>
      </div>
      <div class="wow-card">
        <span class="icon">🎮</span>
        <p><b>Roblox and PUBG Mobile combined</b> suggest meaningful time spent in gaming ecosystems that also collect in-app behavioral and social data. <span class="tag tag-estimate">Estimate</span></p>
      </div>
      <div class="wow-card">
        <span class="icon">🧩</span>
        <p><b>Meta owns 2 of your services</b> (Instagram, WhatsApp), giving it visibility into both your social graph and private messaging metadata. <span class="tag tag-fact">Fact</span></p>
      </div>
      <div class="wow-card">
        <span class="icon">🔒</span>
        <p>WhatsApp and iMessage both use end-to-end encryption for message content, which meaningfully lowers — but does not eliminate — communication metadata exposure. <span class="tag tag-estimate">Estimate</span></p>
      </div>
      <div class="wow-card">
        <span class="icon">📍</span>
        <p>Shopping apps (Amazon, Meesho) combined with Google services likely create overlapping location signals through delivery addresses and device data. <span class="tag tag-estimate">Estimate</span></p>
      </div>
    </div>
  </section>

  <!-- MOST VALUABLE DATA ASSETS -->
  <section>
    <div class="sec-head">
      <h2><span class="idx">07</span> Most Valuable Data Assets</h2>
      <p class="sub">Ranked by typical advertiser/monetization value across the industry. <span class="tag tag-estimate">Estimate</span></p>
    </div>
    <div class="panel">
      <div class="asset-row">
        <div class="asset-rank">01</div>
        <div style="flex:1;"><div class="asset-name">Purchase &amp; Payment History</div><div class="asset-desc">Google Pay, Amazon, Meesho — directly reveals spending power and buying intent, the highest-value signal for advertisers.</div></div>
        <div class="asset-value">Very High</div>
      </div>
      <div class="asset-row">
        <div class="asset-rank">02</div>
        <div style="flex:1;"><div class="asset-name">Search &amp; Browsing Intent</div><div class="asset-desc">Google Search — near real-time signal of needs, interests, and upcoming decisions.</div></div>
        <div class="asset-value">Very High</div>
      </div>
      <div class="asset-row">
        <div class="asset-rank">03</div>
        <div style="flex:1;"><div class="asset-name">Social Graph &amp; Relationships</div><div class="asset-desc">Instagram, WhatsApp, Snapchat, Discord — maps who you know and interact with most.</div></div>
        <div class="asset-value">High</div>
      </div>
      <div class="asset-row">
        <div class="asset-rank">04</div>
        <div style="flex:1;"><div class="asset-name">Behavioral / Engagement Patterns</div><div class="asset-desc">TikTok, Instagram, YouTube, Snapchat — granular attention and habit data used for feed and ad optimization.</div></div>
        <div class="asset-value">High</div>
      </div>
      <div class="asset-row">
        <div class="asset-rank">05</div>
        <div style="flex:1;"><div class="asset-name">Location History</div><div class="asset-desc">Google services, Amazon/Meesho delivery data, Snapchat — approximate movement and residence patterns.</div></div>
        <div class="asset-value">Medium–High</div>
      </div>
      <div class="asset-row">
        <div class="asset-rank">06</div>
        <div style="flex:1;"><div class="asset-name">Media &amp; Photo Content</div><div class="asset-desc">Google Photos, Instagram, Snapchat — personal images, potentially including faces and location metadata.</div></div>
        <div class="asset-value">Medium</div>
      </div>
      <div class="asset-row">
        <div class="asset-rank">07</div>
        <div style="flex:1;"><div class="asset-name">Communication Metadata</div><div class="asset-desc">WhatsApp, iMessage, Discord — who, when, and how often, even where message content stays encrypted.</div></div>
        <div class="asset-value">Medium</div>
      </div>
    </div>
  </section>

  <!-- PRIVACY IMPROVEMENT SIMULATOR -->
  <section>
    <div class="sec-head">
      <h2><span class="idx">08</span> Privacy Improvement Simulator</h2>
      <p class="sub">Check the actions you're willing to take and see an estimated improved privacy score. Point values are illustrative, not guaranteed. <span class="tag tag-estimate">Estimate</span></p>
    </div>
    <div class="panel sim-grid">
      <div>
        <div class="sim-item">
          <input type="checkbox" data-pts="6" class="simCheck" id="s1"><label for="s1">Turn off ad personalization in your Google Account settings <span class="pts">+6</span></label>
        </div>
        <div class="sim-item">
          <input type="checkbox" data-pts="5" class="simCheck" id="s2"><label for="s2">Limit ad topics and disconnect off-platform activity tracking on Meta (Instagram/WhatsApp) <span class="pts">+5</span></label>
        </div>
        <div class="sim-item">
          <input type="checkbox" data-pts="7" class="simCheck" id="s3"><label for="s3">Review and revoke unused app permissions (location, contacts, microphone) across all 15 apps <span class="pts">+7</span></label>
        </div>
        <div class="sim-item">
          <input type="checkbox" data-pts="4" class="simCheck" id="s4"><label for="s4">Use a separate email/phone number for shopping apps like Meesho and Amazon <span class="pts">+4</span></label>
        </div>
        <div class="sim-item">
          <input type="checkbox" data-pts="6" class="simCheck" id="s5"><label for="s5">Enable 2-Step Verification on Google, Amazon, and WhatsApp <span class="pts">+6</span></label>
        </div>
        <div class="sim-item">
          <input type="checkbox" data-pts="5" class="simCheck" id="s6"><label for="s6">Restrict ad tracking and personalized ads on TikTok, Snapchat, and Instagram <span class="pts">+5</span></label>
        </div>
        <div class="sim-item">
          <input type="checkbox" data-pts="4" class="simCheck" id="s7"><label for="s7">Turn off Google Photos face grouping and review cloud sync for sensitive photos <span class="pts">+4</span></label>
        </div>
        <div class="sim-item">
          <input type="checkbox" data-pts="3" class="simCheck" id="s8"><label for="s8">Review chat and privacy settings on Roblox and PUBG Mobile, especially for younger users <span class="pts">+3</span></label>
        </div>
      </div>
      <div class="sim-result">
        <div class="lbl">Simulated Privacy Score</div>
        <div class="val" id="simScoreVal">44</div>
        <span class="status status-fair" id="simStatusChip">🟠 Fair</span>
        <div class="bar-track"><div class="bar-fill" id="simBar" style="width:44%; background:linear-gradient(90deg,#ef4444,#f2b134);"></div></div>
        <div class="note">Starting score: 44/100. Check items on the left to see how much headroom is available — nothing here is applied automatically to your real accounts.</div>
      </div>
    </div>
  </section>

  <!-- FINAL VERDICT -->
  <section>
    <div class="verdict">
      <h2>Final Verdict</h2>
      <p><b>Digital Footprint:</b> Significant (74/100) <span class="tag tag-fact">Fact-based on service count</span>. Your 15 services span 8 distinct categories of daily life — social, messaging, entertainment, gaming, shopping, and payments — giving you one of the broader footprint profiles in this scoring range.</p>
      <p><b>Privacy Posture:</b> Fair (44/100) <span class="tag tag-estimate">Estimate</span>. The biggest structural risk isn't any single app — it's concentration: Google alone touches search, video, payments, and photos, and Meta connects your social graph to your private messaging. Together they represent roughly a third of your entire tracked surface.</p>
      <p>None of the behavioral, demographic, or lifestyle conclusions above are certain — they are directional patterns based on how these platforms are typically used, not verified facts about you specifically. No private or hidden data source was accessed to produce this report; every inference is built only from the 15 services you listed.</p>
      <div class="verdict-tags">
        <span class="tag tag-fact">15 Services · Fact</span>
        <span class="tag tag-fact">11 Parent Companies · Fact</span>
        <span class="tag tag-estimate">Behavioral Profile · Estimate</span>
        <span class="tag tag-estimate">Risk Radar · Estimate</span>
      </div>
    </div>
  </section>

  <footer class="foot">
    Generated from user-reported service list only · No private databases, no external data brokers, no certainty claims · All estimates are modeled, directional, and non-verifiable
  </footer>

</div>

<script>
(function(){

  // ---------- Company Exposure Ranking ----------
  var companies = [
    { name:"Google",    score:100 },
    { name:"Meta",      score:72 },
    { name:"Amazon",    score:53 },
    { name:"Snap Inc.", score:53 },
    { name:"ByteDance", score:53 },
    { name:"Meesho",    score:47 },
    { name:"Roblox",    score:47 },
    { name:"Krafton",   score:47 },
    { name:"Discord",   score:44 },
    { name:"Apple",     score:35 },
    { name:"Spotify AB",score:35 }
  ];

  var rankingHost = document.getElementById("companyRanking");
  companies.forEach(function(c, i){
    var row = document.createElement("div");
    row.className = "rank-row";
    row.innerHTML =
      '<div class="rank-pos">#'+(i+1)+'</div>' +
      '<div class="rank-name">'+c.name+'</div>' +
      '<div class="rank-track"><div class="rank-fill" style="width:'+c.score+'%;"></div></div>' +
      '<div class="rank-val">'+c.score+'</div>';
    rankingHost.appendChild(row);
  });

  // ---------- Data Collection Matrix ----------
  var matrixCompanies = ["Meta","Snap Inc.","ByteDance","Google","Discord","Apple","Spotify","Roblox","Krafton","Amazon","Meesho"];
  var matrixRows = [
    { label:"Location Data",        vals:[2,3,2,3,1,1,1,1,2,2,2] },
    { label:"Contacts",              vals:[3,2,2,2,2,2,1,1,1,1,1] },
    { label:"Payment / Financial",   vals:[1,1,1,3,1,1,1,2,2,3,2] },
    { label:"Search / Browsing",     vals:[2,1,2,3,1,1,1,1,1,3,2] },
    { label:"Photos / Media",        vals:[3,3,3,3,2,1,1,1,1,1,1] },
    { label:"Social Graph",          vals:[3,2,2,2,2,1,1,2,1,1,1] },
    { label:"Communication Metadata",vals:[2,2,1,1,2,1,0,2,2,1,1] },
    { label:"App Usage Behavior",    vals:[3,3,3,3,2,1,3,3,3,3,2] },
    { label:"Purchase History",      vals:[2,1,2,3,1,1,1,2,2,3,3] }
  ];

  var table = document.getElementById("matrixTable");
  var thead = "<thead><tr><th class='rowlabel'>Data Type</th>" + matrixCompanies.map(function(c){ return "<th>"+c+"</th>"; }).join("") + "</tr></thead>";
  var tbody = "<tbody>" + matrixRows.map(function(r){
    var cells = r.vals.map(function(v){ return "<td><span class='dot dot-"+v+"'></span></td>"; }).join("");
    return "<tr><td class='rowlabel'>"+r.label+"</td>"+cells+"</tr>";
  }).join("") + "</tbody>";
  table.innerHTML = thead + tbody;

  // ---------- Risk Radar ----------
  var radarValues = [85, 80, 70, 65, 60, 55]; // Behavioral, Social, Financial, Location, Youth, Communication
  var radarLabels = ["Behavioral","Social","Financial","Location","Youth","Comms"];
  var cx = 150, cy = 150, maxR = 110;
  var axisCount = radarValues.length;

  function pointFor(index, valuePercent){
    var angle = (Math.PI * 2 * index / axisCount) - Math.PI/2;
    var r = maxR * (valuePercent/100);
    return { x: cx + r * Math.cos(angle), y: cy + r * Math.sin(angle) };
  }

  var gridGroup = document.getElementById("radarGrid");
  [0.25, 0.5, 0.75, 1].forEach(function(scale){
    var pts = [];
    for (var i=0;i<axisCount;i++){
      var p = pointFor(i, 100*scale);
      pts.push(p.x+","+p.y);
    }
    var poly = document.createElementNS("http://www.w3.org/2000/svg","polygon");
    poly.setAttribute("points", pts.join(" "));
    gridGroup.appendChild(poly);
  });
  for (var i=0;i<axisCount;i++){
    var outer = pointFor(i, 100);
    var line = document.createElementNS("http://www.w3.org/2000/svg","line");
    line.setAttribute("x1", cx); line.setAttribute("y1", cy);
    line.setAttribute("x2", outer.x); line.setAttribute("y2", outer.y);
    gridGroup.appendChild(line);
  }

  var polyPoints = radarValues.map(function(v, i){
    var p = pointFor(i, v);
    return p.x+","+p.y;
  }).join(" ");
  document.getElementById("radarPolygon").setAttribute("points", polyPoints);

  var labelGroup = document.getElementById("radarLabels");
  radarLabels.forEach(function(lab, i){
    var p = pointFor(i, 118);
    var t = document.createElementNS("http://www.w3.org/2000/svg","text");
    t.setAttribute("x", p.x);
    t.setAttribute("y", p.y);
    t.setAttribute("text-anchor","middle");
    t.textContent = lab;
    labelGroup.appendChild(t);
  });

  // ---------- Privacy Simulator ----------
  var baseScore = 44;
  var simVal = document.getElementById("simScoreVal");
  var simBar = document.getElementById("simBar");
  var simChip = document.getElementById("simStatusChip");
  var checks = document.querySelectorAll(".simCheck");

  function statusFor(score){
    if (score <= 30) return { txt:"🔴 Weak", cls:"status-weak" };
    if (score <= 60) return { txt:"🟠 Fair", cls:"status-fair" };
    if (score <= 80) return { txt:"🟡 Good", cls:"status-good" };
    return { txt:"🟢 Strong", cls:"status-strong" };
  }

  function recalcSim(){
    var total = baseScore;
    checks.forEach(function(c){
      if (c.checked) total += parseInt(c.getAttribute("data-pts"), 10);
    });
    total = Math.min(total, 96);
    simVal.textContent = total;
    simBar.style.width = total + "%";
    var st = statusFor(total);
    simChip.textContent = st.txt;
    simChip.className = "status " + st.cls;
  }

  checks.forEach(function(c){ c.addEventListener("change", recalcSim); });
  recalcSim();

})();
</script>


SCREENSHOTS:
<img width="1551" height="1002" alt="Screenshot 2026-07-16 120304" src="https://github.com/user-attachments/assets/5b3e20d0-a4f4-4583-a28e-847dca34ce74" />
<img width="1582" height="1000" alt="Screenshot 2026-07-16 120317" src="https://github.com/user-attachments/assets/0eee6c0c-6d00-4e7c-9dff-893fbf66f652" />
<img width="1571" height="992" alt="Screenshot 2026-07-16 120331" src="https://github.com/user-attachments/assets/960fee45-cc77-4446-a645-9be74a4271f1" />
<img width="1646" height="981" alt="Screenshot 2026-07-16 120345" src="https://github.com/user-attachments/assets/6a359f43-1295-4025-917c-bdf781692194" />
<img width="1708" height="983" alt="Screenshot 2026-07-16 120421" src="https://github.com/user-attachments/assets/463b76a9-10ec-4911-887c-ad583f5d3dfb" />
<img width="1626" height="961" alt="Screenshot 2026-07-16 120435" src="https://github.com/user-attachments/assets/26eb3761-1193-4ae8-a61a-24fb7f82503b" />

