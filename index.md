---
layout: default
---

<b>Latest Notes: </b>

<ul class="no-bullets"> 
    {% for post in site.posts limit: 10 %}
    <li>
        <a href="{{ post.url }}"> <b>{{ post.title }}</b> </a>
        [{{ post.date | date_to_string }}]
        <p>{{ post.excerpt }}</p>
        <hr class="dotted">
    </li>
    {% endfor %}
</ul>
