---
layout: default
title: 分类
permalink: /categories/
description: i小火箭 · Shadowrocket 文章分类导航
---

<section class="page-hero">
  <h1>🗂️ 文章分类</h1>
  <p>按主题浏览 Shadowrocket 相关的全部文章。</p>
</section>

<div class="cat-grid cat-grid-large">
  {% for cat in site.categories %}
  {% assign cat_name = cat[0] %}
  {% if cat_name != "categories" %}
  <a class="cat-card" href="{% include cat_url.html cat=cat_name %}">
    <span class="cat-name">{{ cat_name }}</span>
    <span class="cat-count">{{ cat[1] | size }} 篇</span>
  </a>
  {% endif %}
  {% endfor %}
</div>
