---
layout: default
title: 标签
permalink: /tags/
---

{% assign tags = site.tags | sort %}
<div style="display:flex;flex-wrap:wrap;gap:16px;font-size:1.2em;margin:1em 0;">
{% for tag in tags %}
<a class="tag-btn" data-tag="{{ tag[0] }}" href="javascript:void(0);" style="font-style:italic;">{{ tag[0] }} {{ tag[1].size }}</a>
{% endfor %}
<a class="tag-btn" data-tag="all" href="javascript:void(0);" style="font-style:italic;">查看全部</a>
</div>
<hr>

{% for tag in tags %}
<div class="tag-block" data-group="{{ tag[0] }}">
<h3 style="font-style:italic;">{{ tag[0] }} {{ tag[1].size }}</h3>
<ul>
{% for post in tag[1] %}
<li><a href="{{ post.url }}">{{ post.title }}</a> {{ post.date | date: "%Y-%m-%d" }}</li>
{% endfor %}
</ul>
</div>
{% endfor %}

<script>
// 筛选函数
function switchTag(targetName) {
  const blocks = document.querySelectorAll('.tag-block');
  blocks.forEach(block => {
    if (targetName === 'all' || block.dataset.group === targetName) {
      block.style.display = 'block';
    } else {
      block.style.display = 'none';
    }
  })
}

// 从地址栏hash读取标签
function getHashTag() {
  const h = window.location.hash.slice(1);
  return h ? decodeURIComponent(h) : 'all';
}

// 绑定顶部标签点击
document.querySelectorAll('.tag-btn').forEach(btn => {
  btn.onclick = () => {
    switchTag(btn.dataset.tag);
  }
})

// 页面加载完执行一次
function init() {
  switchTag(getHashTag());
}
init();

// 监听hash变化
window.addEventListener('hashchange', () => {
  switchTag(getHashTag());
})
</script>
