# crypto-market-
Market analysis 
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Crypto Pulse</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Sans:wght@400;500;600&family=Fraunces:opsz,wght@9..144,600&display=swap" rel="stylesheet">
<style>
:root{--bg:#eef2f6;--card:#fff;--ink:#14213d;--muted:#5d6b82;--line:#d9e0ea;--up:#0f8a5f;--down:#c8372d;--flat:#8a6d1d;--upbg:#e3f4ec;--downbg:#fbe8e6;--flatbg:#f6efd9}
@media (prefers-color-scheme:dark){:root{--bg:#0f1624;--card:#18223a;--ink:#e8edf6;--muted:#9aa8c0;--line:#2a3652;--up:#43c795;--down:#ff7a70;--flat:#e0c36a;--upbg:#123a2e;--downbg:#47211f;--flatbg:#3c3516}}
*{box-sizing:border-box}
html,body{margin:0}
body{background:var(--bg);color:var(--ink);font:400 15px/1.5 "IBM Plex Sans",system-ui,sans-serif;padding:20px 16px 40px}
.wrap{max-width:1080px;margin:0 auto}
header{display:flex;justify-content:space-between;align-items:center;gap:12px;margin-bottom:18px}
h1{font:600 26px "Fraunces",Georgia,serif;margin:0}
button{font:inherit;background:var(--ink);color:var(--bg);border:0;border-radius:8px;padding:8px 14px;cursor:pointer}
button:focus-visible{outline:3px solid var(--up);outline-offset:2px}
.card{background:var(--card);border:1px solid var(--line);border-radius:12px;padding:18px}
.verdict{display:flex;flex-wrap:wrap;gap:24px;align-items:center;margin-bottom:18px}
.verdict .main{flex:1 1 320px}
.big{font:600 44px/1.1 "Fraunces",Georgia,serif;margin:2px 0 12px}
.gauge{position:relative;height:12px;border-radius:6px;background:linear-gradient(90deg,var(--down),var(--flat),var(--up));margin:10px 0 6px}
.mark{position:absolute;top:-5px;width:6px;height:22px;border-radius:3px;background:var(--ink);border:2px solid var(--card);transform:translateX(-50%);transition:left .6s}
.scale{display:flex;justify-content:space-between;color:var(--muted);font-size:13px}
.reasons{flex:1 1 280px;margin:0;padding-left:18px;color:var(--muted)}
.reasons b{color:var(--ink);font-weight:500}
.grid{display:grid;grid-template-columns:3fr 2fr;gap:18px}
@media(max-width:820px){.grid{grid-template-columns:1fr}}
h2{font:600 17px "IBM Plex Sans",sans-serif;margin:0 0 10px}
.scroll{overflow-x:auto}
table{width:100%;border-collapse:collapse;min-width:520px}
th{text-align:right;font-weight:500;color:var(--muted);font-size:13px;padding:6px 8px;border-bottom:1px solid var(--line)}
th:first-child,td:first-child{text-align:left}
td{padding:9px 8px;border-bottom:1px solid var(--line);text-align:right;white-space:nowrap}
.coin{display:flex;align-items:center;gap:8px;font-weight:500}
.coin img{width:22px;height:22px;border-radius:50%}
.coin small{color:var(--muted);font-weight:400}
.up{color:var(--up)}.down{color:var(--down)}
.badge{display:inline-block;padding:2px 10px;border-radius:999px;font-size:13px;font-weight:500}
.b-up{background:var(--upbg);color:var(--up)}.b-down{background:var(--downbg);color:var(--down)}.b-flat{background:var(--flatbg);color:var(--flat)}
svg.spark{width:90px;height:28px;vertical-align:middle}
.news{list-style:none;margin:0;padding:0}
.news li{padding:10px 0;border-bottom:1px solid var(--line)}
.news a{color:var(--ink);text-decoration:none;font-weight:500}
.news a:hover{text-decoration:underline}
.meta{display:flex;gap:8px;align-items:center;color:var(--muted);font-size:13px;margin-top:3px}
.msg{color:var(--muted);padding:12px 0}
.err{color:var(--down)}
.lhead{display:flex;justify-content:space-between;align-items:center;gap:12px;flex-wrap:wrap;margin-bottom:10px}
.lhead h2{margin:0}
select{font:inherit;background:var(--card);color:var(--ink);border:1px solid var(--line);border-radius:8px;padding:6px 10px}
select:focus-visible{outline:3px solid var(--up);outline-offset:2px}
#chart{width:100%;min-width:640px;height:auto;display:block}
.lists{display:grid;grid-template-columns:1fr 1fr;gap:18px;margin-top:14px}
@media(max-width:820px){.lists{grid-template-columns:1fr}}
.lists h3{font:600 15px "IBM Plex Sans",sans-serif;margin:0 0 6px}
.lists ul{list-style:none;margin:0;padding:0}
.lists li{padding:7px 0;border-bottom:1px solid var(--line)}
footer{color:var(--muted);font-size:13px;margin-top:18px}
</style>
</head>
<body>
<div class="wrap">
  <header>
    <h1>Crypto Pulse</h1>
    <div><span id="updated" class="meta" style="display:inline"></span> <button id="refresh">Refresh</button></div>
  </header>

  <div id="banner" class="card err" style="display:none;margin-bottom:18px" role="alert"></div>

  <section class="card verdict" aria-live="polite">
    <div class="main">
      <div class="meta">Market signal right now</div>
      <div class="big" id="verdict">Loading…</div>
      <div class="gauge"><div class="mark" id="mark" style="left:50%"></div></div>
      <div class="scale"><span>Bearish</span><span>Neutral</span><span>Bullish</span></div>
    </div>
    <ul class="reasons" id="reasons"></ul>
  </section>

  <div class="grid">
    <section class="card">
      <h2>Top coins</h2>
      <div class="scroll"><table>
        <thead><tr><th>Coin</th><th>Price</th><th>24h</th><th>7d</th><th>Last 7 days</th><th>Signal</th></tr></thead>
        <tbody id="coins"><tr><td colspan="6" class="msg">Loading prices…</td></tr></tbody>
      </table></div>
    </section>
    <section class="card">
      <h2>Latest news</h2>
      <ul class="news" id="news"><li class="msg">Loading news…</li></ul>
    </section>
  </div>

  <section class="card" style="margin-top:18px">
    <div class="lhead">
      <h2>Order blocks &amp; limit orders</h2>
      <div><select id="sym" aria-label="Coin"></select> <select id="tf" aria-label="Timeframe"><option value="15m">15m</option><option value="1h" selected>1h</option><option value="4h">4h</option><option value="1d">1d</option></select></div>
    </div>
    <div class="scroll"><svg id="chart" viewBox="0 0 900 340" role="img" aria-label="Candlestick chart with order blocks and limit order walls"></svg></div>
    <div class="lists">
      <div><h3>Buy zones below price</h3><ul id="buys"></ul></div>
      <div><h3>Sell zones above price</h3><ul id="sells"></ul></div>
    </div>
    <p class="meta" id="lnote" style="display:block"></p>
    <p class="meta" style="display:block">Shaded boxes are <b>order blocks</b>: the last opposite candle before a strong move, estimated from past candles, only shown if price hasn’t broken through them yet. Dashed lines are <b>limit order walls</b>: large resting buy and sell orders in the live Binance order book. Walls can be cancelled at any time.</p>
  </section>

  <footer>Data: CoinGecko, Binance public market data, alternative.me Fear &amp; Greed Index, CoinDesk and Cointelegraph feeds. The signal combines recent price trend, news tone and market mood. It is a rough estimate, not financial advice.</footer>
</div>

<script>
const $ = id => document.getElementById(id);
const POS = new Set("surge surges surged rally rallies soar soars jump jumps gain gains bull bullish record high highs adopt adoption approve approval approved etf inflow inflows growth rise rises rising breakout recover recovery partnership launch upgrade boost optimism milestone".split(" "));
const NEG = new Set("crash crashes plunge plunges drop drops fall falls slump bear bearish hack hacked exploit ban bans lawsuit sue fraud outflow outflows selloff fear loss losses decline declines liquidation liquidations warn warns scam probe reject rejects dump tumble tumbles slide slides".split(" "));

function sentiment(text){
  let s = 0;
  for (const w of text.toLowerCase().replace(/[^a-z\s-]/g, " ").split(/\s+/)){
    if (POS.has(w)) s++; else if (NEG.has(w)) s--;
  }
  return s;
}
const clamp = (v, a, b) => Math.max(a, Math.min(b, v));
function label(score){ return score > 20 ? "Bullish" : score < -20 ? "Bearish" : "Neutral"; }
function cls(score){ return score > 20 ? "up" : score < -20 ? "down" : "flat"; }

async function getJSON(url){
  const ctl = new AbortController();
  const t = setTimeout(() => ctl.abort(), 12000);
  try {
    const r = await fetch(url, { signal: ctl.signal });
    if (!r.ok) throw new Error(r.status);
    return await r.json();
  } finally { clearTimeout(t); }
}

const usd = n => new Intl.NumberFormat("en-US", { style: "currency", currency: "USD", maximumFractionDigits: n < 1 ? 4 : 2 }).format(n);
const pct = n => (n >= 0 ? "+" : "") + n.toFixed(1) + "%";

function spark(prices){
  const min = Math.min(...prices), max = Math.max(...prices), w = 90, h = 28;
  const pts = prices.filter((_, i) => i % 4 === 0).map((p, i, a) =>
    (i / (a.length - 1) * w).toFixed(1) + "," + (h - 2 - (p - min) / (max - min || 1) * (h - 4)).toFixed(1)).join(" ");
  const up = prices[prices.length - 1] >= prices[0];
  return `<svg class="spark" viewBox="0 0 ${w} ${h}" aria-hidden="true"><polyline fill="none" stroke="${up ? "var(--up)" : "var(--down)"}" stroke-width="1.8" points="${pts}"/></svg>`;
}

const NAMES = { BTC: "Bitcoin", ETH: "Ethereum", BNB: "BNB", SOL: "Solana", XRP: "XRP", DOGE: "Dogecoin", ADA: "Cardano", TRX: "TRON", AVAX: "Avalanche", LINK: "Chainlink" };
async function fetchCoins(){
  try {
    const r = await getJSON("https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=10&page=1&sparkline=true&price_change_percentage=24h,7d");
    if (r.length) return { coins: r, src: "CoinGecko" };
  } catch (e) { /* fall back to Binance */ }
  const coins = await Promise.all(Object.keys(NAMES).map(async s => {
    const k = await getJSON(`https://data-api.binance.vision/api/v3/klines?symbol=${s}USDT&interval=1h&limit=169`);
    const cl = k.map(x => +x[4]), last = cl[cl.length - 1];
    return { name: NAMES[s], symbol: s.toLowerCase(), image: "", current_price: last,
      price_change_percentage_24h: (last / cl[cl.length - 25] - 1) * 100,
      price_change_percentage_7d_in_currency: (last / cl[0] - 1) * 100,
      sparkline_in_7d: { price: cl } };
  }));
  return { coins, src: "Binance" };
}

async function loadNews(){
  const feeds = ["https://www.coindesk.com/arc/outboundfeeds/rss/", "https://cointelegraph.com/rss"];
  const res = await Promise.allSettled(feeds.map(f =>
    getJSON("https://api.rss2json.com/v1/api.json?rss_url=" + encodeURIComponent(f))));
  let items = [];
  res.forEach((r, i) => {
    if (r.status !== "fulfilled" || !r.value.items) return;
    const src = i === 0 ? "CoinDesk" : "Cointelegraph";
    r.value.items.slice(0, 12).forEach(it => items.push({
      title: it.title, link: it.link, src,
      time: new Date(it.pubDate.replace(" ", "T") + "Z"),
      score: sentiment(it.title)
    }));
  });
  items.sort((a, b) => b.time - a.time);
  if (!items.length) throw new Error("no news");
  return items.slice(0, 14);
}

function renderNews(items){
  const ul = $("news"); ul.innerHTML = "";
  for (const it of items){
    const li = document.createElement("li");
    const a = document.createElement("a");
    a.href = it.link; a.target = "_blank"; a.rel = "noopener"; a.textContent = it.title;
    const meta = document.createElement("div"); meta.className = "meta";
    const tone = it.score > 0 ? ["Positive", "b-up"] : it.score < 0 ? ["Negative", "b-down"] : ["Neutral", "b-flat"];
    const b = document.createElement("span"); b.className = "badge " + tone[1]; b.textContent = tone[0];
    const s = document.createElement("span");
    s.textContent = it.src + " · " + (isNaN(it.time) ? "" : it.time.toLocaleString([], { month: "short", day: "numeric", hour: "2-digit", minute: "2-digit" }));
    meta.append(b, s); li.append(a, meta); ul.append(li);
  }
}

function trendScore(c){
  const d7 = c.price_change_percentage_7d_in_currency || 0, d1 = c.price_change_percentage_24h || 0;
  return clamp(d7 / 15, -1, 1) * 50 + clamp(d1 / 6, -1, 1) * 20;
}

function renderCoins(coins, extra){
  const body = $("coins"); body.innerHTML = "";
  for (const c of coins){
    const sc = trendScore(c) + extra;
    const d1 = c.price_change_percentage_24h || 0, d7 = c.price_change_percentage_7d_in_currency || 0;
    const tr = document.createElement("tr");
    tr.innerHTML = `<td><span class="coin">${c.image ? `<img alt="" src="${c.image}">` : ""}<span></span></span></td>
      <td>${usd(c.current_price)}</td>
      <td class="${d1 >= 0 ? "up" : "down"}">${pct(d1)}</td>
      <td class="${d7 >= 0 ? "up" : "down"}">${pct(d7)}</td>
      <td>${c.sparkline_in_7d ? spark(c.sparkline_in_7d.price) : ""}</td>
      <td><span class="badge b-${cls(sc)}">${label(sc)}</span></td>`;
    tr.querySelector(".coin span").textContent = c.name;
    const sm = document.createElement("small"); sm.textContent = c.symbol.toUpperCase();
    tr.querySelector(".coin").append(sm);
    body.append(tr);
  }
}

function renderVerdict(coins, news, fng){
  const avgTrend = coins.reduce((s, c) => s + trendScore(c), 0) / coins.length;
  const net = news.reduce((s, n) => s + Math.sign(n.score), 0);
  const newsScore = news.length ? clamp(net / news.length, -1, 1) * 20 : 0;
  const moodScore = fng != null ? (fng - 50) / 50 * 10 : 0;
  const total = clamp(avgTrend + newsScore + moodScore, -100, 100);
  const v = $("verdict");
  v.textContent = label(total); v.className = "big " + (cls(total) === "flat" ? "" : cls(total));
  $("mark").style.left = (50 + total / 2) + "%";
  const pos = news.filter(n => n.score > 0).length, neg = news.filter(n => n.score < 0).length;
  $("reasons").innerHTML =
    `<li><b>Price trend:</b> top coins are ${avgTrend > 5 ? "mostly rising" : avgTrend < -5 ? "mostly falling" : "moving sideways"} over the last 7 days.</li>
     <li><b>News tone:</b> ${pos} positive and ${neg} negative among the latest ${news.length} headlines.</li>
     <li><b>Market mood:</b> ${fng != null ? "Fear &amp; Greed Index is " + fng + " out of 100." : "Fear &amp; Greed Index is unavailable."}</li>`;
  return newsScore + moodScore;
}

async function load(){
  $("refresh").disabled = true;
  const [coinsR, newsR, fngR] = await Promise.allSettled([
    fetchCoins(),
    loadNews(),
    getJSON("https://api.alternative.me/fng/?limit=1")
  ]);
  const news = newsR.status === "fulfilled" ? newsR.value : [];
  const fng = fngR.status === "fulfilled" ? Number(fngR.value.data[0].value) : null;

  if (news.length) renderNews(news);
  else $("news").innerHTML = '<li class="msg err">Couldn’t load news. Check your internet and press Refresh.</li>';

  $("banner").style.display = "none";
  if (coinsR.status === "fulfilled" && coinsR.value.coins.length){
    const extra = renderVerdict(coinsR.value.coins, news, fng);
    renderCoins(coinsR.value.coins, extra * 0.5);
    $("updated").textContent = "Updated " + new Date().toLocaleTimeString([], { hour: "2-digit", minute: "2-digit" }) + " · Prices: " + coinsR.value.src;
  } else {
    const b = $("banner");
    b.style.display = "block";
    b.textContent = "No live data reached this page. Download the file and open it in Chrome or Safari (not inside the Claude app), turn off VPN or ad-blockers, then press Refresh. Error: " + (coinsR.reason && coinsR.reason.message ? coinsR.reason.message : "network blocked");
    $("coins").innerHTML = '<tr><td colspan="6" class="msg err">Couldn’t load prices. CoinGecko may be limiting requests. Wait a minute and press Refresh.</td></tr>';
    $("verdict").textContent = "No data";
  }
  $("refresh").disabled = false;
}
/* ---------- Order blocks & limit order walls ---------- */
const SYMS = ["BTC","ETH","BNB","SOL","XRP","DOGE","ADA","TRX","AVAX","LINK"];
const fmtP = n => n >= 1000 ? n.toLocaleString("en-US", { maximumFractionDigits: 0 }) : n >= 1 ? n.toFixed(2) : n.toFixed(4);
const fmtUsd = n => "$" + new Intl.NumberFormat("en-US", { notation: "compact", maximumFractionDigits: 1 }).format(n);

function findOBs(c){
  const atr = c.slice(-50).reduce((s, x) => s + (x.h - x.l), 0) / Math.min(50, c.length);
  const price = c[c.length - 1].c, out = [];
  for (let i = 1; i < c.length - 4; i++){
    const x = c[i], nx = c[i + 1], fut = c.slice(i + 1, i + 4), later = c.slice(i + 4);
    if (x.c < x.o && nx.c > nx.o && Math.max(...fut.map(f => f.c)) > x.h + 1.2 * atr
        && !later.some(f => f.c < x.l) && x.l < price)
      out.push({ type: "buy", i, hi: x.h, lo: x.l });
    if (x.c > x.o && nx.c < nx.o && Math.min(...fut.map(f => f.c)) < x.l - 1.2 * atr
        && !later.some(f => f.c > x.h) && x.h > price)
      out.push({ type: "sell", i, hi: x.h, lo: x.l });
  }
  const near = t => out.filter(o => o.type === t)
    .sort((a, b) => Math.abs((a.hi + a.lo) / 2 - price) - Math.abs((b.hi + b.lo) / 2 - price)).slice(0, 3);
  return [...near("buy"), ...near("sell")];
}

function findWalls(d, price){
  const step = price * 0.0025;
  const bucket = rows => {
    const m = new Map();
    for (const [p, q] of rows){
      const k = Math.floor(+p / step) * step;
      m.set(k, (m.get(k) || 0) + +p * +q);
    }
    return [...m].map(([p, usd]) => ({ p: p + step / 2, usd })).sort((a, b) => b.usd - a.usd).slice(0, 3);
  };
  return { buy: bucket(d.bids), sell: bucket(d.asks) };
}

function drawLevels(c, obs, w){
  const s = Math.max(0, c.length - 90), v = c.slice(s), price = c[c.length - 1].c;
  const W = 900, H = 340, P = 14, R = 96, cw = (W - R) / v.length;
  let lo = Math.min(...v.map(x => x.l)), hi = Math.max(...v.map(x => x.h));
  const pad = (hi - lo) * 0.04; lo -= pad; hi += pad;
  const y = p => P + (hi - p) / (hi - lo) * (H - 2 * P);
  let g = "";
  for (const o of obs){
    if (o.lo > hi || o.hi < lo) continue;
    const a = Math.max(y(o.hi), P), b = Math.min(y(o.lo), H - P), x0 = Math.max(0, o.i - s) * cw;
    const col = o.type === "buy" ? "var(--up)" : "var(--down)";
    g += `<rect x="${x0}" y="${a}" width="${W - R - x0}" height="${Math.max(b - a, 2)}" fill="${col}" opacity=".2"/>
          <text x="${W - R - 4}" y="${a + 11}" text-anchor="end" font-size="11" fill="${col}">${o.type === "buy" ? "Buy" : "Sell"} order block</text>`;
  }
  for (const t of ["buy", "sell"]) for (const k of w[t]){
    if (k.p < lo || k.p > hi) continue;
    const col = t === "buy" ? "var(--up)" : "var(--down)";
    g += `<line x1="0" x2="${W - R}" y1="${y(k.p)}" y2="${y(k.p)}" stroke="${col}" stroke-width="1.6" stroke-dasharray="6 4"/>
          <text x="${W - R + 4}" y="${y(k.p) + 4}" font-size="11" fill="${col}">${fmtUsd(k.usd)} ${t === "buy" ? "buy" : "sell"}</text>`;
  }
  v.forEach((x, i) => {
    const cx = i * cw + cw / 2, col = x.c >= x.o ? "var(--up)" : "var(--down)";
    g += `<line x1="${cx}" x2="${cx}" y1="${y(x.h)}" y2="${y(x.l)}" stroke="${col}"/>
          <rect x="${cx - cw * 0.3}" y="${y(Math.max(x.o, x.c))}" width="${cw * 0.6}" height="${Math.max(1, Math.abs(y(x.o) - y(x.c)))}" fill="${col}"/>`;
  });
  g += `<line x1="0" x2="${W - R}" y1="${y(price)}" y2="${y(price)}" stroke="var(--muted)" stroke-width="1"/>
        <text x="${W - R + 4}" y="${y(price) + 4}" font-size="11" fill="var(--ink)" font-weight="600">${fmtP(price)}</text>`;
  $("chart").innerHTML = g;

  const fill = (id, type, empty) => {
    const ul = $(id); ul.innerHTML = "";
    const rows = [
      ...obs.filter(o => o.type === type).map(o => ({ mid: (o.hi + o.lo) / 2, text: `Order block ${fmtP(o.lo)} to ${fmtP(o.hi)}` })),
      ...w[type].map(k => ({ mid: k.p, text: `Limit orders near ${fmtP(k.p)}: ${fmtUsd(k.usd)} waiting` }))
    ].sort((a, b) => Math.abs(a.mid - price) - Math.abs(b.mid - price));
    if (!rows.length){ ul.innerHTML = `<li class="msg">${empty}</li>`; return; }
    for (const r of rows){
      const li = document.createElement("li");
      li.textContent = `${r.text} (${pct((r.mid - price) / price * 100)} from price)`;
      ul.append(li);
    }
  };
  fill("buys", "buy", "No untouched buy order block found on this timeframe.");
  fill("sells", "sell", "No untouched sell order block found on this timeframe.");
  $("lnote").textContent = "Showing " + $("sym").value + "/USDT, " + $("tf").value + " candles, last " + v.length + " candles.";
}

async function loadLevels(){
  const sym = $("