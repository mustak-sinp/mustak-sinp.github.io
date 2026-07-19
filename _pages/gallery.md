---
layout: page
title: gallery
permalink: /gallery/
description: Moments from conferences, labs, and beamtimes.
nav: true
nav_order: 8
---

<div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3">
{% for file in site.static_files %}
  {% assign ext = file.extname | downcase %}
  {% if file.path contains 'assets/img/gallery/' and (ext == '.jpg' or ext == '.jpeg' or ext == '.png') %}
  <div class="col">
    {% include figure.liquid loading="lazy" path=file.path class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  {% endif %}
{% endfor %}
</div>
