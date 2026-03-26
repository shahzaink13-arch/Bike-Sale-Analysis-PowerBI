<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Bike Sales Power BI Dashboard README</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --primary:       #E65100;
    --primary-light: #FF8A50;
    --green:         #2E7D32;
    --green-light:   #66BB6A;
    --blue:          #0D47A1;
    --blue-light:    #64B5F6;
    --gold:          #F9A825;
    --purple:        #6A1B9A;
    --purple-light:  #CE93D8;
    --white:         #F5F5F5;
    --dark:          #0D1117;
    --card-bg:       #161B22;
    --border:        rgba(255,255,255,0.08);
  }

  * { margin:0; padding:0; box-sizing:border-box; }

  body {
    background: var(--dark);
    color: var(--white);
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    line-height: 1.7;
    overflow-x: hidden;
  }

  /* HERO */
  .hero {
    position: relative;
    padding: 80px 40px 64px;
    text-align: center;
    overflow: hidden;
  }
  .hero::before {
    content:'';
    position:absolute; inset:0;
    background:
      radial-gradient(ellipse 80% 55% at 50% 0%,  rgba(230,81,0,0.18)    0%, transparent 70%),
      radial-gradient(ellipse 50% 40% at 5%  80%, rgba(13,71,161,0.14)   0%, transparent 60%),
      radial-gradient(ellipse 50% 40% at 95% 80%, rgba(46,125,50,0.14)   0%, transparent 60%);
    z-index:0;
  }
  .hero-icon { font-size:3rem; margin-bottom:20px; position:relative; z-index:1; }
  .hero-eyebrow {
    font-family:'Syne',sans-serif;
    font-size:11px; letter-spacing:4px; text-transform:uppercase;
    color:var(--primary-light); margin-bottom:16px;
    position:relative; z-index:1;
  }
  .hero h1 {
    font-family:'Syne',sans-serif;
    font-size:clamp(2.2rem,5vw,3.6rem);
    font-weight:800; line-height:1.1;
    margin-bottom:20px; position:relative; z-index:1;
  }
  .hero h1 .c-orange { color:var(--primary); }
  .hero h1 .c-blue   { color:var(--blue-light); }
  .hero h1 .c-green  { color:var(--green-light); }

  .hero-sub {
    font-size:16px; color:rgba(255,255,255,0.6);
    max-width:640px; margin:0 auto 36px;
    position:relative; z-index:1;
  }
  .badge-row {
    display:flex; flex-wrap:wrap; gap:10px;
    justify-content:center; position:relative; z-index:1;
  }
  .badge {
    padding:6px 16px; border-radius:999px;
    font-size:12px; font-weight:500; letter-spacing:0.5px; border:1px solid;
  }
  .b-orange { background:rgba(230,81,0,0.12);   border-color:var(--primary);       color:var(--primary-light); }
  .b-blue   { background:rgba(13,71,161,0.12);   border-color:var(--blue-light);    color:var(--blue-light); }
  .b-green  { background:rgba(46,125,50,0.12);   border-color:var(--green);         color:var(--green-light); }
  .b-gold   { background:rgba(249,168,37,0.12);  border-color:var(--gold);          color:var(--gold); }
  .b-purple { background:rgba(106,27,154,0.12);  border-color:var(--purple-light);  color:var(--purple-light); }

  /* DIVIDER */
  .divider { display:flex; height:4px; width:100%; }
  .divider span:nth-child(1) { flex:1; background:var(--primary); }
  .divider span:nth-child(2) { flex:1; background:var(--blue-light); }
  .divider span:nth-child(3) { flex:1; background:var(--green-light); }

  /* LAYOUT */
  .container { max-width:980px; margin:0 auto; padding:60px 40px; }
  .section    { margin-bottom:56px; }

  /* SECTION TITLE */
  .section-title {
    font-family:'Syne',sans-serif;
    font-size:1.5rem; font-weight:700;
    margin-bottom:24px; display:flex; align-items:center; gap:12px;
  }
  .icon {
    width:36px; height:36px; border-radius:10px;
    display:flex; align-items:center; justify-content:center;
    font-size:18px; flex-shrink:0;
  }
  .i-orange { background:rgba(230,81,0,0.18); }
  .i-blue   { background:rgba(13,71,161,0.18); }
  .i-green  { background:rgba(46,125,50,0.18); }
  .i-gold   { background:rgba(249,168,37,0.18); }
  .i-purple { background:rgba(106,27,154,0.18); }

  /* CARD */
  .card {
    background:var(--card-bg); border:1px solid var(--border);
    border-radius:16px; padding:28px; margin-bottom:16px;
  }

  /* KPI GRID */
  .kpi-grid {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(150px,1fr));
    gap:14px; margin-bottom:40px;
  }
  .kpi-card {
    background:var(--card-bg); border:1px solid var(--border);
    border-radius:14px; padding:20px 16px;
    text-align:center; position:relative; overflow:hidden;
  }
  .kpi-card::before {
    content:''; position:absolute; top:0; left:0; right:0; height:3px;
  }
  .kpi-card.k-orange::before { background:var(--primary); }
  .kpi-card.k-blue::before   { background:var(--blue-light); }
  .kpi-card.k-green::before  { background:var(--green-light); }
  .kpi-card.k-gold::before   { background:var(--gold); }
  .kpi-card.k-purple::before { background:var(--purple-light); }
  .kpi-card.k-white::before  { background:white; }

  .kpi-value {
    font-family:'Syne',sans-serif;
    font-size:1.65rem; font-weight:800; line-height:1; margin-bottom:8px;
  }
  .kpi-card.k-orange .kpi-value { color:var(--primary); }
  .kpi-card.k-blue   .kpi-value { color:var(--blue-light); }
  .kpi-card.k-green  .kpi-value { color:var(--green-light); }
  .kpi-card.k-gold   .kpi-value { color:var(--gold); }
  .kpi-card.k-purple .kpi-value { color:var(--purple-light); }
  .kpi-card.k-white  .kpi-value { color:white; }
  .kpi-label { font-size:11px; color:rgba(255,255,255,0.5); letter-spacing:0.5px; text-transform:uppercase; }

  /* VISUALS GRID */
  .visuals-grid {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
    gap:14px; margin-bottom:40px;
  }
  .visual-card {
    background:var(--card-bg); border:1px solid var(--border);
    border-radius:14px; padding:20px;
    display:flex; gap:14px; align-items:flex-start;
  }
  .visual-num {
    font-family:'Syne',sans-serif;
    font-size:1.4rem; font-weight:800; line-height:1;
    min-width:32px; opacity:0.3;
  }
  .visual-info h4 {
    font-family:'Syne',sans-serif;
    font-size:0.95rem; font-weight:600; margin-bottom:6px; color:white;
  }
  .visual-info p { font-size:12.5px; color:rgba(255,255,255,0.5); line-height:1.5; }

  /* ANALYSIS GRID */
  .analysis-grid {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(290px,1fr));
    gap:14px; margin-bottom:40px;
  }
  .analysis-card {
    background:var(--card-bg); border:1px solid var(--border);
    border-radius:14px; padding:22px;
  }
  .analysis-card h4 {
    font-family:'Syne',sans-serif;
    font-size:1rem; font-weight:700; margin-bottom:10px;
    display:flex; align-items:center; gap:8px;
  }
  .dot { width:8px; height:8px; border-radius:50%; flex-shrink:0; }
  .d-orange { background:var(--primary); }
  .d-blue   { background:var(--blue-light); }
  .d-green  { background:var(--green-light); }
  .d-gold   { background:var(--gold); }
  .d-purple { background:var(--purple-light); }
  .analysis-card p { font-size:13px; color:rgba(255,255,255,0.55); line-height:1.65; }

  /* CATEGORY CARDS */
  .cat-grid {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
    gap:14px; margin-bottom:40px;
  }
  .cat-card {
    background:var(--card-bg); border:1px solid var(--border);
    border-radius:14px; padding:20px; text-align:center;
  }
  .cat-icon  { font-size:2rem; margin-bottom:10px; }
  .cat-name  { font-family:'Syne',sans-serif; font-size:1rem; font-weight:700; margin-bottom:6px; }
  .cat-units { font-family:'Syne',sans-serif; font-size:1.4rem; font-weight:800; }
  .cat-sub   { font-size:11px; color:rgba(255,255,255,0.4); margin-top:4px; }

  /* TECH PILLS */
  .tech-row { display:flex; flex-wrap:wrap; gap:10px; margin-bottom:40px; }
  .tech-pill {
    display:flex; align-items:center; gap:8px;
    padding:10px 18px;
    background:var(--card-bg); border:1px solid var(--border);
    border-radius:999px; font-size:13px; font-weight:500;
  }
  .tech-pill .dot { width:7px; height:7px; }

  /* INSIGHT LIST */
  .insight-list { list-style:none; margin-bottom:40px; }
  .insight-list li {
    display:flex; gap:14px; align-items:flex-start;
    padding:14px 0; border-bottom:1px solid var(--border);
    font-size:14px; color:rgba(255,255,255,0.7);
  }
  .insight-list li:last-child { border-bottom:none; }
  .insight-list li .num {
    font-family:'Syne',sans-serif;
    font-size:1rem; font-weight:800; color:var(--primary); min-width:24px;
  }

  /* TREE */
  .tree {
    background:var(--card-bg); border:1px solid var(--border);
    border-radius:14px; padding:24px 28px;
    font-family:'Courier New',monospace;
    font-size:13px; line-height:1.9; margin-bottom:40px;
    color:rgba(255,255,255,0.7);
  }
  .tree .folder { color:var(--gold); font-weight:bold; }
  .tree .file   { color:var(--green-light); }
  .tree .item   { color:var(--blue-light); }

  /* DAX BLOCK */
  .dax-grid {
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(300px,1fr));
    gap:14px; margin-bottom:40px;
  }
  .dax-card {
    background:var(--card-bg); border:1px solid var(--border);
    border-radius:14px; padding:20px;
  }
  .dax-card h4 {
    font-family:'Syne',sans-serif;
    font-size:0.9rem; font-weight:700;
    color:var(--gold); margin-bottom:12px;
    display:flex; align-items:center; gap:8px;
  }
  .dax-card pre {
    font-family:'Courier New',monospace;
    font-size:12px; color:rgba(255,255,255,0.65);
    line-height:1.7; white-space:pre-wrap;
    background:rgba(0,0,0,0.3); padding:12px;
    border-radius:8px; border-left:3px solid var(--primary);
  }

  /* FOOTER */
  .footer {
    text-align:center; padding:40px;
    border-top:1px solid var(--border);
    color:rgba(255,255,255,0.35); font-size:13px;
  }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity:0; transform:translateY(20px); }
    to   { opacity:1; transform:translateY(0); }
  }
  .hero > * { animation:fadeUp 0.6s ease both; }
  .hero .hero-icon    { animation-delay:0.05s; }
  .hero .hero-eyebrow { animation-delay:0.15s; }
  .hero h1            { animation-delay:0.25s; }
  .hero .hero-sub     { animation-delay:0.35s; }
  .hero .badge-row    { animation-delay:0.45s; }
</style>
</head>
<body>

<!-- HERO -->
<div class="hero">
  <div class="hero-icon">🚲</div>
  <p class="hero-eyebrow">📊 Power BI Dashboard Project</p>
  <h1>
    <span class="c-orange">Bike</span> <span class="c-blue">Sales</span><br>
    <span class="c-green">Analytics</span> Dashboard
  </h1>
  <p class="hero-sub">
    An interactive Power BI dashboard analyzing $25M in sales across
    Accessories, Bikes & Clothing categories from 2015–2017,
    covering 25,164 orders across multiple countries and continents.
  </p>
  <div class="badge-row">
    <span class="badge b-orange">💰 $25M Revenue</span>
    <span class="badge b-blue">📅 2015 – 2017</span>
    <span class="badge b-green">🚲 3 Categories</span>
    <span class="badge b-gold">📦 25,164 Orders</span>
    <span class="badge b-purple">🌍 Multi-Country</span>
    <span class="badge b-orange">📊 Power BI</span>
  </div>
</div>

<div class="divider"><span></span><span></span><span></span></div>

<div class="container">

  <!-- AT A GLANCE -->
  <div class="section">
    <div class="section-title"><div class="icon i-orange">📌</div>At a Glance</div>
    <div class="kpi-grid">
      <div class="kpi-card k-orange"><div class="kpi-value">$25M</div><div class="kpi-label">Total Revenue</div></div>
      <div class="kpi-card k-blue">  <div class="kpi-value">$10.46M</div><div class="kpi-label">Total Profit</div></div>
      <div class="kpi-card k-green"> <div class="kpi-value">$14.46M</div><div class="kpi-label">Total Expense</div></div>
      <div class="kpi-card k-gold">  <div class="kpi-value">84,174</div><div class="kpi-label">Units Sold</div></div>
      <div class="kpi-card k-purple"><div class="kpi-value">25,164</div><div class="kpi-label">Total Orders</div></div>
      <div class="kpi-card k-white"> <div class="kpi-value">2.17%</div><div class="kpi-label">Return Rate</div></div>
    </div>
  </div>

  <!-- PROJECT OVERVIEW -->
  <div class="section">
    <div class="section-title"><div class="icon i-green">🧭</div>Project Overview</div>
    <div class="card">
      <p style="color:rgba(255,255,255,0.7); margin-bottom:14px;">
        This <strong style="color:white">Power BI Sales Dashboard</strong> project analyzes retail sales data
        from <strong style="color:var(--primary)">January 2015</strong> to
        <strong style="color:var(--primary)">June 2017</strong> across three product categories —
        <strong style="color:var(--green-light)">Accessories</strong>,
        <strong style="color:var(--blue-light)">Bikes</strong>, and
        <strong style="color:var(--gold)">Clothing</strong>.
      </p>
      <p style="color:rgba(255,255,255,0.7); margin-bottom:14px;">
        The dashboard provides deep insights into revenue trends, profit margins, country-wise performance,
        weekend vs weekday sales, return rates, and 10-day rolling averages — all built using
        <strong style="color:white">Power BI Desktop</strong> with custom <strong style="color:white">DAX measures</strong>.
      </p>
      <p style="color:rgba(255,255,255,0.55); font-size:13px;">
        🌍 Top Market: <strong style="color:var(--blue-light)">United States (31.86%)</strong> &nbsp;|&nbsp;
        📅 Date Range: <strong style="color:var(--primary-light)">01-Jan-2015 to 30-Jun-2017</strong>
      </p>
    </div>
  </div>

  <!-- PRODUCT CATEGORIES -->
  <div class="section">
    <div class="section-title"><div class="icon i-green">🚲</div>Product Categories</div>
    <div class="cat-grid">
      <div class="cat-card">
        <div class="cat-icon">🔧</div>
        <div class="cat-name" style="color:var(--green-light)">Accessories</div>
        <div class="cat-units" style="color:var(--green-light)">57,809</div>
        <div class="cat-sub">units sold — highest</div>
      </div>
      <div class="cat-card">
        <div class="cat-icon">🚲</div>
        <div class="cat-name" style="color:var(--blue-light)">Bikes</div>
        <div class="cat-units" style="color:var(--blue-light)">13,929</div>
        <div class="cat-sub">units sold</div>
      </div>
      <div class="cat-card">
        <div class="cat-icon">👕</div>
        <div class="cat-name" style="color:var(--gold)">Clothing</div>
        <div class="cat-units" style="color:var(--gold)">12,436</div>
        <div class="cat-sub">units sold</div>
      </div>
    </div>
  </div>

  <!-- DASHBOARD VISUALS -->
  <div class="section">
    <div class="section-title"><div class="icon i-blue">📊</div>Dashboard Visuals — 8 Reports</div>
    <div class="visuals-grid">
      <div class="visual-card"><div class="visual-num">01</div><div class="visual-info"><h4>Final Dashboard</h4><p>Main overview with KPI cards, map, revenue by country donut chart, quantity by day, and all key metrics in one view.</p></div></div>
      <div class="visual-card"><div class="visual-num">02</div><div class="visual-info"><h4>Bar & Column Charts</h4><p>Revenue by Day Name, Quantity by Day, Revenue & Profit by Year, and Weekend Revenue vs Weekday Qty by Category.</p></div></div>
      <div class="visual-card"><div class="visual-num">03</div><div class="visual-info"><h4>Line Chart</h4><p>Total Quantity Sold and Revenue/Profit plotted over time by Year, Quarter, Month, and Day for trend analysis.</p></div></div>
      <div class="visual-card"><div class="visual-num">04</div><div class="visual-info"><h4>Map Visual</h4><p>Total Quantity Sold by Continent and Category shown as pie charts on a world map (North America, Europe, Pacific).</p></div></div>
      <div class="visual-card"><div class="visual-num">05</div><div class="visual-info"><h4>Decomposition Tree</h4><p>Drill-down from Total Quantity Sold → Category → Subcategory → Product Name → Product Cost.</p></div></div>
      <div class="visual-card"><div class="visual-num">06</div><div class="visual-info"><h4>Gauge Chart</h4><p>Revenue vs Target Month Revenue gauge showing $25M actual against $50M target with previous month comparison table.</p></div></div>
      <div class="visual-card"><div class="visual-num">07</div><div class="visual-info"><h4>Matrix Tables</h4><p>Revenue by Product Color, Return Rate by Category, YTD/QTD/MTD Revenue, and Return Rate % by Product Name.</p></div></div>
      <div class="visual-card"><div class="visual-num">08</div><div class="visual-info"><h4>10-Day Rolling Tables</h4><p>Day-level breakdown of 10-Day Rolling Revenue, Profit, and Quantity Sold for 2015 Q1 with running totals.</p></div></div>
    </div>
  </div>

  <!-- KEY ANALYSES -->
  <div class="section">
    <div class="section-title"><div class="icon i-gold">🔍</div>Key Analyses Performed</div>
    <div class="analysis-grid">
      <div class="analysis-card"><h4><span class="dot d-orange"></span>Revenue & Profit Trend</h4><p>Year-over-year revenue grew from $6.4M (2015) → $9.3M (2016) → $9.2M (2017 partial), with profit tracking consistently at ~42%.</p></div>
      <div class="analysis-card"><h4><span class="dot d-blue"></span>Country-wise Performance</h4><p>USA leads at 31.86% revenue share, followed by Australia and United Kingdom. Sales mapped across 6 countries.</p></div>
      <div class="analysis-card"><h4><span class="dot d-green"></span>Weekend vs Weekday Sales</h4><p>Weekend Revenue = $7M vs Weekday Revenue = $18M. Weekend Qty = 24K vs Weekday Qty = 61K units.</p></div>
      <div class="analysis-card"><h4><span class="dot d-gold"></span>10-Day Rolling Average</h4><p>Custom DAX rolling window analysis for Revenue, Profit, and Quantity tracking momentum over any 10-day period.</p></div>
      <div class="analysis-card"><h4><span class="dot d-purple"></span>Return Rate Analysis</h4><p>Overall return rate of 2.17%. Bikes have highest return rate (3.08%) vs Accessories (1.95%) and Clothing (2.16%).</p></div>
      <div class="analysis-card"><h4><span class="dot d-orange"></span>Revenue by Product Color</h4><p>Black color products generate highest revenue at $7.88M, tracked across Bikes, Clothing, and Accessories.</p></div>
    </div>
  </div>

  <!-- KEY FINDINGS -->
  <div class="section">
    <div class="section-title"><div class="icon i-purple">💡</div>Key Findings & Insights</div>
    <ul class="insight-list">
      <li><span class="num">01</span><span>🔧 <strong style="color:white">Accessories</strong> dominate sales volume at 57,809 units (68.7% of total), far ahead of Bikes and Clothing.</span></li>
      <li><span class="num">02</span><span>🌍 <strong style="color:white">United States</strong> is the top revenue market at 31.86%, followed by Australia at ~29.77%.</span></li>
      <li><span class="num">03</span><span>📅 <strong style="color:white">Wednesday</strong> generates the highest daily revenue, while Sunday has the lowest weekday performance.</span></li>
      <li><span class="num">04</span><span>🚲 <strong style="color:white">Bikes</strong> have the highest return rate at 3.08%, signaling potential quality or fit issues to investigate.</span></li>
      <li><span class="num">05</span><span>📈 Revenue and quantity sold <strong style="color:white">grew significantly from mid-2016 into 2017</strong>, showing strong business momentum.</span></li>
      <li><span class="num">06</span><span>🎯 Target Month Revenue is set at <strong style="color:white">105% of previous month</strong>, tracked live via the Gauge Chart visual.</span></li>
      <li><span class="num">07</span><span>⚫ <strong style="color:white">Black color products</strong> generate the most revenue at $7.88M, followed by Red ($4.9M) and Yellow ($4.6M).</span></li>
    </ul>
  </div>

  <!-- DAX MEASURES -->
  <div class="section">
    <div class="section-title"><div class="icon i-gold">🧮</div>Key DAX Measures</div>
    <div class="dax-grid">
      <div class="dax-card">
        <h4>⚡ Revenue & Profit</h4>
        <pre>Total Revenue = SUM(Sales[Revenue])

Total Profit =
  [Total Revenue] - [Total Expense]

Profit Margin % =
  DIVIDE([Total Profit],[Total Revenue],0)</pre>
      </div>
      <div class="dax-card">
        <h4>📅 10-Day Rolling Revenue</h4>
        <pre>10 Days Rolling Revenue =
CALCULATE(
  [Total Revenue],
  DATESINPERIOD(
    'Date'[Date],
    LASTDATE('Date'[Date]),
    -10, DAY
  )
)</pre>
      </div>
      <div class="dax-card">
        <h4>📊 YTD / QTD / MTD</h4>
        <pre>YTD Revenue =
  TOTALYTD([Total Revenue],'Date'[Date])

QTD Revenue =
  TOTALQTD([Total Revenue],'Date'[Date])

MTD Revenue =
  TOTALMTD([Total Revenue],'Date'[Date])</pre>
      </div>
      <div class="dax-card">
        <h4>🔄 Return Rate & Target</h4>
        <pre>Return Rate % =
  DIVIDE([Total Return Qty],
         [Total Qty Sold], 0)

Target Month Revenue =
  [Previous Month Revenue] * 1.05

Previous Month Revenue =
  CALCULATE([Total Revenue],
    PREVIOUSMONTH('Date'[Date]))</pre>
      </div>
      <div class="dax-card">
        <h4>📆 Weekend vs Weekday</h4>
        <pre>Weekend Revenue =
  CALCULATE([Total Revenue],
    'Date'[DayType] = "Weekend")

Weekday Qty Sold =
  CALCULATE([Total Qty Sold],
    'Date'[DayType] = "Weekday")</pre>
      </div>
      <div class="dax-card">
        <h4>🎨 Black Color Revenue</h4>
        <pre>Black Color Revenue =
  CALCULATE(
    [Total Revenue],
    'Product'[ProductColor] = "Black"
  )</pre>
      </div>
    </div>
  </div>

  <!-- TOOLS -->
  <div class="section">
    <div class="section-title"><div class="icon i-blue">🛠️</div>Tools & Technologies</div>
    <div class="tech-row">
      <div class="tech-pill"><span class="dot d-orange"></span> Power BI Desktop</div>
      <div class="tech-pill"><span class="dot d-blue"></span> DAX</div>
      <div class="tech-pill"><span class="dot d-green"></span> Power Query (ETL)</div>
      <div class="tech-pill"><span class="dot d-gold"></span> Microsoft Bing Maps</div>
      <div class="tech-pill"><span class="dot d-purple"></span> Decomposition Tree</div>
      <div class="tech-pill"><span class="dot d-orange"></span> Gauge Chart</div>
      <div class="tech-pill"><span class="dot d-blue"></span> Matrix Visual</div>
      <div class="tech-pill"><span class="dot d-green"></span> Rolling Window Analysis</div>
    </div>
  </div>

  <!-- FILE STRUCTURE -->
  <div class="section">
    <div class="section-title"><div class="icon i-gold">📂</div>File Structure</div>
    <div class="tree">
      <div><span class="folder">📁 Bike-Sales-PowerBI-Dashboard/</span></div>
      <div>&nbsp;&nbsp;├── <span class="file">📊 BikeSales.pbix</span> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;← Power BI file</div>
      <div>&nbsp;&nbsp;├── <span class="folder">📁 images/</span></div>
      <div>&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├── <span class="item">Final_Dashboard.png</span></div>
      <div>&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├── <span class="item">Bar_Column_Chart.png</span></div>
      <div>&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├── <span class="item">Line_Chart.png</span></div>
      <div>&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├── <span class="item">Map_Visual.png</span></div>
      <div>&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├── <span class="item">Decomposition_Tree.png</span></div>
      <div>&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├── <span class="item">Gauge_Chart.png</span></div>
      <div>&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;├── <span class="item">Matrix.png</span></div>
      <div>&nbsp;&nbsp;│&nbsp;&nbsp;&nbsp;└── <span class="item">10Days_Rolling_Revenue.png</span></div>
      <div>&nbsp;&nbsp;└── <span class="file">📄 README.html</span></div>
    </div>
  </div>

</div>

<div class="divider"><span></span><span></span><span></span></div>

<div class="footer">
  <p style="margin-bottom:8px;">🚲 &nbsp; Bike Sales Analytics Dashboard &nbsp;•&nbsp; Power BI Project</p>
  <p>Built with ❤️ using Power BI Desktop & DAX &nbsp;|&nbsp; Sales data covering 2015–2017 across 6 countries</p>
</div>

</body>
</html>
