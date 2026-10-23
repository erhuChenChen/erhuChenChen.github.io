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
const tagBtns = document.querySelectorAll('.tag-btn');
const tagBlocks = document.querySelectorAll('.tag-block');

function switchTag(targetName){
  tagBlocks.forEach(block=>{
    if(targetName === 'all' || block.dataset.group === targetName){
      block.style.display = 'block';
    }else{
      block.style.display = 'none';
    }
  })
}

tagBtns.forEach(btn=>{
  btn.onclick = ()=>{
    switchTag(btn.dataset.tag);
  }
})

document.addEventListener('DOMContentLoaded', ()=>{
  const rawHash = window.location.hash.slice(1);
  if(rawHash){
    const hash = decodeURIComponent(rawHash);
    switchTag(hash);
  }
})
</script>
