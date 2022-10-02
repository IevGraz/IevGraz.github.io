---
title: I watch
---
# Things I've watched

Reviews of technical or otherwise work related courses or conferences

{% assign sorted_reviews = site.reviews | sort: 'date' | reverse %}
{% include box_items.html collection = sorted_reviews %}