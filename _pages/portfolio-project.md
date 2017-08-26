---
layout: archive
permalink: /portfolio-project/
title: "Projects"
author_profile: true
---
<div class="grid__wrapper">
  {% for project in site.projects %}
    {% include project-single.html type="grid" %}
  {% endfor %}
</div>
