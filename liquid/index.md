---
title: Liquid
description: Liquid on this site.
use_nav: false
use_footer: false
---
# {{ page.title }}

###### assign

`todo: assigning values`

###### jsonify

{% assign object = '{ "key": "value" }' | parse_json %}
{% assign values = '[ "key" => "value" ]' | parse_json %}
{% assign arrays = '[ "array", 1, 2 ]' | parse_json %}
{% assign products = '[
  {"name": "Laptop", "price": 1200.00, "in_stock": true},
  {"name": "Mouse", "price": 25.50, "in_stock": true},
  {"name": "Keyboard", "price": 80.00, "in_stock": false}
]' | parse_json %}

```yml
object: {{ object | jsonify }}
------------------------------
values: {{ values | jsonify }}
------------------------------
arrays: {{ arrays | jsonify }}
------------------------------
products: {{ products | jsonify }}
```

###### loop

{% assign collection_a = [1,2,3,4,5,6,7,8,9] %}
{% assign collection_b = '1,2,3,4,5,6,7,8,9' %}
{% assign collection_c = '[1,2,3,4,5,6,7,8,9]' | parse_json %}

```
collection_a: {{ collection_a | jsonify }}
{% for item in collection_a limit:5 %}{{ item }},
{%- endfor %}

collection_b: {{ collection_b | split: ',' | jsonify }}
{% for item in collection_b limit:5 %}{{ item }},
{%- endfor %}

collection_c: {{ collection_c | jsonify }}
{% for item in collection_c limit:5 %}{{ item }},
{%- endfor %}

# there is also break and continue.
```

###### comments

There’s a comment block below this line.

<!-- This HTML comment will not appear in the rendered Markdown -->

{% comment %}This Liquid comment will not appear in the rendered Markdown{%- endcomment %}
{% comment %}
Another comment
in multiple
lines
{%- endcomment %}

Comment block should not appear in the rendered Markdown.

###### capture

{% capture block %}
**captured block**{: .text-purple }
{%- endcapture %}

{{ block }}
{: .box.ba.text-center }

###### filters

{% assign my_name = "jAmEs pEtErSoN" %}
{% assign today = '2025-11-19T10:30:00' %}
{% assign list = "apple,banana,cherry" %}

```
default     : {{ default | default: '(default)' }}
upcase      : {{ my_name | upcase }}
downcase    : {{ my_name | downcase }}
capitalize  : {{ my_name | capitalize }}
replace     : {{ my_name | capitalize | replace: "peterson", "Rodney" }}
date        : {{ today | date: "%B %d, %Y" }}
size        : {{ list | size }} (string length)
split       : {{ list | split: "," | size }} (array size)
```

###### controls

```
{% assign condition = true %}condition : {{ condition }}
{% if condition %}if.condition : true
{%- endif %}

{% assign condition_2 = true %}condition_2 : {{ condition_2 }}
{% if condition_ %}{%- elsif condition_2 %}elsif.condition_2 : true
{%- endif %}

{% assign condition_3 = true %}condition_3 : {{ condition_3 }}
{% if condition_ %}{%- else %}else.condition_3 : true
{%- endif %}

{% assign condition_4 = 'unique' %}condition_4 : {{ condition_4 }}
{% unless condition_4 == 'x_unique' %}unless.condition_4 : x_unique
{%- endunless %}
{% unless condition_4 == 'unique' %}unless.condition_4 : unique
{%- endunless %}

{% assign condition_5 = 'when-b' %}condition_5 : {{ condition_5 }}
{% case condition_5 %}
case.condition_5 :
{%- when 'when-a' %}is A
{%- when 'when-b' %}is B
{%- endcase %}
```

###### raw

`raw` skips liquid rendering. 
Be carefull when closing the `raw` tag. 
Closing with `%-` cause build error.  

```liquid
{% raw %}{% assign x = 'x' %}
product.title : {{ product.title | default: 'undefined' }}
product.description : {{ product.description | default: 'undefined' }}{% endraw %}
```

###### echo

Github Pages did not support the `echo` tag at the moment.

```
{% raw %}{% echo 'echo' %}{% endraw %}
```

###### render

Github Pages did not support the `render` tag at the moment. 

```
{% raw %}{% render 'snippet', 
  card_title: "Coffee Maker", 
  card_description: "Brews perfect coffee every time." 
%}{% endraw %}
```
