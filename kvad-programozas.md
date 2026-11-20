---
layout: default
title: Programozási alapismeretek – betekintő
permalink: /kvad/programozas/
theme: green
# Nem listázott oldal: nincs rá link, kimarad a sitemap.xml-ből, és a
# keresőknek noindex jelzést kap (_includes/meta.html).
sitemap: false
noindex: true

# A YouTube-lejátszási lista azonosítója (csak a "teljes lista" linkhez).
playlist: PLRFBSL7aDrD0

# Videók. index: a kártyán megjelenő sorszám; id: a YouTube-videó azonosítója
# (a youtu.be/ utáni 11 karakter, a ?si=... rész nélkül).
videos:
  - index: 1
    id: wHitq7hmKDQ
    title: Mi az adat?
    summary: Mit jelent a viselkedés tudományos értelemben, és miért ilyen zajos minden adat, ami az emberekről szól? A pszichológia egy eredményt húszból tizenkilenc ismétlésnél vesz komolyan, a részecskefizika nagyjából hárommilliónál. Utána arról, hogy minden mérés közvetett (a pókos példa), és hogy az adatokat két szempont szerint érdemes elrendezni. Rögzítheted, amit az emberek mondanak, vagy amit csinálnak. Az adatot értelmezheted szövegként, vagy kifejezheted számokkal.
  - index: 2
    id: lf2bAbwdhuI
    title: Miért nem Excel? Programozás és AI
    summary: Egy kimaradt képlet egy nagy hatású közgazdasági tanulmányban, dátummá alakított génnevek, tizenhatezer elveszett covid-teszt. A táblázatkezelők nem hagynak nyomot, hamar a korlátaikba ütköznek, és nem bírják a nagy adathalmazokat. A programozási nyelv átvezet az írásbeliségbe. A nagy nyelvmodellek óta pedig a kód betűhív megírása helyett az eredmények ellenőrzésén van a hangsúly.
  - index: 3
    id: qVuMC-yKOqU
    title: Mi az ábra?
    summary: Az ábra nem dísz, és nem ártatlan. A 18. századi botanikai rajzoktól eljutunk a torzítás, az ügyetlenség és a hangsúlyozás közötti különbségig, amelyek ugyanazokkal az eszközökkel dolgoznak. Az AI által rajzolt grafikon is tele van döntésekkel, csak nem a tieiddel.
    reading:
      - Lorraine Daston, Peter Galison, <em>Objectivity</em>. Zone Books, 2007.
      - Alberto Cairo, <em>How Charts Lie</em>. W. W. Norton, 2019.
      - Darrell Huff, <em>How to Lie with Statistics</em>. W. W. Norton, 1954.
  - index: 4
    id: cw4mZbqj4KE
    title: Melyik adatra melyik ábra? (1. rész)
    summary: Kategorikus, sorrendi és folyamatos adatok. Hisztogram és sűrűségábra, és miért rajzol a simító algoritmus negatív reakcióidőt. Oszlopdiagram, amelynek nulláról kell indulnia. Melyik ábrázolási elemet olvassuk le a legpontosabban, és melyiket a legrosszabbul.
    reading:
      - Claus O. Wilke, <em>Fundamentals of Data Visualization</em>. O'Reilly, 2019. <a href="https://clauswilke.com/dataviz/">Ingyenesen olvasható online</a>.
      - William S. Cleveland, Robert McGill (1984), Graphical perception. <em>Journal of the American Statistical Association</em> 79(387), 531–554.
  - index: 5
    id: nqncx3vq1Zw
    title: Melyik adatra melyik ábra? (2. rész)
    summary: Pontdiagram és átfedés, mit rejt el a dobozábra, esőfelhő- és hegedűábra. Két kategorikus változó, idősorok, három változó egy ábrán vagy panelekre bontva. Végül három dolog, amit ne csinálj soha (tortadiagram, dinamitábra, szivárványszínskála).
    reading:
      - Tracey L. Weissgerber et al. (2015), Beyond bar and line graphs. <em>PLOS Biology</em> 13(4), e1002128.
      - Micah Allen et al. (2019), Raincloud plots. <em>Wellcome Open Research</em> 4, 63.
  - index: 6
    id: Hc5c9BbSDkU
    title: Ismerkedés a Colabbal
    summary: Végigmegyünk a bemutató jegyzetfüzeten. Kódcella futtatása, egy kis táblázat, a beépített AI-asszisztens megkérése, hogy magyarázzon el, alakítson át vagy írjon kódot, és mit csinálj, ha hibaüzenetet kapsz.
    notebook: bemutato

notebooks:
  bemutato:
    title: Ismerkedés a Colabbal
    url: https://colab.research.google.com/drive/1MRtTSDisZ8Eeb3-JWhqYMjGuoWjTsLsN?usp=sharing
  abrak:
    title: Ábrák készítése AI-asszisztenssel
    url: https://colab.research.google.com/drive/1NNWa47GqniI9X5o_KPGAneJBNNq7z_EL?usp=sharing
---

<!-- HERO -->
<section class="hero">
  <div class="wrap">
    <p class="eyebrow">Kognitív és viselkedéses adattudomány · 1. félév · Modul 01</p>
    <h1>Programozási alapismeretek, adatkezelés, adatvizualizáció</h1>
    <p class="sub">Betekintő a képzés első kurzusába: rövid videók és kipróbálható Colab-jegyzetfüzetek. Az adatelemzéshez szükséges kódot egy AI-asszisztens írja, a döntések és az ellenőrzés a tieid.</p>
    <div class="chips">
      <span class="chip">{{ page.videos | size }} videó</span>
      <span class="chip">2 Colab-jegyzetfüzet</span>
      <span class="chip">Telepítés nélkül, böngészőben</span>
    </div>
    <div class="hero-actions">
      <a class="btn btn--solid" href="#videok">Videók</a>
      <a class="btn btn--ghost" href="#colab">Próbáld ki</a>
      <a class="btn btn--ghost" href="{{ site.baseurl }}/kvad/">A képzés oldala</a>
    </div>
  </div>
</section>

<!-- A KURZUS LÉNYEGE -->
<section class="section" id="lenyeg">
  <div class="wrap grid-2">
    <div>
      <p class="eyebrow">A kurzusról</p>
      <h2 class="section-title">Nem programozni tanulsz, hanem kérdezni és ellenőrizni</h2>
      <p class="lead">Az adatokkal végzett munka a táblázatkezelőkön túl programozási nyelvet kíván. Régen ehhez évekig kellett programozni tanulni. Ma egy AI-asszisztens természetes nyelvből is megírja a kódot.</p>
      <p style="margin-top:1.2rem;color:var(--muted)">A precizitás ettől nem tűnik el, csak máshová kerül: a kód betűhív megírásáról az eredmények ellenőrzésére. A kurzuson azt tanuljuk meg, hogyan kérj kódot az asszisztenstől, és hogyan ellenőrizd, amit kaptál: ábrákkal, egyszerű tesztekkel, és eleinte olyan adatokon, ahol előre tudod a helyes választ.</p>
    </div>
    <div class="pillar" style="align-self:start">
      <p class="n">A 2. VIDEÓBÓL</p>
      <h3>Az ellenőrzést nem lehet megúszni</h3>
      <p>Az AI által írt kód általában lefut, és éppen ez benne a veszélyes. Ha két táblázatot rosszul kapcsol össze, ha csendben eldobja a hiányos sorokat, vagy egy statisztikai próbát rossz beállítással futtat, nem kapsz hibaüzenetet. Kapsz egy rossz eredményt, ami ugyanolyan meggyőzően néz ki, mint egy jó.</p>
    </div>
  </div>
</section>

<!-- VIDEÓK -->
<section class="section section--tint" id="videok">
  <div class="wrap">
    <p class="eyebrow">Videók</p>
    <h2 class="section-title">A kurzus első hat videója</h2>
    <p style="color:var(--muted);max-width:62ch">A lejátszó csak akkor töltődik be a YouTube-ról, ha rákattintasz. A teljes lista <a href="https://www.youtube.com/playlist?list={{ page.playlist }}">a YouTube-on</a> is megtalálható.</p>
    <div class="vgrid">
      {% for v in page.videos %}
      <article class="vcard">
        <!-- Kattintásra a lenti szkript cseréli le a valódi lejátszóra; szkript nélkül a YouTube-ra visz. -->
        <a class="vplay" href="https://www.youtube.com/watch?v={{ v.id }}"
           data-src="https://www.youtube-nocookie.com/embed/{{ v.id }}?autoplay=1&amp;rel=0"
           data-title="{{ v.title }}">
          <span class="vplay-n">{{ v.index }}. videó</span>
          <span class="vplay-icon" aria-hidden="true">▶</span>
          <span class="vplay-t">{{ v.title }}</span>
        </a>
        <div class="vbody">
          <h3>{{ v.index }}. {{ v.title }}</h3>
          <p>{{ v.summary }}</p>
          {% if v.reading %}
          <p class="vread-h">Olvasnivaló</p>
          <ul class="vread">
            {% for r in v.reading %}<li>{{ r }}</li>{% endfor %}
          </ul>
          {% endif %}
          {% if v.notebook %}
          {% assign nb = page.notebooks[v.notebook] %}
          <p class="vnb">Jegyzetfüzet: <a href="{{ nb.url }}">{{ nb.title }}</a></p>
          {% endif %}
        </div>
      </article>
      {% endfor %}
    </div>
  </div>
</section>

<!-- COLAB -->
<section class="section" id="colab">
  <div class="wrap">
    <p class="eyebrow">Próbáld ki</p>
    <h2 class="section-title">Colab-jegyzetfüzetek</h2>
    <p style="color:var(--muted);max-width:62ch">A Colab a Google böngészőben futó programozási környezete. Nem kell hozzá semmit telepíteni, és van beépített AI-asszisztense. Egy Google-fiókra van szükséged.</p>
    <p class="nb-note"><strong>Fontos:</strong> a megosztott jegyzetfüzeteket nem tudod szerkeszteni. Megnyitás után válaszd a <strong>Fájl → Másolat mentése a Drive-ba</strong> menüpontot, és a saját másolatodban dolgozz.</p>
    <p class="nb-note"><strong>Diákkedvezmény:</strong> a szakirányú továbbképzés résztvevői a BME hallgatói, így jogosultak lehetnek a Google egyetemi hallgatóknak szóló ajánlatára, amellyel egy évig ingyenesen használhatják a Google fizetős AI-csomagját. A pontos feltételek és a jelentkezés <a href="https://one.google.com/ai-student?g1_landing_page=75">a Google oldalán</a> találhatók.</p>
    <div class="pillars">
      <div class="pillar">
        <p class="n">01 · BEMUTATÓ</p>
        <h3>{{ page.notebooks.bemutato.title }}</h3>
        <p>Hét rövid lépés: kódcella futtatása, egy kis táblázat, és az AI-asszisztens három fő funkciója (kód magyarázata, átalakítása és megírása). A végén kiderül, mit csinálj, ha hibaüzenetet kapsz. A 6. videó végigvezet rajta.</p>
        <p style="margin-top:1.2rem"><a class="btn btn--brand" href="{{ page.notebooks.bemutato.url }}">Megnyitás a Colabban</a></p>
      </div>
      <div class="pillar">
        <p class="n">02 · ADATVIZUALIZÁCIÓ 1 · BETEKINTŐ</p>
        <h3>{{ page.notebooks.abrak.title }}</h3>
        <p>Nyolc feladat egy filmes adathalmazon, a 3–5. videó anyagára építve. Az asszisztens írja a kódot, te ellenőrzöd: hány film maradt ki csendben az ábráról, hol lóg a tengely, mit rejt el egy dinamitábra. A feladatok három szinten nehezednek, az előre megírt kéréstől a saját megfogalmazásig.</p>
        <p style="margin-top:1.2rem"><a class="btn btn--brand" href="{{ page.notebooks.abrak.url }}">Megnyitás a Colabban</a></p>
        <p class="nb-wip">A kurzus további jegyzetfüzetei készülnek.</p>
      </div>
    </div>
  </div>
</section>

<!-- JÓ ÁBRA, ROSSZ ÁBRA -->
<section class="section section--tint" id="abrak">
  <div class="wrap">
    <p class="eyebrow">Ízelítő</p>
    <h2 class="section-title">Ugyanaz az adat, kétféleképpen</h2>
    <p style="color:var(--muted);max-width:62ch">Néhány ábrapár a 4–5. videóból. A bal oldali változat félrevezet vagy elrejt valamit, a jobb oldali ugyanazt az adatot mutatja becsületesen.</p>

    <div class="pair">
      <figure><span class="verdict verdict--bad">Rossz</span><img src="{{ site.baseurl }}/images/kvad/programozas/07_munkahely_oszlop_tengely_rossz.png" alt="Oszlopdiagram, amelynek tengelye 60-nál indul, ezért a különbségek eltúlzottnak látszanak" loading="lazy"></figure>
      <figure><span class="verdict verdict--good">Jobb</span><img src="{{ site.baseurl }}/images/kvad/programozas/06_munkahely_oszlop.png" alt="Ugyanaz az oszlopdiagram nulláról induló tengellyel" loading="lazy"></figure>
      <p class="pair-cap">Az oszlopdiagramon a hosszt hasonlítjuk össze. Ha a tengely nem nulláról indul, a hossz hazudik.</p>
    </div>

    <div class="pair pair--stack">
      <figure><span class="verdict verdict--bad">Rossz</span><img src="{{ site.baseurl }}/images/kvad/programozas/28_dinamit_abra_rossz.png" alt="Három szinte egyforma dinamitábra: átlag oszlopként, hibasávval" loading="lazy"></figure>
      <figure><span class="verdict verdict--good">Jobb</span><img src="{{ site.baseurl }}/images/kvad/programozas/29_dinamit_igazsag_pontok.png" alt="Ugyanaz az adat pontokkal: szoros eloszlás, egy kiugró érték, illetve csoportonként három megfigyelés" loading="lazy"></figure>
      <p class="pair-cap">Három szinte egyforma dinamitábra, és mögöttük három teljesen különböző adathalmaz.</p>
    </div>

    <div class="pair">
      <figure><span class="verdict verdict--bad">Rossz</span><img src="{{ site.baseurl }}/images/kvad/programozas/12_dobozabra_elrejti_bimodalis.png" alt="Dobozábra három csoporttal; a C csoport kétpúpú eloszlása nem látszik" loading="lazy"></figure>
      <figure><span class="verdict verdict--good">Jobb</span><img src="{{ site.baseurl }}/images/kvad/programozas/14_esofelho_kozepes_n.png" alt="Esőfelhő-ábra ugyanarról az adatról: sűrűség, doboz és az egyes megfigyelések" loading="lazy"></figure>
      <p class="pair-cap">A dobozábra elrejti az eloszlás alakját. Az esőfelhő-ábrán látszik, hogy a C csoportban kétféle ember van.</p>
    </div>

    <div class="pair">
      <figure><span class="verdict verdict--bad">Rossz</span><img src="{{ site.baseurl }}/images/kvad/programozas/24_harom_folytonos_szin_rossz_szivarvany.png" alt="Harmadik változó szivárványszínskálával" loading="lazy"></figure>
      <figure><span class="verdict verdict--good">Jobb</span><img src="{{ site.baseurl }}/images/kvad/programozas/23_harom_folytonos_szin_jo_viridis.png" alt="Ugyanaz egyenletes, színvakok számára is olvasható színskálával" loading="lazy"></figure>
      <p class="pair-cap">A szivárványskálán a szem ott is határt lát, ahol az adatban nincs, és a színvak nézők számára olvashatatlan.</p>
    </div>
  </div>
</section>

<!-- ÉRDEKEL? -->
<section class="section">
  <div class="wrap">
    <div class="applybox">
      <h2>Érdekel a képzés?</h2>
      <p>Ez a kurzus a Kognitív és viselkedéses adattudomány szakirányú továbbképzés első félévének része. A tantervről, a jelentkezésről és a képzés menetéről a képzés oldalán és a gyakran ismételt kérdések között olvashatsz. Kérdéseidet e-mailben is szívesen fogadjuk: <a href="mailto:babarczy.anna@ttk.bme.hu">babarczy.anna@ttk.bme.hu</a>.</p>
      <div class="links">
        <a class="btn" href="{{ site.baseurl }}/kvad/">A képzés oldala</a>
        <a class="btn ghost" href="{{ site.baseurl }}/kvad/gyik/">Gyakran ismételt kérdések</a>
      </div>
    </div>
  </div>
</section>

<script>
  // Kattintásig nem töltünk be semmit a YouTube-ról (ld. fonts.css: a látogató IP-címe ne menjen ki kérés nélkül).
  document.querySelectorAll('.vplay').forEach(function (a) { // minden videó-helyőrző
    a.addEventListener('click', function (e) { // kattintásra
      e.preventDefault(); // ne kövesse a tartalék YouTube-linket
      var f = document.createElement('iframe'); // a lejátszó kerete
      f.src = a.dataset.src; // adatvédelmi módú beágyazási cím, automatikus lejátszással
      f.title = a.dataset.title; // a keret neve képernyőolvasóknak
      f.allow = 'autoplay; encrypted-media; picture-in-picture; fullscreen'; // a lejátszó engedélyei
      f.allowFullscreen = true; // teljes képernyős gomb
      a.replaceWith(f); // a helyőrző helyére kerül a lejátszó
    });
  });
</script>
