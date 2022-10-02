---
title: Books I've read
---

# Books I've read

Reviews of technical or otherwise work related books I've read

{% assign sorted_reviews = site.book_reviews | sort: 'date' | reverse %}
{% include box_items.html collection = sorted_reviews %}