---
layout: archive
title: "Publications"
permalink: /publications/
author_profile: true
---

You can find a list of my publications on <u><a href="https://scholar.google.com/citations?user=EW1iZEMAAAAJ">my Google Scholar profile</a>.</u>

{% include base_path %}

{% for post in site.publications reversed %}
  {% include archive-single.html %}
{% endfor %}
