---
layout: default
---

<ul class="no-bullets"> 
    {% for post in site.posts %}
    <li>
        <a href="{{ post.url }}"> <b>{{ post.title }}</b> </a>
        [{{ post.date | date_to_string }}]
        <p>{{ post.excerpt }}</p>
        <hr class="dotted">
    </li>
    {% endfor %}
</ul>

