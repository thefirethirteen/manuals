---
title: CD&DVD-info
---

# Contents

{% assign page_dir = page.dir | remove_first: "/" | split: "/" %}
{% assign max_nesting = page_dir.size | plus: 1 %}

{% assign doclist = site.pages | sort: 'url' %}
<ul>
    {% for doc in doclist %}
        {% assign doc_dir = doc.dir | remove_first: "/" | split: "/" %}
        {% unless doc.path == page.path or doc_dir.size > max_nesting %}
            {% if doc.name == "index.md" and doc.dir contains page.dir%}
                    <li><a href="{{ site.baseurl }}{{ doc.url }}">{{ doc.title }}</a></li>
            {% endif %}

            {% if doc.name contains ".md" and doc.dir == page.dir %}
                    <li><a href="{{ site.baseurl }}{{ doc.url }}">{{ doc.title }}</a></li>
            {% endif %}
        {% endunless %}
    {% endfor %}
</ul>
