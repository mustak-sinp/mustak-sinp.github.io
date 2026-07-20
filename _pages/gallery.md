---
layout: page
title: gallery
permalink: /gallery/
description: Around the world with nuclear physics...
nav: true
nav_order: 8
---

{% assign gallery_files = site.static_files | where_exp: "file", "file.path contains 'assets/img/gallery/'" %}

{% comment %}
  Custom album titles. Format: folder_name:Display Title
  Separate entries with a semicolon. Albums not listed here fall back
  to the automatic name (folder minus year, underscores as spaces).
{% endcomment %}
{% assign label_overrides = "2026_IIT_ISM_Dhanbad:Dhanbad" | split: ";" %}

{% assign folders = "" | split: "" %}
{% for file in gallery_files %}
  {% assign rel = file.path | split: "assets/img/gallery/" | last %}
  {% assign segs = rel | split: "/" %}
  {% if segs.size == 2 %}
    {% assign folders = folders | push: segs[0] %}
  {% endif %}
{% endfor %}
{% assign folders = folders | uniq | sort | reverse %}

<!-- Album index: one card per folder -->
<div id="album-index" class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3">
{% for folder in folders %}
  {% assign folder_path = folder | prepend: "assets/img/gallery/" | append: "/" %}
  {% assign count = 0 %}
  {% assign thumb = "" %}
  {% for file in gallery_files %}
    {% assign ext = file.extname | downcase %}
    {% if file.path contains folder_path and (ext == '.jpg' or ext == '.jpeg' or ext == '.png') %}
      {% assign count = count | plus: 1 %}
      {% if thumb == "" %}{% assign thumb = file.path %}{% endif %}
    {% endif %}
  {% endfor %}
  {% if count > 0 %}
  {% assign yr = folder | split: "_" | first %}
  {% assign label = folder | remove_first: yr | remove_first: "_" | replace: "_", " " %}
  {% for override in label_overrides %}
    {% assign pair = override | split: ":" %}
    {% if pair[0] == folder %}{% assign label = pair[1] %}{% endif %}
  {% endfor %}
  <div class="col">
    <a href="#{{ folder }}" class="album-card card h-100" data-album="{{ folder }}" style="text-decoration: none;">
      <img src="{{ thumb | relative_url }}" class="card-img-top" style="height: 220px; object-fit: cover;" alt="{{ label }}">
      <div class="card-body">
        <h5 class="card-title mb-1">{{ label }}</h5>
      </div>
    </a>
  </div>
  {% endif %}
{% endfor %}
</div>

<!-- One hidden section per album -->
{% for folder in folders %}
{% assign yr = folder | split: "_" | first %}
{% assign label = folder | remove_first: yr | remove_first: "_" | replace: "_", " " %}
{% for override in label_overrides %}
  {% assign pair = override | split: ":" %}
  {% if pair[0] == folder %}{% assign label = pair[1] %}{% endif %}
{% endfor %}
<div class="album-section" id="album-{{ folder }}" style="display: none;">
  <p><a href="#" class="back-link">&larr; back to albums</a></p>
  <h2>{{ label }}</h2>
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
</div>
{% endfor %}

<style>
  /* Uniform thumbnails inside album photo grids */
  .album-section .row .col img {
    aspect-ratio: 4 / 3;
    object-fit: cover;
    width: 100%;
    height: auto;
  }
</style>

<script>
  function openAlbum(name) {
    document.getElementById('album-index').style.display = 'none';
    document.querySelectorAll('.album-section').forEach(function(s) { s.style.display = 'none'; });
    var target = document.getElementById('album-' + name);
    if (target) { target.style.display = 'block'; }
  }
  function showIndex() {
    document.querySelectorAll('.album-section').forEach(function(s) { s.style.display = 'none'; });
    document.getElementById('album-index').style.display = '';
  }
  document.querySelectorAll('.album-card').forEach(function(card) {
    card.addEventListener('click', function(e) {
      e.preventDefault();
      var name = card.getAttribute('data-album');
      history.pushState(null, '', '#' + name);
      openAlbum(name);
      window.scrollTo(0, 0);
    });
  });
  document.querySelectorAll('.back-link').forEach(function(link) {
    link.addEventListener('click', function(e) {
      e.preventDefault();
      history.pushState(null, '', window.location.pathname);
      showIndex();
      window.scrollTo(0, 0);
    });
  });
  window.addEventListener('popstate', function() {
    var h = window.location.hash.replace('#', '');
    if (h) { openAlbum(h); } else { showIndex(); }
  });
  (function() {
    var h = window.location.hash.replace('#', '');
    if (h) { openAlbum(h); }
  })();
</script>
