---
layout: default
title: 全部文章
permalink: /articles/
description: i小火箭 · Shadowrocket 使用与账号攻略全部文章
---

<h1>全部文章</h1>
<div class="post-list">
  {% assign latest = site.posts | reverse %}
  {% for post in latest %}
    <article class="post-row">
      <time>{{ post.date | date: '%Y-%m-%d' }}</time>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p>{{ post.description }}</p>
    </article>
  {% endfor %}
</div>
