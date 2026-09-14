---
title: Online Hosted Instructions
permalink: index.html
layout: home
---

This page lists lab exercises associated with the Microsoft skilling course [MS-4004: Empower your workforce with Microsoft 365 Copilot Use Cases](https://learn.microsoft.com/en-us/training/courses/ms-4004) on [Microsoft Learn](https://learn.microsoft.com).

<hr>

## Labs

### Index {#index}

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 20px; margin-bottom: 30px;">

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" | where_exp:"page", "page.lab.title" | sort: "url" -%}
{% assign modules = "" | split: "" -%}
{% assign module_names = "" | split: "" -%}
{% for activity in labs -%}
{% assign relative_url = activity.url | remove: "/Instructions/Labs/" -%}
{% assign module_folder = relative_url | split: "/" | first -%}
{% if modules contains module_folder -%}
{% else -%}
{% assign modules = modules | push: module_folder -%}
{% endif -%}
{% endfor %}

{% for module_folder in modules -%}
{% assign module_num = module_folder | slice: 0, 3 -%}
{% assign words = module_folder | slice: 4, 200 | split: "-" -%}
{% assign module_desc = "" -%}
{% for word in words -%}
{% if word == "it" or word == "hr" -%}
{% assign word_display = word | upcase -%}
{% else -%}
{% assign word_display = word | capitalize -%}
{% endif -%}
{% assign module_desc = module_desc | append: word_display | append: " " -%}
{% endfor -%}
{% assign module_desc = module_desc | strip -%}
- [{{ module_num }}: {{ module_desc }}](#{{ module_folder }})
{% endfor %}

</div>

{% assign current_module = "" -%}
{% for activity in labs -%}
{% assign relative_url = activity.url | remove: "/Instructions/Labs/" -%}
{% assign module_folder = relative_url | split: "/" | first -%}
{% if module_folder != current_module -%}
{% assign current_module = module_folder -%}
{% assign module_num = module_folder | slice: 0, 3 -%}
{% assign words = module_folder | slice: 4, 200 | split: "-" -%}
{% assign module_desc = "" -%}
{% for word in words -%}
{% if word == "it" or word == "hr" -%}
{% assign word_display = word | upcase -%}
{% else -%}
{% assign word_display = word | capitalize -%}
{% endif -%}
{% assign module_desc = module_desc | append: word_display | append: " " -%}
{% endfor -%}
{% assign module_desc = module_desc | strip -%}
{% assign total_duration = 0 -%}
{% for p in labs -%}
{% assign p_rel = p.url | remove: "/Instructions/Labs/" -%}
{% assign p_mod = p_rel | split: "/" | first -%}
{% if p_mod == module_folder -%}
{% assign d = p.lab.duration | split: " " | first | plus: 0 -%}
{% assign total_duration = total_duration | plus: d -%}
{% endif -%}
{% endfor %}

### {{ module_num }}: {{ module_desc }} ({{ total_duration }} min) {#{{ module_folder }}}

[Back to Index](#index)

| Lab | Level | Duration |
| --- | --- | --- |
{% endif -%}
| [{{ activity.lab.title }}{% if activity.lab.type %} - {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) | {{ activity.lab.level }} | {{ activity.lab.duration }} |
{% endfor %}
