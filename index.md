---
layout: default
title: 我的博客
---

<details style="margin-bottom: 20px;">
  <summary>🔍 搜索文章标题</summary>
  <div style="margin-top: 8px;">
    <input type="text" id="search" placeholder="输入关键词..." style="width: 100%; padding: 8px;">
  </div>
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
</script>