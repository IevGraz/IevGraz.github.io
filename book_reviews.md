---
title: Books I've read
---

# Books I've read

Reviews of technical or otherwise work related books I've read

{% assign by_year = site.book_reviews | group_by_exp: "r", "r.date | date: '%Y'" | sort: "name" -%}
{%- assign first = by_year.first.name | plus: 0 -%}
{%- assign last = by_year.last.name | plus: 0 -%}
<div class="year-histogram">
{%- for y in (first..last) -%}
{%- assign ys = y | append: "" -%}
{%- assign g = by_year | where: "name", ys | first -%}
{%- assign n = g.size | default: 0 -%}
<div class="bar" style="--n: {{ n }}"><span>{{ n }}</span><small>{{ y }}</small></div>
{%- endfor -%}
</div>

{% assign sorted_reviews = site.book_reviews | sort: 'date' | reverse %}
{% include box_items.html collection = sorted_reviews %}