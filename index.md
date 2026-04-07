---
layout: default
title: 我的博客
---

<details style="margin-bottom: 20px;">
  <summary style="cursor: pointer; padding: 8px; background: #f0f0f0; border-radius: 4px;">🔍 搜索文章标题</summary>
  <div style="padding: 12px; background: #f9f9f9; margin-top: 8px; border-radius: 4px;">
    <input type="text" id="search" placeholder="输入关键词..." style="width: 100%; padding: 8px; box-sizing: border-box;">
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
  const searchInput = document.getElementById('search');
  if (searchInput) {
    searchInput.addEventListener('keyup', function() {
      const keyword = this.value.toLowerCase();
      const items = document.querySelectorAll('#posts li');
      items.forEach(item => {
        const title = item.getAttribute('data-title');
        if (title.includes(keyword)) {
          item.style.display = '';
        } else {
          item.style.display = 'none';
        }
      });
    });
  }
</script>