---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: 專輯一覽
---

<h1>專輯一覽</h1>
<ul class="album-list">
  {% for page in site.pages %}
    {% if page.layout == "album" %}
      {% assign album = site.data.albums[page.album_data] %}
      <li>
        <a href="{{ page.url }}">{{ album.album_title }}</a>
        <span class="album-year">（{{ album.album_year }}）</span>
      </li>
    {% endif %}
  {% endfor %}
</ul>

<style>
.album-list {
  list-style: none;
  padding: 0;
}

.album-list li {
  margin: 0.5rem 0;
  font-size: 1rem;
}

.album-list a {
  color: #333;
  text-decoration: none;
  font-weight: bold;
}

.album-list a:hover {
  text-decoration: underline;
}

.album-year {
  color: #777;
  font-size: 0.9rem;
  margin-left: 0.5rem;
}
</style>

