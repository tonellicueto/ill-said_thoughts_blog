---
layout: page
title: Tags
permalink: /tags/
---
{% comment%}
Here we generate all the categories.
{% endcomment%}

{% assign rawcats = "" %}
{% for post in site.posts %}
{% assign tcats = post.category | join:'|' | append:'|' %}
{% assign rawcats = rawcats | append:tcats %}
{% endfor %}

{% assign rawcats = rawcats | split:'|' | sort %}

{% assign cats = "" %}

{% for cat in rawcats %}
{% if cat != "" %}

{% if cats == "" %}
{% assign cats = cat | split:'|' %}
{% endif %}

{% unless cats contains cat %}
{% assign cats = cats | join:'|' | append:'|' | append:cat | split:'|' %}
{% endunless %}
{% endif %}
{% endfor %}



{% for ct in cats %}
[{{ ct }}](#{{ ct | slugify }})
{% endfor %}

{% for ct in cats %}
## {{ ct }}
{% for post in site.posts %}
{% if post.category contains ct %}
* [{{ post.title }}]({{ post.url }}) {{ post.date | date_to_string }}
{% for ct in post.category %}
[{{ ct }}](#{{ ct | slugify }})
{% endfor %}
{% endif %}
{% endfor %}
{% endfor %}
