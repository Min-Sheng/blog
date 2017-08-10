---
layout: archive
permalink: /portfolio-archive/
title: "Portfolio"
author_profile: true
---
<div class="grid__wrapper">
  {% for post in site.posts %}
    {% include archive-single.html type="grid" %}
    {% assign currentDate = post.date | date: "%Y" %}
    {% if currentDate != myDate %}
        {% unless forloop.first %}</ul>{% endunless %}
        <h1>{{ currentDate }}</h1>
        <ul>
        {% assign myDate = currentDate %}
     {% endif %}
     <li><a href="{{ post.url }}"><span>{{ post.date | date: "%B %-d, %Y" }}</span> - {{ post.title }}</a></li>
     {% if forloop.last %}</ul>{% endif %}
  {% endfor %}
</div>

