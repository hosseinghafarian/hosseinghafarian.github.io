---
layout: page
title: slides
permalink: /slides/
nav: true
nav_order: 2
---

<!-- This page lists items from the _slides collection -->

{% assign slides = site.slides | sort: "date" | reverse %}
<h1>{{ page.title }}</h1>

{% if slides and slides.size > 0 %}
  <ul class="slides-list" style="list-style:none;padding-left:0;">
  {% for s in slides %}
    <li style="margin-bottom:1.2rem;">
      <h2 style="margin:0; font-size:1.05rem;">
        {% if s.url %}
          <a href="{{ s.url }}">{{ s.title }}</a>
        {% else %}
          {{ s.title }}
        {% endif %}
      </h2>
      {{ s.content | markdownify }}
      <p style="margin:.2rem 0 .4rem; color:#6c757d; font-size:.95rem;">
        {{ s.date | date: "%B %d, %Y" }}
        {% if s.event %} — {{ s.event }}{% endif %}
      </p>

      {% if s.slides_url %}
        <p style="margin:.2rem 0;">
          <a href="{{ s.slides_url }}" rel="noopener" target="_blank">Download slides</a>
          {% if s.notes or s.description %} — {{ s.description | default: s.notes }}{% endif %}
        </p>
      {% elsif s.url %}
        <p style="margin:.2rem 0;">
          <a href="{{ s.url }}" rel="noopener" target="_blank">Open</a>
        </p>
      {% endif %}
      {% if s.slides_url %}
        <div class="ratio ratio-16x9 mt-3">
          <iframe
            src="{{ s.slides_url }}#view=FitH"
            width="100%"
            height="600"
            style="border:1px solid #ccc; border-radius:10px;"
            allowfullscreen>
          </iframe>
        </div>
        <p class="mt-2">
          <a href="{{ s.slides_url }}" target="_blank">Open full screen ↗</a>
        </p>
      {% endif %}
    </li>
    <hr class="my-4">
  {% endfor %}
  </ul>
{% else %}
  <p>No slides added yet. Add files to <code>_slides/</code> with YAML front matter.</p>
{% endif %}
