---
layout: album
title: About
permalink: /about/
---
<style>
.song-nav {
  display: flex;
  flex-wrap: wrap;            /* ✅ 允許按鈕換行 */
  gap: 0.5em;
  padding: 0.5em 0;
  border-bottom: 1px solid #ccc;
  margin-bottom: 1em;
}

.song-nav a {
  display: inline-block;
  padding: 0.4em 0.8em;
  font-size: 0.9em;
  background: #f7f7f7;
  border: 1px solid #ccc;
  border-radius: 0.4em;
  color: #333;
  text-decoration: none;
  white-space: nowrap;
  transition: background 0.3s;
}

.song-nav a:hover {
  background: #ddd;
}

  .lang-tabs {
    margin: 1em 0;
  }

  .lang-tabs button {
    padding: 0.5em 1.2em;
    margin-right: 8px;
    border: 1px solid #ddd;
    background-color: #f8f8f8;
    color: #333;
    cursor: pointer;
    font-size: 0.9rem;  /* 縮小字體 */
    border-radius: 4px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    transition: background-color 0.3s ease, color 0.3s ease, transform 0.2s ease;
  }

  .lang-tabs button.active {
    background-color: #333; /* 深灰色背景 */
    color: white;
    transform: scale(1.05);
  }

  .lang-tabs button:hover {
    background-color: #e0e0e0;
    transform: scale(1.05);
  }

  .song-info {
    text-align: center;
    font-size: 1.1rem;
    margin-bottom: 1em;
    color: #333;
  }

  .song-info .title {
    font-size: 1.3rem;
    font-weight: bold;
  }

  .song-info .credits {
    margin-top: 0.5em;
  }

  .lyrics-wrapper {
    display: flex;
    flex-wrap: wrap;
    gap: 1.5em;
    margin-top: 1em;
  }

  .lyrics-block {
    flex-grow: 1;
    flex-basis: 0;
    padding: 1.2em;
    border: 1px solid #ddd;
    display: none;
    white-space: pre-line;
    background: #f9f9f9;
    border-radius: 4px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  }

  .lyrics-block.active {
    display: block;
  }

  .separator {
    margin: 2em 0;
    border-top: 2px solid #ddd;
    width: 100%;
  }
</style>
<script>
function toggleLang(langId) {
  const btn = document.getElementById(`btn-${langId}`);
  const block = document.getElementById(`lyrics-${langId}`);
  const isActive = btn.classList.contains('active');
  btn.classList.toggle('active', !isActive);
  block.classList.toggle('active', !isActive);
}
</script>

<div class="song-nav">
  <strong>曲目列表：</strong>
  {% for song in site.data.songs %}
    <a href="#song{{ forloop.index }}">{{ forloop.index }}. {{ song.title }}</a>
  {% endfor %}
</div>

{% for song in site.data.songs %}
<div class="song-block" id="song{{ forloop.index }}">
  <div class="song-title">{{ forloop.index }}. {{ song.title }}</div>
  <div class="song-meta">詞：{{ song.lyrics_by }}<br>曲：{{ song.music_by }}</div>

  <div class="lang-tabs">
    {% if song.lyrics.zh %}
      <button onclick="toggleLang('zh{{ forloop.index }}')" {% if song.default_language == 'zh' %}class="active"{% endif %} id="btn-zh{{ forloop.index }}">中文</button>
    {% endif %}
    {% if song.lyrics.en %}
      <button onclick="toggleLang('en{{ forloop.index }}')" {% if song.default_language == 'en' %}class="active"{% endif %} id="btn-en{{ forloop.index }}">English</button>
    {% endif %}
    {% if song.lyrics.jp %}
      <button onclick="toggleLang('jp{{ forloop.index }}')" {% if song.default_language == 'jp' %}class="active"{% endif %} id="btn-jp{{ forloop.index }}">日本語</button>
    {% endif %}
  </div>

  <div class="lyrics-wrapper">
    {% if song.lyrics.zh %}
      <div id="lyrics-zh{{ forloop.index }}" class="lyrics-block {% if song.default_language == 'zh' %}active{% endif %}">{{ song.lyrics.zh | newline_to_br }}</div>
    {% endif %}
    {% if song.lyrics.en %}
      <div id="lyrics-en{{ forloop.index }}" class="lyrics-block {% if song.default_language == 'en' %}active{% endif %}">{{ song.lyrics.en | newline_to_br }}</div>
    {% endif %}
    {% if song.lyrics.jp %}
      <div id="lyrics-jp{{ forloop.index }}" class="lyrics-block" {% if song.default_language == 'jp' %}active{% endif %}>{{ song.lyrics.jp | newline_to_br }}</div>
    {% endif %}
  </div>
</div>

{% unless forloop.last %}
  <hr>
{% endunless %}
{% endfor %}
