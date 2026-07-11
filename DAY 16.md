Analyze Indian (NSE/BSE) and global listed companies using fundamentals, financial statements, business quality, competitive advantages, valuation, and risks, and produce evidence-based equity research reports. Use this skill whenever the user asks to analyze, research, evaluate, or "look into" a stock or company's fundamentals, asks for a quick take, deep dive, comparison, pros/cons, or portfolio-fit on a listed company, mentions ticker symbols, P/E, ROE, ROCE, moat, valuation, or asks things like "is this stock cheap", "how healthy is this company's balance sheet", or "should I look at X vs Y" — even if they don't use the word "fundamentals" explicitly. This skill NEVER gives buy/sell/hold calls, target prices, or personalized investment advice — it always produces neutral, evidence-based analysis instead.Stock Fundamental Analyzer
Analyze listed stocks (NSE/BSE primarily, but the same approach applies to global companies) using fundamentals only. The goal is to give the user a clear, evidence-based picture of a company's financial health, quality, and valuation context — never a recommendation. This distinction matters: people read a lot into what an AI says about a stock, so the analysis needs to stay descriptive ("here's what the numbers show") rather than prescriptive ("here's what you should do").
Step 1: Figure out the mode
Read the user's request and pick the mode it matches:

Quick Take — default when the user just names a stock or asks a short/simple question about it.
Deep Dive — user asks for a detailed, thorough, or "full" analysis.
Compare — user names two (or more) stocks, or asks to compare/vs.
Pros & Cons — user specifically asks for strengths/weaknesses or risks.
Portfolio Fit — user shares their existing holdings and asks how a stock would fit alongside them.

If it's ambiguous, Quick Take is the safe default — it's short enough that offering a Deep Dive afterward costs little, and the closing line of Quick Take already invites that follow-up.
Step 2: Gather data
Live, current data is the whole point of this skill — stale fundamentals produce misleading analysis, so treat data-gathering as seriously as the write-up itself.
Source priority (for Indian stocks): Screener.in > Tickertape > Moneycontrol > NSE/BSE filings > Annual Reports > earnings call transcripts. For global companies, use the equivalent primary sources (company IR pages, 10-K/10-Q filings, or reputable financial data sites) since Screener/Tickertape/Moneycontrol are India-specific.
Cross-check important figures (valuation multiples, margins, debt ratios) across at least two sources before presenting them — a single source could be stale or wrong, and this is exactly the kind of number a user might act on.
If a figure can't be verified or fetched:

Mark it inline: 🚩 Data unavailable — verify at [source]
If live retrieval fails entirely for a request, say so plainly near the top: "Live data couldn't be fetched; figures below may be outdated."

Never fabricate a number. An estimate presented as fact is worse than an honest gap — flag it and move on.
Cite the source next to every key figure you present (not just once at the end) so the user can trace where each number came from.
Step 3: Build the picture using this checklist
Not every field is needed for every mode (see Output Formats below for what each mode actually surfaces), but pull from this list as the backbone of the research:
Valuation & size: CMP, Market Cap, Face Value, 52-week High/Low; P/E, P/B, EV/EBITDA — each compared against sector peers and the company's own 5-year average.
Growth: Revenue, Profit, EPS CAGR (3Y and 5Y); EPS for the last 8 quarters.
Profitability & cash generation: EBITDA Margin and Net Profit Margin (5-year trend); Free Cash Flow (3–5Y).
Balance sheet health: Debt/Equity, Interest Coverage, Current Ratio.
Returns: ROE and ROCE — current, 3-year average, 5-year average.
Shareholder-friendliness: Dividend history and payout ratio.
Ownership signals: Promoter holding trend and pledging (flag if pledging >10%); FII/DII holding trend over the last 8 quarters.
Qualitative: Moat, pricing power, brand strength, switching costs, market share; management quality and governance track record; sector tailwinds/headwinds; latest earnings call commentary; recent notable news.
Peers: 3 closest peers with their P/E, P/B, ROE, Revenue Growth, and D/E for context.
Step 4: Interpret using these fixed thresholds
Apply these consistently rather than freehand judgment calls — they keep the analysis reproducible and defensible:
MetricThresholdsValuationCheap = below sector & own history; Fair = within ~10% of both; Expensive = above bothDebt/Equity<1 Safe · 1–2 Moderate · >2 LeveragedInterest Coverage>3 Healthy · 1.5–3 Watch · <1.5 RiskCurrent Ratio>1.5 Comfortable · 1–1.5 Watch · <1 RiskFree Cash FlowPositive & growing = Strong · Positive & stable = Stable · Negative = ConcernROE / ROCE>15% Good · 10–15% Average · <10% WeakGrowth trendAccelerating · Steady · Slowing · Declining
Explain jargon briefly the first time a term appears (e.g., "ROCE (Return on Capital Employed, which shows...)") since not every reader is a finance professional.
Step 5: Produce the output
Quick Take (150–220 words)
Company overview → CMP, Market Cap, P/E with valuation verdict → D/E, ROE, ROCE → growth trend → 3 strengths → 2 watch-points → Fundamental Quality verdict (Strong/Moderate/Weak) with a one-line reason. Include a price chart of the stock. End with: "Want the full Deep Dive?"
Deep Dive
Use assets/deep-dive-template.html. Replace every placeholder with real, sourced data (never leave a placeholder in the output — if a figure is unavailable, insert the 🚩 flag text instead of deleting the field). Output the completed file as an HTML artifact. Tabs: Snapshot, Valuation, Growth, Health, Returns, Peers, Ownership, View. The View tab must contain: strengths, watch-points, one key metric worth tracking going forward, an overall quality verdict, the closing disclaimer, and a data-confidence rating (High/Moderate/Low) reflecting how much of the checklist you could verify.
Compare
Side-by-side table: CMP, Market Cap, P/E, P/B, EV/EBITDA, Revenue CAGR, Profit CAGR, EBITDA Margin, ROE, ROCE, D/E, Promoter Holding, Pledging, Dividend. Include price charts for both stocks. Structure the narrative as "Where A Leads" / "Where B Leads" plus a neutral summary — deliberately avoid naming an overall winner, since that starts to shade into a recommendation.
Pros & Cons
3–5 evidence-backed strengths, 3–5 evidence-backed risks, each tied to a specific figure or fact — not generic statements — followed by a short balanced summary.
Portfolio Fit
Given the user's stated holdings: concentration analysis, sector overlap, what this stock would add that's missing, what it would duplicate, and a compact fundamental snapshot of the candidate stock. Discuss fit descriptively — what the addition would mean for the portfolio's shape — without advising whether to act on it.
Charts
Every mode benefits from a price chart — include one (image search or a rendered chart) alongside the numbers rather than describing price action in prose alone.
Closing line
Every output — regardless of mode — ends with:

This is a view of the fundamentals for educational purposes only. It is not investment advice and not a buy/sell/hold recommendation. Verify all figures independently. The final decision is yours.

The one hard rule
Never produce a buy/sell/hold call, a target price, or advice framed as "you should..." — even if the user asks directly or rephrases the request to try to get one
. Redirect back to the fundamentals: describe what the data shows and let the user draw their own conclusion.


HTML OF SKILLL
<style>
  .sfr-wrap {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    max-width: 900px;
    margin: 0 auto;
    color: #1a1a1a;
    background: #ffffff;
  }
  .sfr-header {
    padding: 20px 24px;
    border-bottom: 1px solid #e5e5e5;
  }
  .sfr-header h1 {
    margin: 0 0 4px 0;
    font-size: 22px;
  }
  .sfr-header .sfr-sub {
    color: #666;
    font-size: 14px;
  }
  .sfr-tabs {
    display: flex;
    flex-wrap: wrap;
    border-bottom: 2px solid #e5e5e5;
    background: #fafafa;
  }
  .sfr-tab-btn {
    padding: 10px 16px;
    font-size: 13px;
    font-weight: 600;
    color: #666;
    background: none;
    border: none;
    cursor: pointer;
    border-bottom: 2px solid transparent;
    margin-bottom: -2px;
  }
  .sfr-tab-btn.active {
    color: #1a1a1a;
    border-bottom: 2px solid #1a1a1a;
  }
  .sfr-panel { display: none; padding: 20px 24px; }
  .sfr-panel.active { display: block; }
  .sfr-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    gap: 12px;
    margin: 12px 0;
  }
  .sfr-metric {
    border: 1px solid #eee;
    border-radius: 8px;
    padding: 10px 14px;
  }
  .sfr-metric .label { font-size: 12px; color: #888; }
  .sfr-metric .value { font-size: 18px; font-weight: 700; margin-top: 2px; }
  .sfr-metric .src { font-size: 11px; color: #aaa; margin-top: 2px; }
  .sfr-verdict {
    display: inline-block;
    padding: 2px 10px;
    border-radius: 12px;
    font-size: 12px;
    font-weight: 700;
  }
  .sfr-verdict.good { background: #e6f4ea; color: #1e7e34; }
  .sfr-verdict.watch { background: #fff4e5; color: #b06000; }
  .sfr-verdict.risk { background: #fdeaea; color: #b00020; }
  table.sfr-table { width: 100%; border-collapse: collapse; margin: 12px 0; font-size: 13px; }
  table.sfr-table th, table.sfr-table td { text-align: left; padding: 8px 10px; border-bottom: 1px solid #eee; }
  table.sfr-table th { color: #888; font-weight: 600; }
  .sfr-list { margin: 8px 0; padding-left: 20px; }
  .sfr-list li { margin-bottom: 6px; font-size: 14px; }
  .sfr-flag { color: #b06000; font-size: 13px; }
  .sfr-disclaimer {
    font-size: 12px;
    color: #888;
    border-top: 1px solid #eee;
    margin-top: 16px;
    padding-top: 12px;
  }
  .sfr-confidence { font-size: 13px; margin-top: 8px; }
</style>

<div class="sfr-wrap">
  <div class="sfr-header">
    <h1>{{COMPANY_NAME}} ({{TICKER}})</h1>
    <div class="sfr-sub">{{SECTOR}} · {{EXCHANGE}} · Data as of {{DATA_DATE}}</div>
  </div>

  <div class="sfr-tabs">
    <button class="sfr-tab-btn active" onclick="sfrShow('snapshot', this)">Snapshot</button>
    <button class="sfr-tab-btn" onclick="sfrShow('valuation', this)">Valuation</button>
    <button class="sfr-tab-btn" onclick="sfrShow('growth', this)">Growth</button>
    <button class="sfr-tab-btn" onclick="sfrShow('health', this)">Health</button>
    <button class="sfr-tab-btn" onclick="sfrShow('returns', this)">Returns</button>
    <button class="sfr-tab-btn" onclick="sfrShow('peers', this)">Peers</button>
    <button class="sfr-tab-btn" onclick="sfrShow('ownership', this)">Ownership</button>
    <button class="sfr-tab-btn" onclick="sfrShow('view', this)">View</button>
  </div>

  <!-- SNAPSHOT -->
  <div class="sfr-panel active" id="sfr-snapshot">
    <div class="sfr-grid">
      <div class="sfr-metric"><div class="label">CMP</div><div class="value">{{CMP}}</div><div class="src">{{CMP_SOURCE}}</div></div>
      <div class="sfr-metric"><div class="label">Market Cap</div><div class="value">{{MARKET_CAP}}</div><div class="src">{{MARKET_CAP_SOURCE}}</div></div>
      <div class="sfr-metric"><div class="label">Face Value</div><div class="value">{{FACE_VALUE}}</div></div>
      <div class="sfr-metric"><div class="label">52W High/Low</div><div class="value">{{FIFTY_TWO_WK_HIGH}} / {{FIFTY_TWO_WK_LOW}}</div></div>
    </div>
    <p>{{COMPANY_OVERVIEW}}</p>
    <div><strong>Price Chart</strong></div>
    <div>{{PRICE_CHART}}</div>
  </div>

  <!-- VALUATION -->
  <div class="sfr-panel" id="sfr-valuation">
    <div class="sfr-grid">
      <div class="sfr-metric"><div class="label">P/E</div><div class="value">{{PE}}</div><div class="src">Sector: {{PE_SECTOR}} · 5Y avg: {{PE_5Y_AVG}} · {{PE_SOURCE}}</div></div>
      <div class="sfr-metric"><div class="label">P/B</div><div class="value">{{PB}}</div><div class="src">Sector: {{PB_SECTOR}} · 5Y avg: {{PB_5Y_AVG}} · {{PB_SOURCE}}</div></div>
      <div class="sfr-metric"><div class="label">EV/EBITDA</div><div class="value">{{EV_EBITDA}}</div><div class="src">Sector: {{EV_EBITDA_SECTOR}} · 5Y avg: {{EV_EBITDA_5Y_AVG}} · {{EV_EBITDA_SOURCE}}</div></div>
    </div>
    <p><strong>Valuation verdict:</strong> <span class="sfr-verdict {{VALUATION_VERDICT_CLASS}}">{{VALUATION_VERDICT}}</span> — {{VALUATION_EXPLANATION}}</p>
  </div>

  <!-- GROWTH -->
  <div class="sfr-panel" id="sfr-growth">
    <div class="sfr-grid">
      <div class="sfr-metric"><div class="label">Revenue CAGR (3Y)</div><div class="value">{{REVENUE_CAGR_3Y}}</div></div>
      <div class="sfr-metric"><div class="label">Revenue CAGR (5Y)</div><div class="value">{{REVENUE_CAGR_5Y}}</div></div>
      <div class="sfr-metric"><div class="label">Profit CAGR (3Y)</div><div class="value">{{PROFIT_CAGR_3Y}}</div></div>
      <div class="sfr-metric"><div class="label">Profit CAGR (5Y)</div><div class="value">{{PROFIT_CAGR_5Y}}</div></div>
      <div class="sfr-metric"><div class="label">EPS CAGR (3Y)</div><div class="value">{{EPS_CAGR_3Y}}</div></div>
      <div class="sfr-metric"><div class="label">EPS CAGR (5Y)</div><div class="value">{{EPS_CAGR_5Y}}</div></div>
    </div>
    <p><strong>Growth trend:</strong> {{GROWTH_TREND}}</p>
    <table class="sfr-table">
      <thead><tr><th>Quarter</th><th>EPS</th></tr></thead>
      <tbody>{{EPS_LAST_8_QUARTERS_ROWS}}</tbody>
    </table>
  </div>

  <!-- HEALTH -->
  <div class="sfr-panel" id="sfr-health">
    <div class="sfr-grid">
      <div class="sfr-metric"><div class="label">Debt/Equity</div><div class="value">{{DEBT_EQUITY}}</div><div class="src"><span class="sfr-verdict {{DEBT_EQUITY_VERDICT_CLASS}}">{{DEBT_EQUITY_VERDICT}}</span></div></div>
      <div class="sfr-metric"><div class="label">Interest Coverage</div><div class="value">{{INTEREST_COVERAGE}}</div><div class="src"><span class="sfr-verdict {{INTEREST_COVERAGE_VERDICT_CLASS}}">{{INTEREST_COVERAGE_VERDICT}}</span></div></div>
      <div class="sfr-metric"><div class="label">Current Ratio</div><div class="value">{{CURRENT_RATIO}}</div><div class="src"><span class="sfr-verdict {{CURRENT_RATIO_VERDICT_CLASS}}">{{CURRENT_RATIO_VERDICT}}</span></div></div>
      <div class="sfr-metric"><div class="label">Free Cash Flow (trend)</div><div class="value">{{FCF_TREND}}</div><div class="src"><span class="sfr-verdict {{FCF_VERDICT_CLASS}}">{{FCF_VERDICT}}</span></div></div>
    </div>
    <p><strong>EBITDA Margin (5Y):</strong> {{EBITDA_MARGIN_5Y}} &nbsp; | &nbsp; <strong>Net Profit Margin (5Y):</strong> {{NPM_5Y}}</p>
  </div>

  <!-- RETURNS -->
  <div class="sfr-panel" id="sfr-returns">
    <div class="sfr-grid">
      <div class="sfr-metric"><div class="label">ROE (current)</div><div class="value">{{ROE_CURRENT}}</div></div>
      <div class="sfr-metric"><div class="label">ROE (3Y avg)</div><div class="value">{{ROE_3Y_AVG}}</div></div>
      <div class="sfr-metric"><div class="label">ROE (5Y avg)</div><div class="value">{{ROE_5Y_AVG}}</div></div>
      <div class="sfr-metric"><div class="label">ROCE (current)</div><div class="value">{{ROCE_CURRENT}}</div></div>
      <div class="sfr-metric"><div class="label">ROCE (3Y avg)</div><div class="value">{{ROCE_3Y_AVG}}</div></div>
      <div class="sfr-metric"><div class="label">ROCE (5Y avg)</div><div class="value">{{ROCE_5Y_AVG}}</div></div>
    </div>
    <p><strong>Dividend history:</strong> {{DIVIDEND_HISTORY}} &nbsp; | &nbsp; <strong>Payout ratio:</strong> {{PAYOUT_RATIO}}</p>
  </div>

  <!-- PEERS -->
  <div class="sfr-panel" id="sfr-peers">
    <table class="sfr-table">
      <thead><tr><th>Company</th><th>P/E</th><th>P/B</th><th>ROE</th><th>Revenue Growth</th><th>D/E</th></tr></thead>
      <tbody>
        <tr><td>{{COMPANY_NAME}} (this company)</td><td>{{PE}}</td><td>{{PB}}</td><td>{{ROE_CURRENT}}</td><td>{{REVENUE_CAGR_3Y}}</td><td>{{DEBT_EQUITY}}</td></tr>
        {{PEER_ROWS}}
      </tbody>
    </table>
  </div>

  <!-- OWNERSHIP -->
  <div class="sfr-panel" id="sfr-ownership">
    <div class="sfr-grid">
      <div class="sfr-metric"><div class="label">Promoter Holding</div><div class="value">{{PROMOTER_HOLDING}}</div><div class="src">Trend: {{PROMOTER_HOLDING_TREND}}</div></div>
      <div class="sfr-metric"><div class="label">Pledging</div><div class="value">{{PLEDGING}}</div><div class="src">{{PLEDGING_FLAG}}</div></div>
    </div>
    <table class="sfr-table">
      <thead><tr><th>Quarter</th><th>FII %</th><th>DII %</th></tr></thead>
      <tbody>{{FII_DII_ROWS}}</tbody>
    </table>
  </div>

  <!-- VIEW -->
  <div class="sfr-panel" id="sfr-view">
    <p><strong>Overall fundamental quality:</strong> <span class="sfr-verdict {{OVERALL_QUALITY_CLASS}}">{{OVERALL_QUALITY}}</span></p>

    <p><strong>Strengths</strong></p>
    <ul class="sfr-list">{{STRENGTHS_LIST}}</ul>

    <p><strong>Watch-points</strong></p>
    <ul class="sfr-list">{{WATCHPOINTS_LIST}}</ul>

    <p><strong>Key metric to track going forward:</strong> {{KEY_METRIC_TO_TRACK}}</p>

    <p class="sfr-confidence"><strong>Data confidence:</strong> {{DATA_CONFIDENCE}}</p>

    <div class="sfr-disclaimer">
      This is a view of the fundamentals for educational purposes only. It is not investment advice and not a buy/sell/hold recommendation. Verify all figures independently. The final decision is yours.
    </div>
  </div>
</div>

<script>
function sfrShow(id, btn) {
  document.querySelectorAll('.sfr-panel').forEach(function(p) { p.classList.remove('active'); });
  document.querySelectorAll('.sfr-tab-btn').forEach(function(b) { b.classList.remove('active'); });
  document.getElementById('sfr-' + id).classList.add('active');
  btn.classList.add('active');
}
</script>
