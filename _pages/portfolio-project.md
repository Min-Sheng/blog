---
layout: archive
permalink: /portfolio-project/
title: "Projects"
author_profile: true
---
<div class="grid__wrapper">
  {% for post in site.projects %}
    {% include archive-single.html type="grid" %}
  {% endfor %}
</div>
