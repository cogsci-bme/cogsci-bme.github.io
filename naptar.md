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
    src="https://calendar.google.com/calendar/embed?src=4c00e7aa0bd8409fb810391e0d4427b5554d569b716b3ff17d6302da25bfb290%40group.calendar.google.com&ctz=Europe%2FBudapest&showTitle=0"
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
