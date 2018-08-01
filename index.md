---
layout: default
---

<b>My Notes: </b>

{% for post in site.posts limit 10 %}
<li>
    {{ post.date | date_to_string }}
    <b>{{ post.title }}</b>
    <a href="{{ post.url }}">   Read more...</a>
</li>
{% endfor %}
