---
layout: page
title: Naptár
permalink: /naptar/
hero: true
eyebrow: Tanszék
lead: A félév menetrendje és a tanszéki események egy helyen.
---

<!--
  TÖBB NAPTÁR MEGJELENÍTÉSE
  ------------------------------------------------------------------
  Egy beágyazásban több naptár is megjeleníthető (színkódolva).
  Minden további naptárhoz adj hozzá egy újabb `&src=...` paramétert
  az alábbi src URL-be. A naptár azonosítója a Google Naptár
  beállításai > "A naptár integrálása" résznél található
  ("Naptár-azonosító", pl. valami@group.calendar.google.com).
  A `@` jelet `%40`-re kell cserélni az URL-ben.

  Színek (opcionális): minden `&src=` után tehetsz egy `&color=%23RRGGBB`
  paramétert; a sorrend számít (az első color az első src-hez tartozik).

  Példa két naptárral, színekkel:

  src="https://calendar.google.com/calendar/embed?ctz=Europe%2FBudapest&showTitle=0
       &src=ELSO_NAPTAR_ID%40group.calendar.google.com&color=%230b8043
       &src=MASODIK_NAPTAR_ID%40group.calendar.google.com&color=%233f51b5"

  (Az src értéke egyetlen sorban legyen, szóköz/sortörés nélkül.)
  Minden megjelenítendő naptárnak nyilvánosnak kell lennie.
-->
<div class="calendar-embed">
  <iframe
    title="Tanszéki naptár"
    src="https://calendar.google.com/calendar/embed?src=9953bbb5e334848db13648e8808fd26ff509104af9b0a6bc982fe83c96d7fe9a%40group.calendar.google.com&src=e561e6eea37bb38ab350b7e6073e6daf99168a607ba5f6dd4a75c824234b398f%40group.calendar.google.com&src=3af81d7394db4e18c1e89fa4a7a7f8e686e4880425b96319e4a59770d463397f%40group.calendar.google.com&src=7885f2781b071b11978a811b4eceda051cc01c0ddfb8c2d8cb0615d8f58db28d%40group.calendar.google.com&src=b12a85fb791fefba6991343db505fac3421c3d3aaaf83b055c060b28b4c53275%40group.calendar.google.com&src=de98cd054ece27dfc1e574dd857417e4556acc3fc1b5e2593d7ee4b95a168648%40group.calendar.google.com&ctz=Europe%2FBudapest"
    loading="lazy"
    style="border:0"
    width="100%"
    height="700"
    frameborder="0"
    scrolling="no"></iframe>
</div>

<p class="muted" style="margin-top:1rem">A naptár bal alsó sarkában található jelölőnégyzetekkel egyenként ki- és bekapcsolható az egyes naptárak megjelenítése. Ha valamelyik naptárt a saját Google-fiókodban is követni szeretnéd, kattints a naptár neve melletti három pontra, majd válaszd a „Hozzáadás a saját naptárhoz” lehetőséget – az események ezután a saját Google Naptáradban is megjelennek.</p>

<style>
  .calendar-embed{border:1px solid var(--line);border-radius:14px;overflow:hidden;background:#fff}
  .calendar-embed iframe{display:block;width:100%;height:700px}
  @media(max-width:640px){.calendar-embed iframe{height:560px}}
</style>
