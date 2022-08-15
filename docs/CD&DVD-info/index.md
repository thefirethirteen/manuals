---
title: CD&DVD-info
---

   {% assign doclist = site.pages | sort: 'url'  %}
    <ul>
       {% for doc in doclist %}
            {% if doc.name == ".md" and doc.dir == page.dir %}
                <li><a href="{{ site.baseurl }}{{ doc.url }}">{{ doc.url }}</a></li>
            {% endif %}
        {% endfor %}
    </ul>
