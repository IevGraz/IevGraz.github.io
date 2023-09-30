---
title: I attend
---
# Conferences I've attended

And the impressions they left me.

{% assign sorted_conferences = site.conferences | sort: 'date' | reverse %}
{% include box_items.html collection = sorted_conferences %}