---
layout: page
title: Naptár
permalink: /naptar/
hero: true
eyebrow: Tanszék
lead: A félév menetrendje és a tanszéki események egy helyen.
---

A tantárgyakhoz tartozó tárgyleírásokat a kar oldalán, [itt](https://www.ttk.bme.hu/tantargyak?keys=&field_felelos_tanszeke_value=7) találjátok.

A 2026/27-es tanév őszi óráinak időpontjai még nem véglegesek, és a félév kezdetéig még változhatnak.

<!--
  TÖBB NAPTÁR MEGJELENÍTÉSE
  ------------------------------------------------------------------
  Egy beágyazásban több naptár is megjeleníthető (színkódolva).
  Minden további naptárhoz adj hozzá egy újabb `&src=...` paramétert
  az alábbi `data-embed-src` URL-be. A naptár azonosítója a Google
  Naptár beállításai > "A naptár integrálása" résznél található
  ("Naptár-azonosító", pl. valami@group.calendar.google.com).
  A `@` jelet `%40`-re kell cserélni az URL-ben.

  Színek (opcionális): minden `&src=` után tehetsz egy `&color=%23RRGGBB`
  paramétert; a sorrend számít (az első color az első src-hez tartozik).

  Példa két naptárral, színekkel:

  data-embed-src="https://calendar.google.com/calendar/embed?ctz=Europe%2FBudapest&showTitle=0
       &src=ELSO_NAPTAR_ID%40group.calendar.google.com&color=%230b8043
       &src=MASODIK_NAPTAR_ID%40group.calendar.google.com&color=%233f51b5"

  (Az érték egyetlen sorban legyen, szóköz/sortörés nélkül.)
  Minden megjelenítendő naptárnak nyilvánosnak kell lennie.

  ADATVÉDELEM: a naptár nem töltődik be automatikusan. A látogatónak rá
  kell kattintania a gombra, és csak ekkor épül fel a kapcsolat a Google
  szerverei felé. Ezt a `data-embed-src` attribútum és az oldal alján
  lévő szkript együtt oldja meg — az iframe csak kattintásra jön létre.
-->
<div class="calendar-embed" data-embed-src="https://calendar.google.com/calendar/embed?src=9953bbb5e334848db13648e8808fd26ff509104af9b0a6bc982fe83c96d7fe9a%40group.calendar.google.com&color=%234986E7&src=e561e6eea37bb38ab350b7e6073e6daf99168a607ba5f6dd4a75c824234b398f%40group.calendar.google.com&color=%2316A765&src=3af81d7394db4e18c1e89fa4a7a7f8e686e4880425b96319e4a59770d463397f%40group.calendar.google.com&color=%2392E1C0&src=7885f2781b071b11978a811b4eceda051cc01c0ddfb8c2d8cb0615d8f58db28d%40group.calendar.google.com&color=%23FFAD46&src=b12a85fb791fefba6991343db505fac3421c3d3aaaf83b055c060b28b4c53275%40group.calendar.google.com&color=%23F83A22&src=de98cd054ece27dfc1e574dd857417e4556acc3fc1b5e2593d7ee4b95a168648%40group.calendar.google.com&color=%23C2C2C2&ctz=Europe%2FBudapest">
  <div class="embed-gate">
    <h3>Tanszéki naptár</h3>
    <p>A naptárat a Google Naptár szolgáltatás jeleníti meg. Ha betöltöd, a
    böngésződ közvetlenül a Google szervereihez kapcsolódik: az IP-címed és a
    böngésződ adatai a Google-höz kerülnek, és a Google sütiket helyezhet el az
    eszközödön. Ezért a naptár csak külön kattintásra töltődik be.</p>
    <button type="button" class="embed-load">Naptár betöltése</button>
    <p class="embed-alt">Vagy <a href="https://calendar.google.com/calendar/embed?src=9953bbb5e334848db13648e8808fd26ff509104af9b0a6bc982fe83c96d7fe9a%40group.calendar.google.com&ctz=Europe%2FBudapest" target="_blank" rel="noopener">nyisd meg új lapon</a>.</p>
  </div>
</div>

<p class="muted" style="margin-top:1rem">A két képzés (MSc, MA) két évfolyamát (I., II.) külön naptárakban találjátok, ahogyan a BME fontos dátumait, és a tanszék további képzéseit is. A naptár jobb fölső sarkában található jelölőnégyzetekkel egyenként ki- és bekapcsolható az egyes naptárak megjelenítése. Ha valamelyik naptárt a saját Google-fiókodban is követni szeretnéd, kattints a naptár aljában látható "add to Google Calendar" linkre. Ezután kiválaszhatod, melyik naptár(ak)at szeretnéd követni. A naptár(ak)ban látható események események ezután a saját Google Naptáradban is megjelennek.</p>

<style>
  .calendar-embed{border:1px solid var(--line);border-radius:14px;overflow:hidden;background:#fff}
  .calendar-embed iframe{display:block;width:100%;height:700px}
  @media(max-width:640px){.calendar-embed iframe{height:560px}}
  .embed-gate{padding:clamp(1.5rem,4vw,2.5rem);text-align:center;background:var(--bg-tint)}
  .embed-gate h3{font-family:var(--display);font-weight:600;font-size:1.1rem;color:var(--brand-deep);margin:0 0 .6rem}
  .embed-gate p{max-width:56ch;margin:0 auto 1.2rem;font-size:.9rem;color:var(--muted)}
  .embed-gate .embed-alt{margin-bottom:0;font-size:.82rem}
  .embed-load{font-family:var(--mono);font-size:.8rem;letter-spacing:.03em;cursor:pointer;
    border:0;border-radius:8px;padding:.7rem 1.4rem;background:var(--brand-deep);color:#fff}
  .embed-load:hover{background:var(--brand-bright)}
</style>

<!-- Kattintásra tölti be a beágyazott naptárt: az iframe csak ekkor jön létre,
     így az oldal megnyitása önmagában nem küld adatot a Google-nek. -->
<script>
  (function () {
    var box = document.querySelector('.calendar-embed[data-embed-src]');
    if (!box) return;
    var btn = box.querySelector('.embed-load');
    if (!btn) return;
    btn.addEventListener('click', function () {
      var frame = document.createElement('iframe');
      frame.title = 'Tanszéki naptár';
      frame.src = box.getAttribute('data-embed-src');
      frame.setAttribute('frameborder', '0');
      frame.setAttribute('scrolling', 'no');
      box.textContent = '';
      box.appendChild(frame);
    });
  })();
</script>
