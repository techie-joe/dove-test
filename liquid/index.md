---
title: Liquid
description: Liquid on this site.
use_nav: false
use_footer: false
---
# {{ page.title }}

###### assign values

```liquid
{% raw %}{% assign var = value_or_expression | filter: 'filter_expression' %}{% endraw %}
```

```yml
var     : {{ var | default: '(value_or_expression)' }}
default : {{ undefined | default: '(default)' }}
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

{% liquid
assign list_x   = 'a,m,b,n,c,o,z,y,x' | split: ','
assign sorted_list_x = list_x | sort
assign reverse_sorted_list_x = list_x | sort | reverse
assign sliced_sorted_list_x  = sorted_list_x | slice: 3, 3
%}

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

{% liquid
assign join_list_a = list_a | join: ','
assign add_list_a  = 'pear,' | append: join_list_a | append: ',durian'
assign new_list_a  = add_list_a | split: ','
assign list_a = new_list_a
%}

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

###### date

{% assign date     = '2005-03-09T20:10:30' %}

```yml
# date
date : {{ date }}
date : {{ date | date: "%A, %B %d, %Y @ %I:%M:%S %p" }}
```

| -- | :-------------------------------- | ----- | 
| %B | Full month name | November |
| %b | Abbreviated month name | Nov |
| %A | Full day name | Thursday |
| %a | Abbreviated day name | Thursday |
| %w | Day of the week as a number (0=Sunday, 6=Saturday) | 4 |
| %d | Month as a padded number (01-12) | 03 |
| %m | Month as a padded number (01-12) | 03 |
| %Y | Full year (4 digits) | 2005 |
| %y | Year as a padded number (2 digits) | 05 |
| %H | 24-hour clock (00-23) | 21 |
| %I | 12-hour clock (01-12) | 06 |
| %M | Minute as a padded number (00-59) | 01 |
| %S | Second as a padded number (00-59) | 02 |
| %p | AM/PM indicator (uppercase) | PM |
{: .simple }

###### controls

```
if true : {% if true %}then{%- endif %}
elsif true : {% if false %}{%- elsif true %}then{%- endif %}
else : {% if false %}{%- else %}means (other than true){%- endif %}
unless false : {% unless false %}means (other than false){%- endunless %}
case 'a' : {% case 'a' %}
{% when 'a' %}is A
{% when 'b' %}is B
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
in multiple
lines too
{%- endcomment %}

Comment block should not appear in the rendered Markdown.

###### raw

`raw` skips liquid rendering.
Be carefull using it. Closing with `%-` cause build error.  

```liquid
{% raw %}{% assign x = 'x' %}{% endraw %}
{% raw %}{% comment %}comment{% endcomment %}
product.title : {{ product.title }}
product.description : {{ product.description }}{% endraw %}
```

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
