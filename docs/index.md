---
title: Manuals Main Page
---

# Browse manuals

{% assign doclist = site.pages | sort: 'url' %}
<ul>
    {% for doc in doclist %}
        {% if doc.name == "index.md" and doc.path != page.path %}
            {% unless doc.path == page.path %}
                <li><a href="{{ site.baseurl }}{{ doc.url }}">{{ doc.title }}</a></li>
            {% endunless %}
        {% endif %}
    {% endfor %}
</ul>

Thanks to [Clement Ong](https://ongclement.com/) for the [above](https://ongclement.com/blog/github-pages-indexing-directory-copy) page listing as it is a modified version of theirs. Unfortunately I don't know what the original is licensed under. :(. Other `index.md` files may contain modified versions of the same Clement Ong code but lack this notice, so consider this as a notice for those also.
