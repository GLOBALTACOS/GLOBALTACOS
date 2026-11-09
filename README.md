      document.getElementById('fxRateVal').innerText = `1 USD = ${currentUsdJpyRate.toFixed(2)} JPY`;
updateView();
if (currentSelectedCountry) showDetail(currentSelectedCountry);

async function fetchFxRate() {
  const statusEl = document.getElementById('apiStatus');
  const t = i18n[currentLang];
  statusEl.innerText = t.fetching;
  statusEl.style.background = '#f59e0b';

  try {
    const res = await fetch('https://open.er-api.com/v6/latest/USD');
    const data = await res.json();
    if (data && data.rates && data.rates.JPY) {
      currentUsdJpyRate = data.rates.JPY;
      document.getElementById('fxRateVal').innerText = `1 USD = ${currentUsdJpyRate.toFixed(2)} JPY`;
      statusEl.innerText = 'オンライン';
      statusEl.style.background = '#10b981';
    } else {
      throw new Error('無効なレート データ');
    }
  } catch (err) {
    console.warn('API取得失敗。固定値を使用します:', err);
    document.getElementById('fxRateVal').innerText = `1 USD = ${currentUsdJpyRate.toFixed(2)} JPY ${t.fixed}`;
    statusEl.innerText = 'オフライン';
    statusEl.style.background = '#ef4444';
  }
  updateView();
  if (currentSelectedCountry) showDetail(currentSelectedCountry);
}

function updateView() {
  const filter = document.getElementById('filterSelect').value;
  markers.forEach(m => map.removeLayer(m));
  markers = [];

  const filtered = countries.filter(c => {
    if (filter === 'over') return c.priceUsd > basePriceUsd;
    if (filter === 'under') return c.priceUsd < basePriceUsd;
    return true;
  });

  filtered.forEach(c => {
    let cls = 'pin-base';
    if (c.priceUsd > basePriceUsd) cls = 'pin-over';
    if (c.priceUsd < basePriceUsd) cls = 'pin-under';

    const icon = L.divIcon({
      className: '',
      html: `<div class="custom-pin ${cls}"></div>`,
      iconSize: [12, 12]
    });

    const m = L.marker([c.lat, c.lng], { icon: icon }).addTo(map);
    m.on('click', () => showDetail(c));
    markers.push(m);
  });

  renderRanking(filtered);
}

function showDetail(c) {
  currentSelectedCountry = c;
  const t = i18n[currentLang];
  const priceJpy = Math.round(c.priceUsd * currentUsdJpyRate);
  const budgetUsd = 1000;
  const tacosBuyable = Math.floor(budgetUsd / c.priceUsd);
  const pppRatio = ((c.priceUsd / basePriceUsd) * 100).toFixed(0);
  const countryName = c.name[currentLang] || c.name.ja;
  const countryNote = c.note[currentLang] || c.note.ja;

  document.getElementById('detailBox').innerHTML = `
    <div class="card-title">
      ${countryName} ${c.priceUsd > basePriceUsd ? t.tagOver : (c.priceUsd === basePriceUsd ? t.tagBase : t.tagUnder)}
    </div>
    <div class="data-row"><span>${t.priceUsd}</span><b>$${c.priceUsd.toFixed(2)}</b></div>
    <div class="data-row"><span>${t.priceJpy}</span><b style="color:#f59e0b;">約 ${priceJpy.toLocaleString()} 円</b></div>
    <div class="data-row"><span>${t.pppRatio}</span><b>${pppRatio}%</b></div>
    <div class="game-box">
      <div style="font-size:0.75rem; color:#cbd5e1;">${t.tripMsg}</div>
      <div class="taco-count">🌮 ${tacosBuyable.toLocaleString()} ${t.buyableMsg}</div>
      <div style="font-size:0.7rem; color:#94a3b8; margin-top:2px;">
        ${tacosBuyable > 400 ? t.highPurchasing : t.lowPurchasing}
      </div>
    </div>
    <div style="font-size: 0.8rem; color: #94a3b8; margin-top: 8px; border-top: 1px dashed #334155; padding-top: 6px;">
      ${t.noteTitle}<br>${countryNote}
    </div>
  `;
  map.panTo([c.lat, c.lng]);
}

function renderRanking(list) {
  const sorted = [...list].sort((a, b) => b.priceUsd - a.priceUsd);
  const rankingEl = document.getElementById('rankingList');
  rankingEl.innerHTML = '';

  sorted.forEach((c, idx) => {
    const priceJpy = Math.round(c.priceUsd * currentUsdJpyRate);
    const li = document.createElement('li');
    const countryName = c.name[currentLang] || c.name.ja;
    li.className = 'ranking-item';
    li.onclick = () => showDetail(c);
    li.innerHTML = `
      <span><b>${idx + 1}.</b> ${countryName}</span>
      <span><b>$${c.priceUsd.toFixed(2)}</b> (${priceJpy.toLocaleString()}円)</span>
    `;
    rankingEl.appendChiｍ
