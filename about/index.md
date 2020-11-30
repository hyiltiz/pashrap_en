---
layout: page
title: Pashrap's Articles
comments: yes
---


[**Pregnancy in Puerto Rico: Protecting the Health of Women and Children by Reducing Metal Exposures**](https://sph.umich.edu/pursuit/2020posts/protecting-the-health-of-women-and-children-by-reducing-metal-exposures.html), by Pahriya Ashrap on [The Pursuit](https://sph.umich.edu/pursuit/)

[**Silk Road Native’s Dream Repeats with Every Intervention**](https://sph.umich.edu/stories/2019posts/pahriya-ashrap.html), a story about Pahriya on [WE ARE MICHIGAN PUBLIC HEALTH](https://sph.umich.edu/stories/), *Published: June 24, 2019*.

[**Trash to Treasure: The Incredible Benefits of Composting**](https://sph.umich.edu/pursuit/2019posts/benefits-of-composting.html). a conversation about composting by Pahriya Ashrap and Amber Cathey on [The Pursuit](https://sph.umich.edu/pursuit/), *Published: September 19, 2019*.

[**Student Spotlight - Pahriya Ashrap**](https://lsa.umich.edu/eli/news-events/all-news/studentspotlightapr20.html), English Language Institute Student Spotlight series.*Published: April 10, 2020*.

[**PROTECT Study finds predictors of metals exposures which contribute to higher toxicity levels amongst Puerto Rican Women compared to US Population**](https://web.northeastern.edu/protect/protect-study-finds-predictors-of-metals-exposures-which-contribute-to-higher-toxicity-levels-amongst-puerto-rican-women-compared-to-us-population/), *Published: November 19, 2020*.

[**PROTECT Study finds that among metals, maternal blood lead concentrations were strongly associated with increased risk of preterm birth**](https://web.northeastern.edu/protect/protect-study-finds-that-among-metals-maternal-blood-lead-concentrations-were-strongly-associated-with-increased-risk-of-preterm-birth/)*Published: May 11, 2020*.

[**PROTECT Study Finds Decrease in Phthalate Exposure Coincides with Increase in Phthalate Replacement Chemicals in PROTECT Cohort**](https://web.northeastern.edu/protect/protect-study-finds-decrease-in-phthalate-exposure-coincides-with-increase-in-phthalate-replacement-chemicals-in-protect-cohort/)*Published: May 6, 2020*.










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
