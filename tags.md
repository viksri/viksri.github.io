---
layout: page
permalink: /tags/
title: Tags
categories: uncategorized
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

<!-- <ul>
    {%- for tag in postTags -%}
        <p class="btn">{{ tag.name }}({{ tag.size}})</p>
        <ul>
        {%- for document in allPosts -%}
            {% if document.categories contains tag.name %}
                {% if tag.name != "" %}
                <li>
                    <a href="{{ site.baseurl }}{{ document.url }}"> {{ document.title }}</a>
                </li>
                {% endif %}
            {% endif %}
        {%- endfor -%}
        </ul>
    {%- endfor -%}
    {%- for tag in pageTags -%}
        {% if tag.name != "" %}
            <p class="btn">{{ tag.name }}({{ tag.size}})</p>
        {% endif %}
    <ul>
        {%- for document in allPages -%}
        {% if document.categories contains tag.name %}
        {% if tag.name != "" %}
        <li>
            <a href="{{ site.baseurl }}{{ document.url }}"> {{ document.title }}</a>
        </li>
        {% endif %}
    {% endif %}
    {%- endfor -%}
</ul>
{%- endfor -%}
</ul> -->