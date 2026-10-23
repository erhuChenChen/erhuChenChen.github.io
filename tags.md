---
layout: default
title: 标签
permalink: /tags/
---

# 标签

<style>
.tag-btn {
  font-style: italic;
  text-decoration: none;
  color: #0066cc;
  cursor: pointer;
}
.tag-btn.active {
  color: #000 !important;
}
</style>

{% assign tags = site.tags | sort %}
<div style="display:flex;flex-wrap:wrap;gap:12px;font-size:0.85em;margin:1em 0;">
{% for tag in tags %}
<a class="tag-btn" data-tag="{{ tag[0] }}" href="javascript:void(0);">{{ tag[0] }} {{ tag[1].size }}</a>
{% endfor %}
<a class="tag-btn" data-tag="all" href="javascript:void(0);">查看全部</a>
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
function switchTag(targetName) {
  console.log("读到的标签：", targetName);
  const blocks = document.querySelectorAll('.tag-block');
  blocks.forEach(block => {
    block.style.display = (targetName === 'all' || block.dataset.group === targetName) ? 'block' : 'none';
  })

  document.querySelectorAll('.tag-btn').forEach(btn => {
    btn.classList.remove('active');
  })
  const activeBtn = document.querySelector(`.tag-btn[data-tag="${targetName}"]`);
  if(activeBtn){
    activeBtn.classList.add('active');
    console.log("找到了匹配按钮，加上高亮");
  }else{
    console.log("⚠️ 没有找到匹配的按钮");
  }
}

function getHashTag() {
  const h = window.location.hash.slice(1);
  const res = h ? decodeURIComponent(h) : 'all';
  return res;
}

document.querySelectorAll('.tag-btn').forEach(btn => {
  btn.onclick = () => {
    switchTag(btn.dataset.tag);
  }
})

function init() {
  switchTag(getHashTag());
}
init();
window.addEventListener('hashchange', () => {
  switchTag(getHashTag());
})
</script>
