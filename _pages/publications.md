---
layout: page
permalink: /publications/
title: Publications
nav: true
nav_order: 1
---

<div class="publications">

{%- assign years = site.bibliography | group_by_exp:"item", "item.year" | sort: "name" | reverse -%}
{%- for year_group in years -%}
  <h2 class="year">{{ year_group.name }}</h2>
  {% bibliography -f {{ site.scholar.bibliography }} -q @*[year={{ year_group.name }}]* %}
{%- endfor -%}

</div>
