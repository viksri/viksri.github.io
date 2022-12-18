---
layout: page
permalink: /categories/
title: Categories
---


<ul id="categories">
{% for category in site.categories %}
  <li class="category-list">
    {% capture category_name %}{{ category | first }}{% endcapture %}
    <div id="#{{ category_name | slugize }}"></div>

    <h3>{{ category_name }}</h3>
    <a name="{{ category_name | slugize }}"></a>
    <ul class="category-post-list">
    {% for post in site.categories[category_name] %}
    <article>
      <li>
      <a href="{{ site.baseurl }}{{ post.url }}">{{post.title}}</a>
      </li>
    </article>
    {% endfor %}
    </ul>
  </li>
{% endfor %}
</ul>
