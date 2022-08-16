---
title: Manuals Main Page
---

# Browse manuals

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


Thanks to [Clement Ong](https://ongclement.com/) for the [above](https://ongclement.com/blog/github-pages-indexing-directory-copy) page listing as it is a heavily modified version of theirs. Unfortunately I don't know what the original is licensed under. :(. All other `index.md` files contain simmilarly modified versions of the same Clement Ong code but lack this notice, so consider this as a notice for those also.
