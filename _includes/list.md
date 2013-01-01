{% for page in site.pages %}
{% if page.repository == repository and page.branch == branch %}
+ [{{page.repository}}/{{page.branch}} {{ page.title }}]({{ page.url }})
{% endif %}
{% endfor %}
