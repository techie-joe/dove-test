---
title: Handling Liquid Variables
description: Handling Liquid variables on this site.
---
# {{ page.title }}

###### assign values

```liquid
{% raw %}{% assign var = value_or_expression | filter: 'filter_expression' %}{% endraw %}
```

```yml
var     : {{ var | default: '(value_or_expression)' }}
default : {{ undefined | default: '(undefined)' }}
nil     : {{ nil | default: '(nil is false and renders nothing)' }}
```

{% assign string   = 'jAmEs pEtErSoN' %}
{% assign color    = 'blue' %}

```yml
# string
string      : {{ string }} [{{ string | size | append: ' characters' }}]
upcase      : {{ string | upcase }}
downcase    : {{ string | downcase }}
capitalize  : {{ string | capitalize }}
replace     : {{ string | capitalize | replace: "peterson", "Rodney" }}

# color
color : {{ color }}{{' > '}}{% assign color = "green" %}{{ color }}
```

###### list & loops

{% assign list_x   = 'a,m,b,n,c,o,z,y,x' | split: ',' %}
{% assign sorted_list_x = list_x | sort %}
{% assign reverse_sorted_list_x = list_x | sort | reverse %}
{% assign sliced_sorted_list_x  = sorted_list_x | slice: 3, 3 %}

```yml
list_x   : {{ list_x }} [{{ list_x | size | append: ' items' }}]
jsonify  : {{ list_x | jsonify }}
join     : {{ list_x | join: ',' }}
order    : {{ list_x | first }}{{' ... '}}{{ list_x | last }}

{{'# list_x  : '}}{% for item in list_x %}[{{ item }}]{{' '}}{%- endfor %}

{{'# limit:3 : '}}{% for item in list_x limit:3 %}[{{ item }}]{{' '}}{%- endfor %}

sorted_list_x         : {{ sorted_list_x | jsonify }}
order                 : {{ sorted_list_x | first }}{{' ... '}}{{ sorted_list_x | last }}

reverse_sorted_list_x : {{ reverse_sorted_list_x | jsonify }}
order                 : {{ reverse_sorted_list_x | first }}{{' ... '}}{{ reverse_sorted_list_x | last }}

sliced_sorted_list_x  : {{ sliced_sorted_list_x | jsonify }}
order                 : {{ sliced_sorted_list_x | first }}{{' ... '}}{{ sliced_sorted_list_x | last }}
```

{% assign list_a   = 'apple,banana,cherry' | split: ',' %}

```yml
list_a   : {{ list_a }} [{{ list_a | size | append: ' items' }}]
jsonify  : {{ list_a | jsonify }}
join     : {{ list_a | join: ',' }}
order    : {{ list_a | first }}{{' ... '}}{{ list_a | last }}
```

{% assign join_list_a = list_a | join: ',' %}
{% assign add_list_a  = 'pear,' | append: join_list_a | append: ',durian' %}
{% assign new_list_a  = add_list_a | split: ',' %}
{% assign list_a = new_list_a %}

```yml
list_a   : {%  | append: list_a | append: "durian" %}{{' > '}}{{ list_aa }}
list_aa.jsonify : {{ list_aa | jsonify }}
```

{% assign list_b   = '["pen","gum","tin"]' | parse_json %}

```yml
# list_b       = '["pen","gum","tin"]'
list_b          : {{ list_b }}
list_b.jsonify  : {{ list_b | jsonify }}
list_b.size     : {{ list_b | size }}
# list_b.0       : {{ list_b[0] }}{% assign list_b[0] = "bin" %}{{' > '}}{{ list_b[0] }}
# list_b.3       : {{ list_b[3] }}{% assign list_b[3] = "can" %}{{' > '}}{{ list_b[3] }}
list_b.jsonify : {{ list_b | jsonify }}

{{'# '}}{% for item in list_b limit:3 %}[{{ item }}]{{' '}}{%- endfor %}
```

{% assign products = '[
  "laptop"   => {"name": "Ace",  "price": 1200.00, "in_stock": true},
  "mouse"    => {"name": "Mice", "price": 25.50,   "in_stock": true},
  "keyboard" => {"name": "Keys", "price": 80.90,   "in_stock": false}
]' | parse_json %}

```yml
products         : {{ products }}
products.size    : {{ products | size }}
products.jsonify : {{ products | jsonify }}
products[0]      : {{ products[0] }}
products.laptop  : {{ products.laptop | jsonify }}

{{'# '}}{% for item in products limit:2 %}[{{ item }}],
{%- endfor %}
```

Use {% raw %}`{% break %}` and `{% continue %}` to get out of a loop.{% endraw %}