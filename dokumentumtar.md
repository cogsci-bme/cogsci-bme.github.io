---
layout: default
title: Dokumentumtár
permalink: /dokumentumtar/
---

<!-- This page auto-lists the files under /dokumentumtar/. Add a file to
     that folder (in the right subfolder) and it appears here on rebuild;
     no need to edit this page. See dokumentumtar/README.md. -->

<section class="hero">
  <div class="wrap">
    <p class="eyebrow">Hallgatóknak</p>
    <h1>Dokumentumtár</h1>
    <p class="sub">Letölthető anyagok mesterszakos hallgatóinknak: mintatantervek, záróvizsga-tételek, diplomamunka-sablonok, etikai és plágium-nyilatkozatok, felvételi tájékoztatók. Az MSc képzés dokumentumait fentebb, az MA képzés dokumentumait lentebb találjátok.</p>
  </div>
</section>

<section class="section">
  <div class="wrap">
    <p class="eyebrow">Számítógépes és kognitív idegtudomány MSc</p>
    <h2 class="section-title">Idegtudomány MSc – dokumentumok</h2>
    <div class="repo">
      {% assign cog = site.static_files | where_exp: "f", "f.path contains '/dokumentumtar/master_CogSci/'" %}
      {% assign cog_groups = cog | group_by_exp: "f", "f.path | remove_first: '/dokumentumtar/master_CogSci/' | split: '/' | first" %}
      {% for g in cog_groups %}
      <div class="repo-group">
        <h3>{% case g.name %}{% when 'Felvi' %}Felvételizőknek{% when 'Zarovizsga' %}Diákoknak{% else %}{{ g.name }}{% endcase %}</h3>
        <ul>
          {% for f in g.items %}
          <li><a href="{{ site.baseurl }}{{ f.path | uri_escape }}">{{ f.name }}</a><span class="ext">{{ f.extname | remove: '.' }}</span></li>
          {% endfor %}
        </ul>
      </div>
      {% endfor %}
    </div>
  </div>
</section>

<section class="section section--tint">
  <div class="wrap">
    <p class="eyebrow">Pszichológia MA</p>
    <h2 class="section-title">Pszichológia MA – dokumentumok</h2>
    <div class="repo">
      {% assign psz = site.static_files | where_exp: "f", "f.path contains '/dokumentumtar/master_pszi/'" %}
      {% assign psz_groups = psz | group_by_exp: "f", "f.path | remove_first: '/dokumentumtar/master_pszi/' | split: '/' | first" %}
      {% for g in psz_groups %}
      <div class="repo-group">
        <h3>{% case g.name %}{% when 'Felvi' %}Felvételizőknek{% when 'Zarovizsga' %}Diákoknak{% else %}{{ g.name }}{% endcase %}</h3>
        <ul>
          {% for f in g.items %}
          <li><a href="{{ site.baseurl }}{{ f.path | uri_escape }}">{{ f.name }}</a><span class="ext">{{ f.extname | remove: '.' }}</span></li>
          {% endfor %}
        </ul>
      </div>
      {% endfor %}
    </div>
  </div>
</section>
