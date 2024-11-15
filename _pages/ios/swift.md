---
title: "🍎 ios / swift"
layout: category
permalink: /ios/swift/
author_profile: true
sidebar_main: true
types: posts
taxonomy:
sidebar:
  nav: "sidebar-category"
  enabled: true
---

{% assign posts_with_ios = site.posts | where: "categories", "ios" %}
{% assign posts_with_ios_and_swift = posts_with_ios | where: "categories", "swift" %}

{% for post in posts_with_ios_and_swift %}
{% include archive-single.html type=page.entries_layout %}
{% endfor %}