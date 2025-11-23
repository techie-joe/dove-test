---
title: Unsupported Liquid Syntaxes
description: Unsupported Liquid syntaxes on this site.
---
{% capture nav_liquid %}{% include_relative nav_liquid.md %}{% endcapture %}
<nav>{{ nav_liquid | markdownify }}<hr/></nav>

# {{ page.title }}

###### json objects ?

> Will these work ?

{%- assign arrays  = [ "pen", 0.9, true ] %}
{%- assign values  = [ "key" => "value" ] %}
{%- assign objects = { "key" :  "value" } %}

```yml
arrays   : {{ arrays  | jsonify }} [{{ arrays  | size | append: ' items' }}]
values   : {{ values  | jsonify }} [{{ values  | size | append: ' items' }}]
objects  : {{ objects | jsonify }} [{{ objects | size | append: ' items' }}]
```

{%- assign arrays  = [ "pen", 0.9, true ] | parse_json %}
{%- assign values  = [ "key" => "value" ] | parse_json %}
{%- assign objects = { "key" :  "value" } | parse_json %}

```yml
arrays   : {{ arrays  | jsonify }} [{{ arrays  | size | append: ' items' }}]
values   : {{ values  | jsonify }} [{{ values  | size | append: ' items' }}]
objects  : {{ objects | jsonify }} [{{ objects | size | append: ' items' }}]
```

{%- assign arrays  = '[ "pen", 0.9, true ]' | parse_json %}
{%- assign values  = '[ "key" => "value" ]' | parse_json %}
{%- assign objects = '{ "key" :  "value" }' | parse_json %}

```yml
arrays   : {{ arrays  | jsonify }} [{{ arrays  | size | append: ' items' }}]
values   : {{ values  | jsonify }} [{{ values  | size | append: ' items' }}]
objects  : {{ objects | jsonify }} [{{ objects | size | append: ' items' }}]
```

{%- assign arrays  = '[ "pen", 0.9, true ]' | jsonify %}
{%- assign values  = '[ "key" => "value" ]' | jsonify %}
{%- assign objects = '{ "key" :  "value" }' | jsonify %}

```yml
arrays   : {{ arrays  | jsonify }} [{{ arrays  | size | append: ' items' }}]
values   : {{ values  | jsonify }} [{{ values  | size | append: ' items' }}]
objects  : {{ objects | jsonify }} [{{ objects | size | append: ' items' }}]
```

> {% if arrays == empty -%} It won't .. {%- else -%} It works! {%- endif %}

###### echo

Github Pages does not support `echo` at the moment.

```liquid
{% raw %}{% echo 'echo' %}{% endraw %}
```

###### render

Github Pages does not support `render` at the moment. 

```liquid
{% raw %}{% render 'snippet', 
  card_title: "Coffee Maker", 
  card_description: "Brews perfect coffee every time." 
%}{% endraw %}
```

---
{: .mt-6 }

{% include_relative nav_liquid.md %}