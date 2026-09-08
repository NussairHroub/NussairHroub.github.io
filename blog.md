---
layout: page
title: Blog
permalink: /blog/
description: Notes on research, engineering, and competitive programming.
---

{% if site.posts.size > 0 %}
<ul style="margin:0 0 20px;">
{% for post in site.posts %}
  <li style="margin:0 0 10px;">
    <a href="{{ post.url | relative_url }}"><autocolor><strong>{{ post.title }}</strong></autocolor></a><br />
    <small>{{ post.date | date: "%b %-d, %Y" }}</small>
    {% if post.description %}<br />{{ post.description }}{% endif %}
  </li>
{% endfor %}
</ul>
{% else %}
<p>No posts yet.</p>
{% endif %}
