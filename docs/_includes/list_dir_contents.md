{% comment %}
    This include file will list, in the following order:
        * an index file labeled `Go up` found in `../`, if this is enabled using the `enable_go_up` parameter
        * any index files found only one folder down
        * any `.md` files found in `.`
{% endcomment %}

<!-- TODO -->
{% assign page_dir = page.dir | remove_first: "/" | split: "/" %}

<!-- TODO -->
{% assign max_nesting = page_dir.size | plus: 1 %}

<!-- TODO -->
{% assign go_up_number = page_dir.size | minus: 1 %}

{% if include.enable_go_up == false %}
    {% assign go_up_enabled = false %}
{% else %}
    {% assign go_up_enabled = true %}
{% endif %}

<!-- TODO -->
{% assign page_list = site.pages | sort: 'url' %}
<ul>
{% for doc in page_list %}
    <!-- TODO -->
    {% assign doc_dir = doc.dir | remove_first: "/" | split: "/" %}

    <!-- List the index file contained one directory above the current file with the text "Go up" (if this is enabled) -->
    {% if doc.name == "index.md" and doc_dir.size == go_up_number and page.dir contains doc.dir and go_up_enabled %}
        <li><a href="{{ site.baseurl }}{{ doc.url }}">Go up</a></li>
    {% endif %}
    
    <!-- List all index files within the maximum nesting, but not the index itself -->
    {% unless doc.path == page.path or doc_dir.size > max_nesting %}
        {% if doc.name == "index.md" and doc.dir contains page.dir %}
                <li><a href="{{ site.baseurl }}{{ doc.url }}">{{ doc.title }}</a></li>
        {% endif %}
    {% endunless %}

    <!-- List all markdown pages in the current dir, but not the index itself -->
    {% if doc.name contains ".md" and doc.dir == page.dir and doc.path != page.path %}
            <li><a href="{{ site.baseurl }}{{ doc.url }}">{{ doc.title }}</a></li>
    {% endif %}

{% endfor %}
</ul>

{% comment %}
    Thanks to [Clement Ong](https://ongclement.com/) for the above [page listing](https://ongclement.com/blog/github-pages-indexing-directory-copy) as it is a very heavily modified version of theirs. Unfortunately I don't know what the original is licensed under. :(. All `index.md` files include the same modified version of the same Clement Ong code but may lack this notice, so consider this as a notice for them.
{% endcomment %}
