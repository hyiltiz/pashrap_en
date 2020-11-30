---
layout: page
title: Pashrap's Articles
comments: yes
---
Tung, MT., **Ashrap, P.**, Watkins, DJ., Mukherjee, B., Rosario, Z., Vélez-Vega, CM., Alshawabkeh, A., Cordero, JF., Meeker, JD., 2020. Maternal lipidomic profiling of pregnancy outcomes reveals unique lipid signatures for spontaneous preterm birth and large-for-gestational age neonates. (in preparation).

**[Silk Road Native’s Dream Repeats with Every Intervention**](https://sph.umich.edu/stories/2019posts/pahriya-ashrap.html), a story about Pahriya on [WE ARE MICHIGAN PUBLIC HEALTH](https://sph.umich.edu/stories/).

**[Trash to Treasure: The Incredible Benefits of Composting**](https://sph.umich.edu/pursuit/2019posts/benefits-of-composting.html). a conversation about composting on [The Pursuit](https://sph.umich.edu/pursuit/)

https://lsa.umich.edu/eli/news-events/all-news/studentspotlightapr20.html
https://web.northeastern.edu/protect/protect-study-finds-predictors-of-metals-exposures-which-contribute-to-higher-toxicity-levels-amongst-puerto-rican-women-compared-to-us-population/
https://web.northeastern.edu/protect/protect-study-finds-that-among-metals-maternal-blood-lead-concentrations-were-strongly-associated-with-increased-risk-of-preterm-birth/
https://web.northeastern.edu/protect/protect-study-finds-decrease-in-phthalate-exposure-coincides-with-increase-in-phthalate-replacement-chemicals-in-protect-cohort/










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
