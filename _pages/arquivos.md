---
layout: page
title: Arquivo
permalink: /arquivos/
image: archive.jpg
navigation_label: "Arquivo"
navigation_header: true
navigation_header_order: 20
navigation_footer_group: "Recursos"
navigation_footer_group_order: 20
navigation_footer_order: 10
---
<p>Consulte abaixo o histórico completo de artigos publicados no Islamic Works, organizado por ano para facilitar a navegação.</p>

<section class="archive-list">
  {% assign published_posts = site.posts | where_exp: "post", "post.date <= site.time" %}
  {% assign postsByYear = published_posts | group_by_exp: "post", "post.date | date: '%Y'" %}
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
