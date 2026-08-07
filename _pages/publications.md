---
layout: page
permalink: /publications/
title: publications
description: Journal publications, conference proceedings, and newsletters.
nav: true
nav_order: 3
---

{% include bib_search.liquid %}

<div class="publications">

  <!-- 1. Journal Publications -->
  <details class="pub-category">
    <summary><strong>Journal Publications</strong></summary>

    <div class="mt-3">
      {% bibliography --query @article %}
    </div>
  </details>


  <!-- 2. Conference Proceedings -->
  <details class="pub-category">
    <summary><strong>Conference Proceedings</strong></summary>

    <div class="mt-3">
      {% bibliography --query @inproceedings %}
    </div>
  </details>


  <!-- 3. Newsletters -->
  <details class="pub-category">
    <summary><strong>Newsletters</strong></summary>

    <div class="mt-3">
      {% bibliography --query @misc %}
    </div>
  </details>

</div>
