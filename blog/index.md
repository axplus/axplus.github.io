---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Home
---

# Blog

{% for post in site.posts %}

## {{ post.title }}

{{ post.date | date_to_string }}

{% if post.description %}
{{ post.description | strip_html | truncate: 200 }}
{% else %}
{{ post.content | strip_html | truncate: 200 }}
{% endif %}

[阅读全文 &raquo;]({{ post.url | relative_url }})

---

{% endfor %}

{% if site.posts.size > 5 %}
{% if paginator.next_page %}
[更早的文章]({{ paginator.next_page_path | relative_url }})
{% else %}
更早的文章
{% endif %}
|
{% if paginator.previous_page %}
[最新文章]({{ paginator.previous_page_path | relative_url }})
{% else %}
最新文章
{% endif %}
{% endif %}
