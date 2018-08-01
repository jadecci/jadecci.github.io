---
layout: default
---

<b>Latest Notes: </b>

{% for post in site.posts limit 10 %}
<li>
    {{ post.date | date_to_string }}
    <a href="{{ post.url }}"> <b>{{ post.title }}</b> </a>
    <p>{{ post.excerpt }}</p>
</li>
{% endfor %}
