{% comment %}
    This include file will list, in the following order:
        * an index file labeled `Go up` found in `../`, if this is enabled using the `enable_go_up` parameter
        * any `.md` files found in `.`
        * any index files found only one folder down
{% endcomment %}

<!-- TODO -->
{% assign page_dir = page.dir | remove_first: "/" | split: "/" %}

<!-- TODO -->
{% assign max_nesting = page_dir.size | plus: 1 %}

<!-- TODO -->
{% assign go_up_number = page_dir.size | minus: 1 %}

{% if include.enable_go_up == false %}
    {% assign enable_go_up = false %}
{% else %}
    {% assign enable_go_up = true %}
{% endif %}

<!-- TODO -->
{% assign page_list = site.pages | sort: 'url' %}
<ul>
{% for doc in page_list %}
    <!-- TODO -->
    {% assign doc_dir = doc.dir | remove_first: "/" | split: "/" %}

    {% if doc.name == "index.md" and doc_dir.size == go_up_number and page.dir contains doc.dir and enable_go_up %}
        <li><a href="{{ site.baseurl }}{{ doc.url }}">Go up</a></li>
    {% endif %}

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
