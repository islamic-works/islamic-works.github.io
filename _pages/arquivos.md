---
layout: page
title: Arquivo de Artigos
permalink: /arquivos/
image: archive.jpg
---

<p>Consulte abaixo o histórico completo de artigos publicados no Islamic Works, organizado por ano para facilitar a navegação.</p>

<section class="archive-list">
  {% assign postsByYear = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
  {% for year in postsByYear %}
  <div class="archive-year">
    <h2>{{ year.name }}</h2>
    <ul class="archive-items">
      {% for post in year.items %}
      <li class="archive-item">
        <span class="archive-date">{{ post.date | date: "%d/%m" }}</span>
        <a class="archive-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </li>
      {% endfor %}
    </ul>
  </div>
  {% endfor %}
</section>
