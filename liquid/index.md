---
title: Liquid
description: Liquid on this site.
use_nav: false
use_footer: false
---
# {{ page.title }}

###### assign

`{% raw %}{% assign var = value_or_expression %}{% endraw %}`
{% assign string  = "jAmEs pEtErSoN" %}
{% assign date    = "2025-11-19T10:30:00" %}
{% assign list    = "apple,banana,cherry" %}
{% assign color   = "red" %}{% assign color   = "blue" %}
{% assign object  = {pen} %}{% assign color   = "blue" %}

```yml
var     : {{ var | default: '(value_or_expression)' }}
string  : {{ string }}
date    : {{ date }}
list    : {{ list }}
color   : {{ color }}
```

###### filters

```yml
default     : {{ undefined | default: '(default)' }}
upcase      : {{ string | upcase }}
downcase    : {{ string | downcase }}
capitalize  : {{ string | capitalize }}
replace     : {{ string | capitalize | replace: "peterson", "Rodney" }}
date        : {{ date | date: "%B %d, %Y" }}
size        : {{ list | size }} (string length)
split       : {{ list | split: "," | size }} (array size)
```

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

###### controls

```
{% if true %}if{%- endif %}
{% if false %}{%- elsif true %}elsif{%- endif %}
{% if false %}{%- else %}else{%- endif %}
{% unless false %}unless{%- endunless %}
{% case 'a' -%}
case:
{%- when 'when-a' %}is A
{%- when 'when-b' %}is B
{%- endcase %}
```

###### capture

{% capture block %}
**captured block**{: .text-purple }
{%- endcapture %}

{{ block }}
{: .box.ba.text-center }

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

###### raw

`raw` skips liquid rendering.
Be carefull using it. Closing with `%-` cause build error.  

```liquid
{% raw %}{% assign x = 'x' %}{% endraw %}
{% raw %}product.title : {{ product.title }}
product.description : {{ product.description }}{% endraw %}
```

###### echo

Github Pages did not support `echo` at the moment.

```
{% raw %}{% echo 'echo' %}{% endraw %}
```

###### render

Github Pages did not support `render` at the moment. 

```
{% raw %}{% render 'snippet', 
  card_title: "Coffee Maker", 
  card_description: "Brews perfect coffee every time." 
%}{% endraw %}
```
