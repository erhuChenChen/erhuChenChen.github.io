---
layout: default
title: 标签
permalink: /tags/
---

{% assign tags = site.tags | sort %}
<div style="display:flex;flex-wrap:wrap;gap:12px;">
{% for tag in tags %}
<a href="javascript:showTag('{{ tag[0] | slugify }}')" style="font-style:italic;">{{ tag[0] }} {{ tag[1].size }}</a>
{% endfor %}
<a href="javascript:showAll()" style="font-style:italic;">查看全部</a>
</div>

<hr>

{% for tag in tags %}
<div class="tag-group" id="tag-{{ tag[0] | slugify }}">
  <h3 style="font-style:italic;">{{ tag[0] }} {{ tag[1].size }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li><a href="{{ post.url }}">{{ post.title }}</a> <small>{{ post.date | date: "%Y-%m-%d" }}</small></li>
    {% endfor %}
  </ul>
</div>
{% endfor %}

<script>
function showTag(id){
  document.querySelectorAll('.tag-group').forEach(el=>el.style.display='none');
  document.getElementById('tag-'+id).style.display='block';
  window.scrollTo({top:0,behavior:'smooth'});
}
function showAll(){
  document.querySelectorAll('.tag-group').forEach(el=>el.style.display='block');
}
document.addEventListener('DOMContentLoaded', function(){
  const hash = window.location.hash.replace('#','');
  if(hash) showTag(hash);
})
</script>
