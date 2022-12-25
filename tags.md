---
layout: page
permalink: /tags/
title: Tags
---

{% assign allPosts = site.documents %}
{% assign allPages = site.pages %}
{% assign postTags = allPosts | map: 'categories' | join: ','  | split: ','  | group_by: categories %}
{% assign pageTags = allPages | map: 'categories' | join: ','  | split: ','  | group_by: categories %}

<ul class="cloud">
    {%- for tag in postTags -%}
        {% if tag.name != "" %}
            <a href="{{ site.baseurl }}/tags/{{ tag.name }}" data-weight="{{ tag.size }}">{{ tag.name }}({{ tag.size}})</a>
        {% endif %}
    {%- endfor -%}
    {%- for tag in pageTags -%}
        {% if tag.name != "" %}
            <a href="{{ site.baseurl }}/tags/{{ tag.name }}" data-weight="{{ tag.size }}">{{ tag.name }}({{ tag.size}})</a>
        {% endif %}
    {%- endfor -%}
</ul>