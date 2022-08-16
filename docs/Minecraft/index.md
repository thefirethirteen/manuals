---
title: Minecraft
---

# Contents

{% assign doclist = site.pages | sort: 'url' %}
<ul>
    {% for doc in doclist %}
        {% unless doc.path == page.path %}
            {% if doc.name == "index.md" %}
                    <li><a href="{{ site.baseurl }}{{ doc.url }}">{{ doc.title }}</a></li>
            {% endif %}

            {% if doc.name contains ".md" and doc.dir == page.dir %}
                    <li><a href="{{ site.baseurl }}{{ doc.url }}">{{ doc.title }}</a></li>
            {% endif %}
        {% endunless %}
    {% endfor %}
</ul>

