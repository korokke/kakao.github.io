---
layout: page
title: Date
permalink: /date/
sitemap:
  priority: 0.7
---
{% assign dates = " " | split: ' ' %}
{% for post in site.posts %}
	{% assign dt = post.date | slice: 0, 10 %}
	{% unless dates contains dt %}
		{% assign dta = dt | split: ' ' %}
		{% assign dates = dates | concat: dta %}
	{% endunless %}
{% endfor %}

{% assign dates = dates | sort %}
{% assign lst = "" %}
{% assign prvM = "" %}
{% assign prvY = "" %}
{% for date in dates %}
	{% assign year = date | slice: 0, 4 %}
	{% if prvY == year %}
		{% continue %}
	{% endif %}
	{% assign lst = lst | append: '<ul><li><a href="' | append: site.baseurl | append: "/date/" | append: year | append: '/">' | append: year | append: "</a></li>" %}
	{% for date2 in dates %}
		{% assign month = date2 | slice: 5, 2 %}
		{% if prvM == month %}
			{% continue %}
		{% endif %}
		{% assign year2 = date2 | slice: 0, 4 %}
		{% if year2 == year %}
			{% assign lst = lst | append: '<ul><li><a href="' | append: site.baseurl | append: "/date/" | append: year  | append: "/" | append: month | append: '/">' | append: month | append: "</a></li><ul><li>" %}
		{% endif %}
		{% for date3 in dates %}
			{% assign day = date3 | slice: 8, 2 %}
			{% assign month2 = date3 | slice: 5, 2 %}
			{% assign year3 = date3 | slice: 0, 4 %}
			{% if year3 == year and month2 == month %}
				{% assign lst = lst | append: '<a href="' | append: site.baseurl | append: "/date/" | append: year  | append: "/" | append: month | append: "/" | append: day | append: '/">' | append: day | append: "</a> / " %}
			{% endif %}
		{% endfor %}
		{% assign lst = lst | append: "</li></ul></ul>" %}
		{% assign prvM = month %}
	{% endfor %}
	{% assign lst = lst | append: "</ul>" %}
	{% assign prvY = year %}
{% else %}
	No Contents
{% endfor %}
{{ lst }}

{% comment %}
	{% assign lst = lst | append: "<ul><li>[" | append: year | append: "](" | append: site.baseurl | append: "/date/" | append: year | append: "/)</li>" %}
			{% assign lst = lst | append: "<ul><li>[" | append: month | append: "](" | append: site.baseurl | append: "/date/" | append: year | append: "/" | append: month | append: "/)</li><li>" %}
				{% assign lst = lst | append: "[" | append: day | append: "](" | append: site.baseurl | append: "/date/" | append: year | append: "/" | append: month | append: "/" | append: day | append: "/) " %}
{% endcomment %}
