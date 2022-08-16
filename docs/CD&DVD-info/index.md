---
title: CD&DVD-info
---

# Contents

{% assign doclist = site.pages | sort: 'url'  %}
 <ul>
    {% for doc in doclist %}
         {% if doc.name contains ".md" and doc.dir == page.dir and doc.path != page.path %}
             <li><a href="{{ site.baseurl }}{{ doc.title }}">{{ doc.name }}</a></li>
         {% endif %}
     {% endfor %}
 </ul>
