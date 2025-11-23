---
title: Handling list
description: Handling list using Liquid.
---
# {{ page.title }}

{%- assign list_x = 'a,m,b,n,c,o,z,y,x' | split: ',' %}

```liquid
{% raw %}{%- assign list_x = 'a,m,b,n,c,o,z,y,x' | split: ',' %}{% endraw %}
```

```yml
list_x   : {{ list_x }} [{{ list_x | size | append: ' items' }}]
jsonify  : {{ list_x | jsonify }}
join     : {{ list_x | join: ',' }}
order    : {{ list_x | first }}{{' ... '}}{{ list_x | last }}
loop     : # {% for item in list_x %}[{{ item }}]{{' '}}{%- endfor %}
sort     : {{ list_x | sort | jsonify }}
reverse  : {{ list_x | reverse | jsonify }}
slice    : {{ list_x | sort | slice: 3, 3 | jsonify }}
```

{%- assign list_a = 'apple,banana,cherry' | split: ',' %}

```liquid
{% raw %}{%- assign list_a = 'apple,banana,cherry' | split: ',' %}{% endraw %}
```

```yml
list_a   : {{ list_a | jsonify }} [{{ list_a | size | append: ' items' }}]
```

{%- assign list_a = list_a | join: ',' | prepend: 'pear,' | append: ',durian' | split: ',' %}

```liquid
{% raw %}{%- assign list_a = list_a | join: ',' | prepend: 'pear,' | append: ',durian' | split: ',' %}{% endraw %}
```

```yml
list_a   : {{ list_a | jsonify }} [{{ list_a | size | append: ' items' }}]
```

{%- assign list_b   = '["pen","gum","tin"]' | parse_json | jsonify %}

```yml
list_b   : {{ list_b }} [{{ list_b | size | append: ' items' }}]
jsonify  : {{ list_b | jsonify }}

{{'# '}}{% for item in list_b %}[{{ item }}]{{' '}}{%- endfor %}
```

{%- assign products = '[
  "laptop"   => {"name": "Ace",  "price": 1200.00, "in_stock": true},
  "mouse"    => {"name": "Mice", "price": 25.50,   "in_stock": true},
  "keyboard" => {"name": "Keys", "price": 80.90,   "in_stock": false}
]' | parse_json | jsonify %}

```yml
products : {{ products | jsonify }} [{{ products | size | append: ' items' }}]
products.laptop : {{ products.laptop | jsonify }}

{{'# '}}{% for item in products %}[{{ item }}],{%- endfor %}
```

---
{: .mt-6 }

{% include_relative nav_liquid.md %}