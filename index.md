---
layout: default
title: 我的博客
---

<style>
  :root{--bg:#fff;--text:#333;--code:#f5f5f5}
  body.dark{--bg:#1a1a1a;--text:#e0e0e0;--code:#2d2d2d}
  body{background:var(--bg);color:var(--text);transition:0.3s}
  .theme-toggle{position:fixed;top:20px;right:20px;background:transparent;border:none;font-size:24px;cursor:pointer}
  details{margin-bottom:20px}
  #search{width:100%;padding:8px;background:var(--bg);color:var(--text);border:1px solid #ccc}
  #posts{list-style:none;padding:0}
  #posts li{padding:8px 0;border-bottom:1px solid var(--code)}
  a{color:#0366d6}
  body.dark a{color:#58a6ff}
</style>

<button class="theme-toggle" id="toggle">🌙</button>

<details>
  <summary>🔍 搜索文章</summary>
  <input type="text" id="search" placeholder="输入标题...">
</details>

<h1>最新文章</h1>

<ul id="posts">
  {% for post in site.posts %}
    <li data-title="{{ post.title | downcase }}">
      <a href="{{ post.url }}">{{ post.title }}</a>
      <span>{{ post.date | date: "%Y-%m-%d" }}</span>
    </li>
  {% endfor %}
</ul>

<script>
document.getElementById('search')?.addEventListener('keyup', function() {
  let keyword = this.value.toLowerCase();
  document.querySelectorAll('#posts li').forEach(item => {
    item.style.display = item.getAttribute('data-title').includes(keyword) ? '' : 'none';
  });
});

function toggleTheme() {
  document.body.classList.toggle('dark');
  let btn = document.getElementById('toggle');
  let isDark = document.body.classList.contains('dark');
  btn.innerHTML = isDark ? '☀️' : '🌙';
  localStorage.setItem('theme', isDark ? 'dark' : 'light');
}

let saved = localStorage.getItem('theme');
if (saved === 'dark') {
  document.body.classList.add('dark');
  document.getElementById('toggle').innerHTML = '☀️';
}
</script>