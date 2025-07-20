---
layout: home
title: Mi blog
---

Bienvenido a mi blog


<h1>Entradas del blog</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a> - {{ post.date | date: "%d/%m/%Y" }}
    </li>
  {% endfor %}
</ul>
