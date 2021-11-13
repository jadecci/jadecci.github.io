---
layout: default
---

<b>Notes on < Numerical Recipes in C > (relevent code are available at [my Github repository](https://github.com/jadecci/numerical_recipes_c)): </b>

<ul class="no-bullets"> 
    {% for post in site.tags.Numerical-Recipes-in-C %}
    <li>
        <a href="{{ post.url }}"> <b>{{ post.title }}</b> </a>
        [{{ post.date | date_to_string }}]
        <p>{{ post.excerpt }}</p>
        <hr class="dotted">
    </li>
    {% endfor %}
</ul>

