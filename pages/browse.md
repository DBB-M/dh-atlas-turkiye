---
title: Keşfet
layout: page
permalink: /browse.html
---

<style>
/* ═══════════════════════════════════════
   KEŞFET — Özel Görünüm
   CollectionBuilder'ın grid'ini gizleyip
   kendi grid'imizi ekliyoruz
═══════════════════════════════════════ */

/* CB'nin varsayılan browse widget'ını gizle */
#browse-nav, #browse-pagination, #cbObjects { display: none !important; }

/* ── Değişkenler ── */
:root {
  --ink: #1a1612;
  --parchment: #f5f0e8;
  --cream: #faf7f2;
  --rust: #8b3a2a;
  --gold: #c9a84c;
  --gold-light: #e8d5a3;
  --muted: #6b5e52;
  --border: #d4c9b8;
}

/* ── Wrapper ── */
#kesfet-wrapper {
  font-family: 'Crimson Pro', 'Georgia', serif;
  color: var(--ink);
  background: var(--cream);
  margin: -1rem -15px 0;
  padding: 0;
}

/* ── Toolbar (sticky) ── */
#kesfet-toolbar {
  position: sticky;
  top: 56px;
  z-index: 100;
  background: var(--ink);
  border-bottom: 2px solid var(--gold);
  padding: 10px 20px;
  display: flex;
  align-items: center;
  gap: 12px;
  flex-wrap: wrap;
}

#kesfet-search {
  flex: 1;
  min-width: 180px;
  max-width: 280px;
  background: rgba(255,255,255,0.1);
  border: 1px solid var(--gold);
  border-radius: 4px;
  color: #fff;
  padding: 6px 12px;
  font-family: inherit;
  font-size: 0.9rem;
}
#kesfet-search::placeholder { color: rgba(255,255,255,0.5); }
#kesfet-search:focus { outline: none; background: rgba(255,255,255,0.18); }

/* ── Sekme Butonları ── */
#kesfet-tabs {
  display: flex;
  gap: 6px;
  flex-wrap: wrap;
}
.ktab {
  background: transparent;
  border: 1px solid rgba(201,168,76,0.4);
  color: rgba(255,255,255,0.75);
  border-radius: 3px;
  padding: 5px 13px;
  font-family: inherit;
  font-size: 0.85rem;
  cursor: pointer;
  transition: all .2s;
}
.ktab:hover { background: rgba(201,168,76,0.2); color: #fff; }
.ktab.active {
  background: var(--gold);
  border-color: var(--gold);
  color: var(--ink);
  font-weight: 600;
}

/* ── Sıralama ── */
#kesfet-sort {
  background: rgba(255,255,255,0.1);
  border: 1px solid var(--gold);
  border-radius: 4px;
  color: #fff;
  padding: 5px 10px;
  font-family: inherit;
  font-size: 0.85rem;
  cursor: pointer;
  margin-left: auto;
}
#kesfet-sort option { background: #2a2018; color: #fff; }

/* ── Sonuç sayısı ── */
#kesfet-count {
  color: var(--gold-light);
  font-size: 0.8rem;
  white-space: nowrap;
}

/* ── Layout: filtre + grid ── */
#kesfet-body {
  display: flex;
  gap: 0;
  min-height: 60vh;
}

/* ── Filtre Paneli ── */
#kesfet-filters {
  width: 220px;
  flex-shrink: 0;
  background: #fff;
  border-right: 1px solid var(--border);
  padding: 20px 16px;
}
#kesfet-filters h6 {
  font-family: 'Georgia', serif;
  font-size: 0.7rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--muted);
  margin: 0 0 8px;
  padding-bottom: 4px;
  border-bottom: 1px solid var(--border);
}
#kesfet-filters h6:not(:first-child) { margin-top: 20px; }

.kfilter-label {
  display: flex;
  align-items: center;
  gap: 7px;
  font-size: 0.88rem;
  color: var(--ink);
  cursor: pointer;
  padding: 3px 0;
  transition: color .15s;
}
.kfilter-label:hover { color: var(--rust); }
.kfilter-label input[type=checkbox] { accent-color: var(--rust); width: 14px; height: 14px; }
.kfilter-count {
  margin-left: auto;
  font-size: 0.75rem;
  color: var(--muted);
  background: var(--parchment);
  border-radius: 10px;
  padding: 1px 6px;
}

/* ── İçerik Alanı ── */
#kesfet-content {
  flex: 1;
  padding: 24px 20px;
  overflow: hidden;
}

/* Bölüm başlıkları (filtre yokken) */
.ksection-title {
  font-family: 'Georgia', serif;
  font-size: 1.15rem;
  color: var(--rust);
  border-bottom: 1px solid var(--gold-light);
  padding-bottom: 6px;
  margin: 28px 0 16px;
}
.ksection-title:first-child { margin-top: 0; }

/* Grid */
.kesfet-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(175px, 1fr));
  gap: 14px;
  margin-bottom: 8px;
}

/* Kart */
.kcard {
  background: #fff;
  border: 1px solid var(--border);
  border-radius: 5px;
  overflow: hidden;
  transition: transform .2s, box-shadow .2s;
  cursor: pointer;
  text-decoration: none;
  color: inherit;
  display: block;
}
.kcard:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 18px rgba(0,0,0,0.1);
  border-color: var(--gold);
  text-decoration: none;
  color: inherit;
}
.kcard-img {
  width: 100%;
  aspect-ratio: 1;
  object-fit: cover;
  background: var(--parchment);
  display: block;
}
/* Görseli olan kartlar kare, olmayanlar metin kartı */
.kcard-text {
  padding: 14px 12px 10px;
  display: flex;
  flex-direction: column;
  min-height: 120px;
}
.kcard-body {
  padding: 8px 10px;
}
.kcard-badge {
  display: inline-block;
  font-size: 0.68rem;
  padding: 1px 6px;
  border-radius: 3px;
  margin-bottom: 4px;
  font-weight: 600;
  letter-spacing: 0.03em;
}
.badge-goruntu { background: #e8f0e8; color: #3a6b3a; }
.badge-dokuman { background: #e8e8f5; color: #3a3a8b; }
.badge-video   { background: #f5e8e8; color: #8b3a3a; }
.badge-ses     { background: #f5f0e0; color: #7a6a20; }
.badge-diger   { background: #ebebeb; color: #555; }

.kcard-title {
  font-size: 0.82rem;
  line-height: 1.35;
  color: var(--ink);
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.kcard-meta {
  font-size: 0.72rem;
  color: var(--muted);
  margin-top: 4px;
}

/* Boş durum */
#kesfet-empty {
  display: none;
  text-align: center;
  padding: 60px 20px;
  color: var(--muted);
}
#kesfet-empty .empty-icon { font-size: 3rem; margin-bottom: 12px; }

/* Responsive */
@media (max-width: 768px) {
  #kesfet-filters { display: none; }
  #kesfet-toolbar { top: 0; }
  .kesfet-grid { grid-template-columns: repeat(auto-fill, minmax(140px, 1fr)); }
}
</style>

<!-- KEŞFET WRAPPER -->
<div id="kesfet-wrapper">

  <!-- Toolbar -->
  <div id="kesfet-toolbar">
    <input id="kesfet-search" type="text" placeholder="🔍  Başlık, konu, yer ara…" autocomplete="off">
    <div id="kesfet-tabs">
      <button class="ktab active" data-top="Tümü">Tümü</button>
      <button class="ktab" data-top="Akademik">📚 Akademik</button>
      <button class="ktab" data-top="Görsel Arşiv">🖼 Görsel Arşiv</button>
      <button class="ktab" data-top="Biyografik">👤 Biyografik</button>
    </div>
    <select id="kesfet-sort">
      <option value="default">Varsayılan sıra</option>
      <option value="title">Başlığa göre</option>
      <option value="date_asc">Tarihe göre ↑</option>
      <option value="date_desc">Tarihe göre ↓</option>
    </select>
    <span id="kesfet-count"></span>
  </div>

  <!-- Body -->
  <div id="kesfet-body">

    <!-- Filtre Paneli -->
    <div id="kesfet-filters">
      <h6>Tür</h6>
      <div id="filter-type"></div>
      <h6>Alt Kategori</h6>
      <div id="filter-sub"></div>
      <h6>Dönem</h6>
      <div id="filter-period"></div>
    </div>

    <!-- İçerik -->
    <div id="kesfet-content">
      <div id="kesfet-empty">
        <div class="empty-icon">🔍</div>
        <p>Sonuç bulunamadı.</p>
      </div>
    </div>

  </div>
</div>

<script>
(function(){

// ── 1. Kategori haritası (CSV'den üretildi) ──
const CAT = {"436":{"t":"Biyografik","s":"Aile Arşivi","y":"","f":"annesiyle.jpeg"},"437":{"t":"Biyografik","s":"Aile Arşivi","y":"","f":"ailesiyle.jpeg"},"438":{"t":"Biyografik","s":"Aile Arşivi","y":"","f":"aile.jpeg"},"435":{"t":"Biyografik","s":"Aile Arşivi","y":"","f":"yeğeniyle.jpeg"},"75":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"malikanesistemi.pdf"},"90":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"56":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"cipolla.pdf"},"82":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"mali.pdf"},"84":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"85":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"86":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"12":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"gumruk.pdf"},"41":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"yorum.pdf"},"71":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"ahi.jpg"},"42":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"feasibility.pdf"},"65":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"kalkinma.pdf"},"80":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"entreprises.pdf"},"23":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"review.pdf"},"32":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"pamuk.pdf"},"34":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"tokat.pdf"},"31":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"ilke.pdf"},"68":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"milletlerarasi.pdf"},"29":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"sanayi.pdf"},"109":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"40":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"industry.pdf"},"110":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"13":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"esham.pdf"},"27":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"guerre.pdf"},"39":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"ahlak.pdf"},"76":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"bildiri.jpg"},"87":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"62":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"fetih.pdf"},"63":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"fetihkapanis.pdf"},"66":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"neden.pdf"},"67":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"degerlendirme.pdf"},"78":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"ticaret.pdf"},"14":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"osmanli.pdf"},"340":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"solak.jpg"},"15":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"iltizam.pdf"},"48":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"reforms.pdf"},"50":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"devlet.pdf"},"443":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"Erol Özvar Mehmet Genç Belgeden Modele Bir Por.pdf"},"38":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"commerce.pdf"},"81":{"t":"Diğer","s":"Genel","y":"","f":"muzakere.pdf"},"332":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"turkishstudies.pdf"},"16":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"malikane.pdf"},"17":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"malikanedivani.pdf"},"28":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"talid.pdf"},"331":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"literatur.pdf"},"47":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"gezinti.pdf"},"172":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"18":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"nazir.pdf"},"19":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"mukataa.pdf"},"46":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"dört.pdf"},"49":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"mukataakavrami.pdf"},"53":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"butcelerbir.pdf"},"54":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"butceleriki.pdf"},"20":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"osmanlilar.pdf"},"103":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"43":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"sosyoloji.pdf"},"77":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"dilencilik.pdf"},"22":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"encyclopaedia.pdf"},"73":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"gungor.pdf"},"79":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"bildiri.jpg"},"444":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"mTteUJy8nDI","f":""},"445":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"UCMGfR3qGNc","f":""},"45":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"kültürler.jpg"},"44":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"deli.pdf"},"70":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"deniz.pdf"},"74":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"bildiri.jpg"},"216":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"esnaf.pdf"},"417":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"üçusta.jpg"},"30":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"saray.pdf"},"94":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"167":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"r2HG1PkAvm4","f":"konferans.jpg"},"382":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sehirdogu.jpg"},"383":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sehirdogu2.jpg"},"388":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sehirdogu7.jpg"},"21":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"yedivahid.pdf"},"55":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"ceviri.pdf"},"72":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"itri.pdf"},"95":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"177":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"212":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"röportaj.jpg"},"219":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"söyleşi.jpg"},"257":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"P-5ZYyauYWc","f":""},"333":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"dortsima.jpg"},"334":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"dortsima.jpg"},"335":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"dortsima.jpg"},"336":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"dortsima.jpg"},"378":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul11.jpg"},"379":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul12.jpg"},"380":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul13.jpg"},"381":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"odtu.jpg"},"384":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sehirdogu3.jpg"},"385":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sehirdogu4.jpg"},"386":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sehirdogu5.jpg"},"387":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sehirdogu6.jpg"},"389":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sehirdogu8.jpg"},"390":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"BIZ1PrZwqpk","f":""},"24":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"modern.pdf"},"25":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"vakif.pdf"},"60":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"cevre.pdf"},"221":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"söyleşi.jpg"},"268":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"anadolu2.jpg"},"269":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"tuba2015.jpg"},"270":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"tubaodul.jpg"},"279":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"yedikıta.jpg"},"330":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"kucukali.pdf"},"59":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"urbanism.jpg"},"273":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"kristallale.jpg"},"307":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"zeyrek.jpg"},"308":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"zeyrek1.jpg"},"309":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"zeyrek2.jpg"},"310":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"zeyrek3.jpg"},"311":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"zeyrek4.jpg"},"313":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"sehir16.jpg"},"64":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"zekat.pdf"},"224":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"7FePAARZ-Fc","f":"söyleşi.jpg"},"171":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"fzMn9O6jIKs","f":"konferans.jpg"},"226":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"söyleşi.jpg"},"298":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"mezuniyet.jpg"},"301":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"ders2018.jpg"},"302":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"paleografi2018.jpg"},"264":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"kadem.png"},"265":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"kadem2.png"},"267":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"anadolu.jpg"},"296":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"istanbuldersi.jpeg"},"299":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"nimet.jpg"},"300":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"ders19.jpg"},"303":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"iftar.jpg"},"338":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"karpat.jpeg"},"282":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"twitter2.jpg"},"283":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"twitter3.jpg"},"284":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"twitter4.jpg"},"285":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"twitter5.jpg"},"286":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"twitter6.jpg"},"51":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"konusmalar.pdf"},"227":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"söyleşi.jpg"},"328":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"bilig.pdf"},"337":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"mustafaozel.jpg"},"349":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"dergah.pdf"},"392":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"evangeliabaltavefeyat.pdf"},"393":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"şevketpamukvefeyat.pdf"},"394":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"seyfikenanvefeyat.pdf"},"396":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"kenanyıldızvefayat.pdf"},"397":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"beşirayvazoğlubiyografidenemesi.pdf"},"434":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"abdulkadirbuluşmetodoloji.pdf"},"439":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"HacYolunda_Ayvazoglu_Kitap.jpg"},"442":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"OSMANLI SEMPOZYUMU CALISMA_DGT.pdf"},"400":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"sosyologca.pdf"},"433":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":""},"404":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"abdullahtok.pdf"},"391":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"oktayözel1.jpg"},"440":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"AhmetCihan.jpg"},"89":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"128":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"33":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"calisma.pdf"},"162":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"161":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"100":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"35":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"savas.pdf"},"69":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"arsiv.pdf"},"101":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"106":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"208":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"196":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"197":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"207":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"205":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"203":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"124":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"107":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"149":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"155":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"178":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"151":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"173":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"108":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"125":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"211":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"röportaj.jpg"},"147":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"180":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"137":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"88":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"148":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"189":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"190":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"191":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"192":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"193":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"194":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"61":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"bildiri.jpg"},"150":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"127":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"102":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"179":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"145":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"37":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"baskent.pdf"},"174":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"111":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"156":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"97":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"129":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"26":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"iktisadi.pdf"},"153":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"142":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"123":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"114":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"122":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"112":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"140":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"251":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"GuJk16SCoPc","f":""},"91":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"92":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"141":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"126":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"104":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"98":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"202":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"187":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"201":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"113":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"136":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"198":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"372":{"t":"Diğer","s":"Genel","y":"","f":"disiplinlerarasi.pdf"},"105":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"135":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"154":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"188":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"195":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"99":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"139":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"157":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"152":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"146":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"181":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"287":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"leiden.jpg"},"288":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"leiden2.jpg"},"289":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"leiden3.jpg"},"290":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"leiden4.jpg"},"291":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"leiden5.jpg"},"293":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"leiden7.jpg"},"294":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"leiden8.jpg"},"295":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"leiden9.jpg"},"292":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"leiden6.jpg"},"83":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"selim.jpg"},"158":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"144":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"138":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"275":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"artvin.jpg"},"276":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"artvin2.jpg"},"277":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"artvin3.jpg"},"278":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"artvin4.jpg"},"143":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"96":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"185":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"186":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"170":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"199":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"200":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"118":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"261":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"dogu.jpg"},"119":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"120":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"166":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"169":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"121":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"160":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"115":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"217":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"scUnRAaAPOM","f":"söyleşi.jpg"},"159":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"241":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"eSrUHkBafws","f":""},"116":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"117":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"233":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"excH4TWsmHI","f":""},"244":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"8r0QMqYB4VQ","f":""},"414":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"qJAVlOZBhvQ","f":""},"210":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"röportaj.jpg"},"318":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"yenisafak.jpg"},"134":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"130":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"163":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"183":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"133":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"220":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"söyleşi.jpg"},"374":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"odessa.jpg"},"375":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"odessa2.jpg"},"376":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"odessa3.jpg"},"377":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"odessa4.jpg"},"206":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"184":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"182":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"131":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"132":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"164":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"218":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"söyleşi.jpg"},"165":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"213":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"röportaj.jpg"},"204":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"konferans.jpg"},"322":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"yalova.jpg"},"209":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"tecrube.pdf"},"426":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"wNSWlYVmnVE","f":""},"427":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"Cvo8DZCwFk","f":""},"428":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"3m2caV7C9ak","f":""},"176":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"osark.jpg"},"254":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"S19KEz_QRBk","f":""},"339":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"ozan.jpg"},"371":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"hurriyet.pdf"},"4":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"gercekhayat.pdf"},"243":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"j-s8FTJ5h_k","f":""},"242":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"YAwDZCG69v8","f":""},"249":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"WaUAF9KQyso","f":""},"412":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"WaUAF9KQyso","f":""},"415":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"XnukGN2JSQs","f":""},"245":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"aKO07ont-aQ","f":""},"223":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"aKO07ont-aQ","f":"söyleşi.jpg"},"250":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"-xAhzwbnJFA","f":"SarayKonferanslari.jpg"},"271":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"derintarih.jpg"},"236":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"mRhrcZkYpUQ","f":""},"246":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"7FePAARZ-Fc","f":""},"343":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"okcular.jpg"},"344":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"okcular2.jpg"},"222":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"7C3CR7Arvyg","f":"söyleşi.jpg"},"247":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"7C3CR7Arvyg","f":""},"252":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"DSbpmL8L6NQ","f":""},"234":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"tT_HIk4h9aA","f":""},"306":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"gercekhayat.jpg"},"235":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"8_zxDAH2mqM","f":""},"272":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"erolgungor.jpg"},"256":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"99eID5HSTbE","f":""},"346":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"fzMn9O6jIKs","f":""},"248":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"NqzR7sJTLZY","f":""},"424":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"BDTaCYya2UM","f":""},"430":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"4q2EM7aMaWA","f":""},"229":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"7YjxO9Tz0-E","f":"söyleşi.jpg"},"232":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"7YjxO9Tz0-E","f":""},"348":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"lMSPLFoV4fU","f":""},"214":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"0cah5mQjkmY","f":""},"231":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"0cah5mQjkmY","f":""},"225":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"cbTGHlmOQyM","f":"söyleşi.jpg"},"422":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"bFJaukfHRrU","f":""},"175":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"duHXusjLT4w","f":"konferans.jpg"},"253":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"duHXusjLT4w","f":""},"314":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"sakarya.jpg"},"315":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"sakarya1.jpg"},"316":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"sakarya2.jpg"},"411":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"korkut.pdf"},"423":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"Wgxl5IzLOic","f":""},"317":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"samblog.jpg"},"429":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"kHcgmXqhooQ","f":""},"324":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"isam.jpg"},"325":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"isam2.jpg"},"326":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"isam3.jpg"},"230":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"söyleşi.jpg"},"255":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"YGAoBDc9qmI","f":""},"274":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"marmara.jpg"},"354":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"iyc.jpg"},"355":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"fazlıoglu.jpg"},"356":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"derin.jpg"},"228":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"söyleşi.jpg"},"280":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"dc-RXpDduQk","f":""},"319":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"dunyabizim3.jpg"},"320":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"dunyabizim4.jpg"},"329":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"trtworld.pdf"},"341":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"yalcın.jpg"},"342":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"enesoglu.jpg"},"352":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"aktay.jpg"},"353":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"aktay2.jpg"},"357":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"turkocaklari.jpg"},"358":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"goksu.jpg"},"369":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"erolgoka.pdf"},"413":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"OnDWbUneQBk","f":""},"6":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"msak.pdf"},"8":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"ulkuyaz.pdf"},"351":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"","f":"armagan.jpg"},"370":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"serbestiyet.pdf"},"419":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"mgencanı.pdf"},"347":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"G7tmXRpCASk","f":""},"373":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"karar.pdf"},"9":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"yenisafak.pdf"},"327":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"dailysabah.pdf"},"2":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"MGenc_Aktar_ToplumsalTarih.pdf"},"3":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"diken.pdf"},"5":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"kriter.pdf"},"304":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"lacivert.pdf"},"1":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"birikim.pdf"},"350":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"altintas.jpg"},"260":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"OnDWbUneQBk","f":""},"262":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"dunyabizim.png"},"263":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"dunyabizim2.png"},"7":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"star.pdf"},"11":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"ihtifal.jpeg"},"305":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"ulesam.pdf"},"321":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"eGjmJTF7_r4","f":""},"368":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"bisav.pdf"},"399":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"cumalibozpınar.pdf"},"395":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"coşkunçakırvefayat.pdf"},"407":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":""},"398":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"tayfunulaş.pdf"},"418":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"niçinazyazdı.pdf"},"441":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"Mgenc_Sempozyum_Gungoren_Marmara.jpg"},"403":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"birâliminhayat.pdf"},"416":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"xEyN3SG9bEA","f":""},"410":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"yeşilyurt.pdf"},"447":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"kabri.jpg"},"406":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"osamer.pdf"},"408":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"kadim.pdf"},"431":{"t":"Diğer","s":"Genel","y":"","f":""},"421":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"gencvegoethe.pdf"},"425":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"mgencanısınasempozyum.jpg"},"402":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"sempozyum.pdf"},"401":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"nasyonelsosyalizm.pdf"},"409":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"telakki.pdf"},"446":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"ahmetfarukyilmaz.jpg"},"420":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":""},"405":{"t":"Akademik","s":"Yazılı Eserler","y":"","f":"yahyaayyıldız.pdf"},"432":{"t":"Diğer","s":"Genel","y":"","f":"sarıklıgenchoca.pdf"},"448":{"t":"Diğer","s":"Genel","y":"","f":"ZKurum_MGenc_Parfum.pdf"},"359":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"sakul.jpg"},"360":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul2.jpg"},"361":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul3.jpg"},"362":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul4.jpg"},"363":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul5.jpg"},"364":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul6.jpg"},"365":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul7.jpg"},"366":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul8.jpg"},"367":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"sakul9.jpg"},"10":{"t":"Biyografik","s":"Vefeyat ve Anma","y":"","f":"kitapdergisi.pdf"},"93":{"t":"Akademik","s":"Konferans ve Bildiriler","y":"","f":"seminer.jpg"},"215":{"t":"Akademik","s":"Röportaj ve Söyleşiler","y":"","f":"islamekonomisi.pdf"},"266":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"academia.jpg"},"281":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"twitter.jpg"},"297":{"t":"Biyografik","s":"Hayat Hikayesi","y":"","f":"kenanyildiz.jpg"},"323":{"t":"Görsel Arşiv","s":"Video Kayıtları","y":"wStjfRjByXI","f":""},"345":{"t":"Görsel Arşiv","s":"Fotoğraflar","y":"","f":"arifbilgin.jpg"},"449":{"t":"Diğer","s":"Genel","y":"","f":"Tarih_HalitOzkan.jpg"},"450":{"t":"Diğer","s":"Genel","y":"","f":"cin_mgenc_hkose1.jpeg"},"451":{"t":"Diğer","s":"Genel","y":"","f":"cin_mgenc_hkose2.jpeg"},"452":{"t":"Diğer","s":"Genel","y":"","f":"tez_seherboz.pdf"},"453":{"t":"Diğer","s":"Genel","y":"","f":"tez_pinarerdogan.pdf"},"454":{"t":"Diğer","s":"Genel","y":"","f":"web_muhammetnegis.jpg"}};

// ── 2. Sabit ayarlar ──
const BASE = 'https://hacyolundabirkarinca.github.io/mgenc';
const IMG_BASE = BASE + '/assets/img/derivatives/square/';
const ITEM_BASE = BASE + '/items/';

const TYPE_ICON = {
  'Görüntü':'🖼', 'Döküman':'📄', 'Doküman':'📄',
  'Video':'🎬', 'Ses':'🎵'
};
const TYPE_BADGE = {
  'Görüntü':'badge-goruntu','Döküman':'badge-dokuman','Doküman':'badge-dokuman',
  'Video':'badge-video','Ses':'badge-ses'
};

// Dönem etiketleri
function getPeriod(date){
  if(!date) return 'Bilinmiyor';
  const y = parseInt(date);
  if(isNaN(y)) return 'Bilinmiyor';
  if(y < 1970) return '1970 öncesi';
  if(y < 1980) return '1970\'ler';
  if(y < 1990) return '1980\'ler';
  if(y < 2000) return '1990\'lar';
  if(y < 2010) return '2000\'ler';
  if(y < 2020) return '2010\'lar';
  return '2020 sonrası';
}

// ── 3. Durum ──
let allItems = [];
let activeTop = 'Tümü';
let activeTypes = new Set();
let activeSubs = new Set();
let activePeriods = new Set();
let searchQ = '';
let sortMode = 'default';

// ── 4. Veriyi CollectionBuilder'dan çek ──
fetch(BASE + '/assets/data/metadata.json')
  .then(r => r.json())
  .then(data => {
    const objects = data.objects || data;
    allItems = objects.map((obj, i) => {
      // objectid'yi reference_url'den çıkar (id değeri == catmap key)
      let oid = '';
      if(obj.reference_url){
        const m = obj.reference_url.match(/id=(\d+)/);
        if(m) oid = m[1];
      }
      const cat = CAT[oid] || null;
      return {
        title: obj.title || '',
        date: obj.date || '',
        type: obj.type || '',
        subject: obj.subject || '',
        location: obj.location || '',
        url: obj.reference_url || '',
        top: cat ? cat.t : 'Diğer',
        sub: cat ? cat.s : 'Genel',
        youtubeid: cat ? cat.y : '',
        filename: cat ? cat.f : '',
        period: getPeriod(obj.date),
        _idx: i,
      };
    });
    console.log('Yüklenen kayıt:', allItems.length);
    buildFilters();
    render();
    // URL hash'i yakala — subjects/locations sayfasından yönlendirme
    (function(){
      var rawHash = window.location.hash;
      if(rawHash && rawHash.length > 1){
        var term = decodeURIComponent(rawHash.substring(1)).trim();
        if(term){
          var inp = document.getElementById('kesfet-search');
          inp.value = term;
          searchQ = term;
          render();
          inp.scrollIntoView({behavior:'smooth', block:'center'});
        }
      }
    // Hash değişince de ara
window.addEventListener('hashchange', function(){
  var term = decodeURIComponent(window.location.hash.substring(1)).trim();
  if(term){
    var inp = document.getElementById('kesfet-search');
    inp.value = term;
    searchQ = term;
    render();
  }
});
  })
  .catch(e => {
    document.getElementById('kesfet-content').innerHTML =
      '<p style="padding:40px;color:#888">Veriler yüklenirken hata oluştu.</p>';
    console.error(e);
  });

// ── 5. Filtre panelini oluştur ──
function buildFilters(){
  buildFilterGroup('filter-type', getFreq(allItems, 'type'), activeTypes);
  buildFilterGroup('filter-sub', getFreq(allItems, 'sub'), activeSubs);
  buildFilterGroup('filter-period', getFreq(getPeriodItems(allItems), 'period'), activePeriods);
}

function getPeriodItems(items){
  return items.map(it => ({period: it.period}));
}

function getFreq(items, key){
  const freq = {};
  items.forEach(it => {
    const v = it[key] || 'Bilinmiyor';
    freq[v] = (freq[v]||0) + 1;
  });
  return Object.entries(freq).sort((a,b) => b[1]-a[1]);
}

function buildFilterGroup(elId, entries, activeSet){
  const el = document.getElementById(elId);
  el.innerHTML = '';
  entries.forEach(([val, cnt]) => {
    const label = document.createElement('label');
    label.className = 'kfilter-label';
    label.innerHTML = `<input type="checkbox" value="${val}">
      <span>${val}</span>
      <span class="kfilter-count">${cnt}</span>`;
    label.querySelector('input').addEventListener('change', function(){
      if(this.checked) activeSet.add(val);
      else activeSet.delete(val);
      render();
    });
    el.appendChild(label);
  });
}

// ── 6. Filtreleme ──
function getFiltered(){
  let items = allItems;

  // Sekme
  if(activeTop !== 'Tümü') items = items.filter(it => it.top === activeTop);

  // Checkbox filtreleri
  if(activeTypes.size) items = items.filter(it => activeTypes.has(it.type));
  if(activeSubs.size)  items = items.filter(it => activeSubs.has(it.sub));
  if(activePeriods.size) items = items.filter(it => activePeriods.has(it.period));

  // Arama
  if(searchQ){
    const q = searchQ.toLowerCase();
    items = items.filter(it =>
      it.title.toLowerCase().includes(q) ||
      it.subject.toLowerCase().includes(q) ||
      it.location.toLowerCase().includes(q)
    );
  }

  // Sıralama
  if(sortMode === 'title') items = [...items].sort((a,b) => a.title.localeCompare(b.title,'tr'));
  else if(sortMode === 'date_asc') items = [...items].sort((a,b) => (parseInt(a.date)||0)-(parseInt(b.date)||0));
  else if(sortMode === 'date_desc') items = [...items].sort((a,b) => (parseInt(b.date)||0)-(parseInt(a.date)||0));

  return items;
}

// ── 7. Render ──
function render(){
  const filtered = getFiltered();
  const content = document.getElementById('kesfet-content');
  const empty = document.getElementById('kesfet-empty');
  document.getElementById('kesfet-count').textContent = filtered.length + ' kayıt';

  if(!filtered.length){
    empty.style.display = 'block';
    // grid'leri temizle
    content.querySelectorAll('.kesfet-grid, .ksection-title').forEach(e => e.remove());
    return;
  }
  empty.style.display = 'none';

  // Filtre veya arama aktifse → düz grid
  const hasFilter = activeTop !== 'Tümü' || activeTypes.size || activeSubs.size || activePeriods.size || searchQ;

  content.querySelectorAll('.kesfet-grid, .ksection-title').forEach(e => e.remove());

  if(hasFilter){
    const grid = makeGrid(filtered);
    content.appendChild(grid);
  } else {
    // Alt kategorilere göre grupla
    const groups = {};
    filtered.forEach(it => {
      const key = it.sub || 'Genel';
      if(!groups[key]) groups[key] = [];
      groups[key].push(it);
    });
    // Sıralama: top sırasına göre
    const subOrder = [
      'Konferans ve Bildiriler','Yazılı Eserler','Röportaj ve Söyleşiler',
      'Fotoğraflar','Video Kayıtları',
      'Aile Arşivi','Hayat Hikayesi','Vefeyat ve Anma',
      'Genel'
    ];
    const sortedKeys = Object.keys(groups).sort((a,b) => {
      const ai = subOrder.indexOf(a); const bi = subOrder.indexOf(b);
      if(ai===-1 && bi===-1) return a.localeCompare(b,'tr');
      if(ai===-1) return 1; if(bi===-1) return -1;
      return ai-bi;
    });
    sortedKeys.forEach(sub => {
      const h = document.createElement('div');
      h.className = 'ksection-title';
      h.textContent = sub + ' (' + groups[sub].length + ')';
      content.appendChild(h);
      content.appendChild(makeGrid(groups[sub]));
    });
  }

  // Filtre sayaçlarını güncelle
  updateFilterCounts(filtered);
}

function makeGrid(items){
  const grid = document.createElement('div');
  grid.className = 'kesfet-grid';
  items.forEach(it => grid.appendChild(makeCard(it)));
  return grid;
}

function makeCard(it){
  const a = document.createElement('a');
  a.className = 'kcard';
  a.href = it.url || '#';
  a.title = it.title;

  // Badge
  const badgeCls = TYPE_BADGE[it.type] || 'badge-diger';
  const badgeLabel = it.type || 'Diğer';

  if(it.youtubeid){
    // YouTube → thumbnail göster
    a.innerHTML = `
      <img class="kcard-img" src="https://img.youtube.com/vi/${it.youtubeid}/mqdefault.jpg"
        alt="${it.title}" loading="lazy"
        onerror="this.remove()">
      <div class="kcard-body">
        <span class="kcard-badge ${badgeCls}">${badgeLabel}</span>
        <div class="kcard-title">${it.title}</div>
        <div class="kcard-meta">${it.date || ''}${it.location ? ' · ' + it.location.split(',')[0] : ''}</div>
      </div>`;
  } else if(it.filename){
    // Dosya → thumbnail dene, hata varsa sade metin kart
    const sq = it.filename.replace(/\.[^.]+$/, '') + '_sm.jpg';
    a.innerHTML = `
      <img class="kcard-img" src="${IMG_BASE}${sq}"
        alt="${it.title}" loading="lazy"
        onerror="this.remove()">
      <div class="kcard-body">
        <span class="kcard-badge ${badgeCls}">${badgeLabel}</span>
        <div class="kcard-title">${it.title}</div>
        <div class="kcard-meta">${it.date || ''}${it.location ? ' · ' + it.location.split(',')[0] : ''}</div>
      </div>`;
  } else {
    // Görsel yok → sade metin kart, resim alanı hiç yok
    a.innerHTML = `
      <div class="kcard-text">
        <span class="kcard-badge ${badgeCls}">${badgeLabel}</span>
        <div class="kcard-title" style="-webkit-line-clamp:5">${it.title}</div>
        <div class="kcard-meta" style="margin-top:auto;padding-top:8px">${it.date || ''}${it.location ? ' · ' + it.location.split(',')[0] : ''}</div>
      </div>`;
  }
  return a;
}

function updateFilterCounts(filtered){
  // Tip sayaçlarını güncelle (opsiyonel - basit versiyon)
}

// ── 8. Event listeners ──
document.querySelectorAll('.ktab').forEach(btn => {
  btn.addEventListener('click', function(){
    document.querySelectorAll('.ktab').forEach(b => b.classList.remove('active'));
    this.classList.add('active');
    activeTop = this.dataset.top;
    render();
  });
});

document.getElementById('kesfet-search').addEventListener('input', function(){
  searchQ = this.value.trim();
  render();
});

document.getElementById('kesfet-sort').addEventListener('change', function(){
  sortMode = this.value;
  render();
});


})();

// Hash'ten arama — subjects/locations sayfasından yönlendirme
// IIFE dışında çalışır, allItems global değil ama searchQ global
// metadata.json yüklenince render() zaten çağrılıyor, hash sonradan uygulanır
function applyHashToSearch(){
  var rawHash = window.location.hash;
  if(!rawHash || rawHash.length <= 1) return;
  var term = decodeURIComponent(rawHash.substring(1)).trim();
  if(!term) return;
  var inp = document.getElementById('kesfet-search');
  if(!inp) return;
  inp.value = term;
  // searchQ ve render global scope'dan erişilemez (IIFE içinde)
  // Bu yüzden input event'i tetikle — browse.md'deki listener yakalar
  inp.dispatchEvent(new Event('input'));
}

// Sayfa yüklenince: metadata hazır olana kadar bekle
window.addEventListener('load', function(){
  // metadata.json fetch async, kısa bekleme
  var attempts = 0;
  var interval = setInterval(function(){
    attempts++;
    var inp = document.getElementById('kesfet-search');
    // Eğer veri yüklendiyse (count gösteriliyor)
    var count = document.getElementById('kesfet-count');
    if((count && count.textContent) || attempts > 20){
      clearInterval(interval);
      applyHashToSearch();
    }
  }, 200);
});

window.addEventListener('hashchange', applyHashToSearch);
</script>
