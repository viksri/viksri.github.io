---
layout: page
permalink: /tags/
title: Tags
---

{% assign alldocs = site.documents %}
{% assign grouptag =  alldocs | map: 'categories' | join: ','  | split: ','  | group_by: categories %}

<ul>
{%- for tag in grouptag -%}
<p class="btn">{{- tag.name -}}: {{tag.size}}</p>

    <ul>
        {%- for document in alldocs -%}
            {% if document.categories contains tag.name %}
            <li>
                <a href="{{ site.baseurl }}{{ document.url }}"> {{ document.title }}</a>
            </li>
            {% endif %}
        {%- endfor -%}
    </ul>

{%- endfor -%}
</ul>