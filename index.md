---
layout: default
---

{% for post in site.posts limit 10 %}
<li>
    {{ post.date | date_to_string }}
    <b">{{ post.title }}</b>
</li>
<p>{{ post.content | strip_html | truncatewords:30}}</p>
<a href="{{ post.url }}">Read more...</a>
{% endfor %}
