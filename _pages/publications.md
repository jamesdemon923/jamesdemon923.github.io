---
layout: page
permalink: /publications/
title: publications
nav: true
nav_order: 1
---

<p style="font-size: 0.85rem; color: var(--global-text-color-light); margin-bottom: 1rem; margin-top: -1.5rem;">* Equal contribution</p>

<div class="publications">
<h2 class="year">2026</h2>
{% bibliography -f papers.bib -q @*[year=2026]* %}

<h2 class="year">2025</h2>

{% bibliography -f papers.bib -q @*[year=2025]* %}

</div>
