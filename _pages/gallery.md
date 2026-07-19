---
layout: page
title: gallery
permalink: /gallery/
description: Moments from conferences, labs, and beamtimes.
nav: true
nav_order: 8
---

{% assign gallery_files = site.static_files | where_exp: "file", "file.path contains 'assets/img/gallery/'" %}

{% comment %} Collect unique subfolder names {% endcomment %}
{% assign folders = "" | split: "" %}
{% for file in gallery_files %}
  {% assign rel = file.path | split: "assets/img/gallery/" | last %}
  {% assign segs = rel | split: "/" %}
  {% if segs.size == 2 %}
    {% assign folders = folders | push: segs[0] %}
  {% endif %}
{% endfor %}
{% assign folders = folders | uniq | sort | reverse %}

{% for folder in folders %}
<h2 class="mt-4">{{ folder | replace: "_", " " }}</h2>
<div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3">
  {% for file in gallery_files %}
    {% assign ext = file.extname | downcase %}
    {% assign folder_path = folder | prepend: "assets/img/gallery/" | append: "/" %}
    {% if file.path contains folder_path and (ext == '.jpg' or ext == '.jpeg' or ext == '.png') %}
  <div class="col">
    {% include figure.liquid loading="lazy" path=file.path class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
    {% endif %}
  {% endfor %}
</div>
{% endfor %}
