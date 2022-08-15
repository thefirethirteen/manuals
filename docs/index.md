---
title: Manuals homepage
---

# Index

{% assign doclist = site.pages | sort: 'url'  %}
<ul>
   {% for doc in doclist %}
        {% if doc.name == "index.md" and doc.path != page.path %}
            <li><a href="{{ site.baseurl }}{{ doc.url }}">{{ doc.name }}</a></li>
        {% endif %}
    {% endfor %}
</ul>
