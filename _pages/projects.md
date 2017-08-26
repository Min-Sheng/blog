---
layout: archive
permalink: /projects/
title: "Projects"
author_profile: true
---
<div class="grid__wrapper">
  {% for post in site.current_projects %}
    {% include archive-single.html type="grid" %}
  {% endfor %}
</div>
