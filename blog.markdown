---
layout: page
title: Writing
intro: Notes on tools, workflows and the way I work.
permalink: /blog/
---

{%- assign current_year = "" -%}
{%- for post in site.posts -%}
  {%- assign year = post.date | date: "%Y" -%}
  {%- if year != current_year -%}
    {%- unless forloop.first %}</ul>{% endunless %}
<h2 class="year">{{ year }}</h2>
<ul class="post-list">
    {%- assign current_year = year -%}
  {%- endif %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a>
    <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%b %-d" }}</time>
  </li>
  {%- if forloop.last %}
</ul>
  {%- endif -%}
{%- endfor %}
