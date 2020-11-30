---
title: Pashrap's Articles
layout: page
---

<ul class="listing">. #ignoreline
{% for post in site.posts %} #ignoreline
  {% capture y %}{{post.date | date:"%Y"}}{% endcapture %} #ignoreline
  {% if year != y %} #ignoreline
    {% assign year = y %} #ignoreline
    <li class="listing-seperator">{{ y }}</li> #ignoreline
  {% endif %} #ignoreline
  <li class="listing-item"> #ignoreline
    <time datetime="{{ post.date | date:"%Y-%m-%d" }}">{{ post.date | date:"%Y-%m-%d" }}</time> #ignoreline
    <a href="{{ site.url }}{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a> #ignoreline
  </li> #ignoreline
{% endfor %} #ignoreline
</ul> #ignoreline
