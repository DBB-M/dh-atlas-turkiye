---
title: Kişiler
layout: cloud
permalink: /subjects.html
cloud-fields: site.data.theme.subjects-fields
---

<style>
.kisiler-tabs { display: flex; gap: 0; margin-bottom: 1.5rem; border-bottom: 2px solid #e0e8f0; }
.kisiler-tab {
  padding: 0.65rem 1.4rem;
  font-size: 0.88rem;
  font-weight: 600;
  color: #666;
  cursor: pointer;
  border-bottom: 3px solid transparent;
  margin-bottom: -2px;
  transition: all 0.15s;
  background: none;
  border-top: none;
  border-left: none;
  border-right: none;
}
.kisiler-tab:hover { color: #1B4F72; }
.kisiler-tab.active { color: #1B4F72; border-bottom-color: #2E86C1; }
.kisiler-panel { display: none; }
.kisiler-panel.active { display: block; }
</style>

<div class="kisiler-tabs">
  <button class="kisiler-tab active" onclick="switchTab('bulut', this)">☁️ Kişi Bulutu</button>
  <button class="kisiler-tab" onclick="switchTab('liste', this)">👥 Araştırmacı Listesi</button>
</div>

<!-- BULUT PANELİ -->
<div id="panel-bulut" class="kisiler-panel active">
  <p style="color:#666; font-size:0.9rem; margin-bottom:1rem;">Kelime boyutu sıklığa göre belirlenir. İsimlere tıklayarak ilgili çalışmalara ulaşabilirsiniz.</p>
</div>

<!-- LİSTE PANELİ -->
<div id="panel-liste" class="kisiler-panel">

<style>
.ar-wrap { max-width: 1100px; margin: 0 auto; padding: 0 0 2rem; }
.ar-header { display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 1rem; margin-bottom: 1.2rem; }
.ar-count { font-size: 0.82rem; color: #888; font-style: italic; }
.ar-search-bar { display: flex; gap: 0.75rem; margin-bottom: 1.5rem; flex-wrap: wrap; }
.ar-search-bar input { flex: 1; min-width: 220px; padding: 0.55rem 0.9rem; border: 1px solid #c5d5e8; border-radius: 8px; font-size: 0.9rem; font-family: inherit; }
.ar-search-bar select { padding: 0.55rem 0.75rem; border: 1px solid #c5d5e8; border-radius: 8px; font-size: 0.88rem; font-family: inherit; background: #fff; }
.ar-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 1rem; }
.ar-card { background: #fff; border-radius: 10px; box-shadow: 0 2px 10px rgba(0,0,0,0.07); overflow: hidden; transition: transform 0.18s, box-shadow 0.18s; }
.ar-card:hover { transform: translateY(-3px); box-shadow: 0 6px 18px rgba(27,79,114,0.13); }
.ar-card-head { background: linear-gradient(135deg, #1B4F72, #2E86C1); padding: 1rem 1.1rem 0.85rem; }
.ar-card-name { font-size: 0.95rem; font-weight: 700; color: #fff; margin: 0; line-height: 1.3; }
.ar-card-body { padding: 0.85rem 1.1rem; }
.ar-badge { display: inline-block; font-size: 0.68rem; font-weight: 700; padding: 0.18rem 0.55rem; border-radius: 10px; margin: 2px; }
.ar-badge-alan { background: #EBF5FB; color: #1B4F72; }
.ar-badge-work { background: #E9F7EF; color: #1E8449; }
.ar-works { margin-top: 0.75rem; padding-top: 0.75rem; border-top: 1px solid #f0f4f8; }
.ar-work-item { font-size: 0.78rem; color: #555; padding: 0.25rem 0; border-bottom: 1px solid #f5f8fb; line-height: 1.4; }
.ar-work-item:last-child { border-bottom: none; }
.ar-work-fmt { font-size: 0.65rem; font-weight: 700; text-transform: uppercase; letter-spacing: 0.05em; margin-right: 4px; }
.ar-link { display: inline-block; margin-top: 0.6rem; font-size: 0.75rem; color: #2E86C1; font-weight: 600; text-decoration: none; }
.ar-link:hover { color: #1B4F72; }
.ar-empty { text-align: center; padding: 3rem; color: #aaa; font-style: italic; grid-column: 1/-1; }
.ar-show-all { text-align: center; margin-top: 1.5rem; }
.ar-show-all button { background: #EBF5FB; color: #1B4F72; border: 1px solid #AED6F1; border-radius: 8px; padding: 0.6rem 1.5rem; font-size: 0.88rem; font-weight: 600; cursor: pointer; }
.ar-show-all button:hover { background: #AED6F1; }
@media (max-width: 600px) { .ar-grid { grid-template-columns: 1fr; } }
</style>

<div class="ar-wrap">
  <div class="ar-header">
    <span class="ar-count" id="ar-count">Yükleniyor...</span>
  </div>
  <div class="ar-search-bar">
    <input type="text" id="ar-search" placeholder="İsim ara..." oninput="filterPeople()">
    <select id="ar-alan" onchange="filterPeople()">
      <option value="">Tüm Disiplinler</option>
    </select>
    <select id="ar-min-work" onchange="filterPeople()">
      <option value="1">Tüm araştırmacılar</option>
      <option value="2">2+ çalışma</option>
      <option value="5">5+ çalışma</option>
      <option value="10">10+ çalışma</option>
    </select>
  </div>
  <div class="ar-grid" id="ar-grid"><p class="ar-empty">Veriler yükleniyor...</p></div>
  <div class="ar-show-all" id="ar-more" style="display:none;">
    <button onclick="showAllPeople()">Tümünü Göster</button>
  </div>
</div>
</div>

<script>
// Sekme geçişi — bulut divini doğru panele taşı
function switchTab(tab, btn) {
  document.querySelectorAll('.kisiler-tab').forEach(function(t){ t.classList.remove('active'); });
  document.querySelectorAll('.kisiler-panel').forEach(function(p){ p.classList.remove('active'); });
  btn.classList.add('active');
  document.getElementById('panel-' + tab).classList.add('active');

  // Bulut div'ini ilgili panele taşı (CB cloud-js dışarıda render ediyor)
  if (tab === 'bulut') {
    var cloudDiv = document.querySelector('[id^="cloud-div-"]');
    if (cloudDiv && !document.getElementById('panel-bulut').contains(cloudDiv)) {
      document.getElementById('panel-bulut').appendChild(cloudDiv);
    }
  }
}

// Sayfa yüklenince bulut divini bulut paneline taşı
document.addEventListener('DOMContentLoaded', function() {
  setTimeout(function() {
    var cloudDiv = document.querySelector('[id^="cloud-div-"]');
    if (cloudDiv) document.getElementById('panel-bulut').appendChild(cloudDiv);
  }, 300);
});

// Araştırmacı listesi
var PEOPLE = [];
var arFiltered = [];
var arShowLimit = 60;
var FMT_COLORS = {'makale':'#1B4F72','proje':'#1E8449','tez':'#6C3483','sunum':'#B7950B','bildiri':'#B7950B','kitap':'#922B21','rapor':'#117A65','çalıştay':'#6E2F8A','sempozyum':'#6E2F8A'};

function fmtColor(f) {
  if (!f) return '#566573';
  f = f.toLowerCase();
  for (var k in FMT_COLORS) { if (f.includes(k)) return FMT_COLORS[k]; }
  return '#566573';
}

fetch('{{ "/assets/data/people_data.json" | relative_url }}')
  .then(function(r){ return r.json(); })
  .then(function(data){
    PEOPLE = data; arFiltered = PEOPLE;
    var alans = [...new Set(PEOPLE.flatMap(function(p){ return p.alanlar; }))].sort();
    var sel = document.getElementById('ar-alan');
    alans.forEach(function(a){ var o=document.createElement('option'); o.value=a; o.textContent=a; sel.appendChild(o); });
    renderArGrid();
  })
  .catch(function(){ document.getElementById('ar-grid').innerHTML='<p class="ar-empty">Veri yüklenemedi.</p>'; });

function filterPeople() {
  var q = document.getElementById('ar-search').value.toLowerCase().trim();
  var alan = document.getElementById('ar-alan').value;
  var min = parseInt(document.getElementById('ar-min-work').value);
  arShowLimit = 60;
  arFiltered = PEOPLE.filter(function(p){
    return (!q||p.name.toLowerCase().includes(q)) && (!alan||p.alanlar.includes(alan)) && p.work_count>=min;
  });
  renderArGrid();
}

function showAllPeople() { arShowLimit = arFiltered.length; renderArGrid(); }

function toggleMore(uid) {
  var el = document.getElementById('more-'+uid);
  var btn = el.nextSibling;
  if (el.style.display==='none') {
    el.style.display='block';
    btn.textContent = btn.textContent.replace('▾','▴').replace('daha','gizle');
  } else {
    el.style.display='none';
    btn.textContent = btn.textContent.replace('▴','▾').replace('gizle','daha');
  }
}

function renderArGrid() {
  var grid = document.getElementById('ar-grid');
  var shown = arFiltered.slice(0, arShowLimit);
  document.getElementById('ar-count').textContent = arFiltered.length + ' araştırmacı';
  document.getElementById('ar-more').style.display = arFiltered.length > arShowLimit ? 'block' : 'none';
  if (!shown.length) { grid.innerHTML='<p class="ar-empty">Araştırmacı bulunamadı.</p>'; return; }

  grid.innerHTML = shown.map(function(p){
    var badges = p.alanlar.slice(0,3).map(function(a){ return '<span class="ar-badge ar-badge-alan">'+a+'</span>'; }).join('');
    var wbadge = '<span class="ar-badge ar-badge-work">'+p.work_count+' çalışma</span>';
    var allWorks = p.works.map(function(w){
      var url='/dh-atlas-turkiye/items/'+w.id+'.html';
      var d=(w.date&&w.date!='nan')?' <span style="color:#aaa;">('+w.date+')</span>':'';
      return '<div class="ar-work-item"><span class="ar-work-fmt" style="color:'+fmtColor(w.format)+'">'+w.format+'</span><a href="'+url+'" style="color:#444;text-decoration:none;">'+w.title+'</a>'+d+'</div>';
    });
    var works = allWorks.slice(0,3).join('');
    var hidden = allWorks.slice(3).join('');
    var uid = p.name.replace(/\s+/g,'-').replace(/[^a-zA-Z0-9-]/g,'');
    var more = p.work_count>3 ? '<div id="more-'+uid+'" style="display:none;">'+hidden+'</div><div class="ar-work-item" style="color:#2E86C1;font-weight:600;cursor:pointer;" onclick="toggleMore(\''+uid+'\')">+'+(p.work_count-3)+' çalışma daha ▾</div>' : '';
    var link = p.yy_link ? '<a href="'+p.yy_link+'" target="_blank" class="ar-link">🔗 Akademik Profil</a>' : '';
    return '<div class="ar-card"><div class="ar-card-head"><p class="ar-card-name">'+p.name+'</p></div><div class="ar-card-body">'+badges+' '+wbadge+'<div class="ar-works">'+works+more+'</div>'+link+'</div></div>';
  }).join('');
}
</script>
