---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: 專輯一覽
---

<div class="content">
<h1>專輯一覽</h1>
<ul class="album-list">
  {% assign album_pages = site.pages | where: "layout", "album" %}
  {% assign sorted_album_pages = album_pages | sort: "sidebar_sort_order" | reverse %}
  {% for page in sorted_album_pages %}
    {% assign album = site.data.albums[page.album_data] %}
    <li>
      <a href="{{ page.url | relative_url }}">{{ album.album_title }}</a>
      <span class="album-year">（{{ album.album_year }}）</span>
    </li>
  {% endfor %}
</ul>
</div>
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

