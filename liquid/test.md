---
title: Test
description: Testing Liquid syntaxes.
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

{%- assign is_working = arrays | jsonify | size %}

> {% if is_working == 0 -%} It fails! {%- else -%} It works! {%- endif %}

###### test 2

{%- assign list_b   = '["pen","gum","tin"]' | parse_json %}

```yml
list_b   : {{ list_b }} [{{ list_b | size | append: ' items' }}]
jsonify  : {{ list_b | jsonify }}
```

```js
{% for item in list_b %}[{{ item }}]{{' '}}{%- endfor %}
```

{%- assign products = '[
  "laptop"   => {"name": "Ace",  "price": 1200.00, "in_stock": true},
  "mouse"    => {"name": "Mice", "price": 25.50,   "in_stock": true},
  "keyboard" => {"name": "Keys", "price": 80.90,   "in_stock": false}
]' | parse_json %}

```yml
products : {{ products | jsonify }} [{{ products | size | append: ' items' }}]
products.laptop : {{ products.laptop | jsonify }}
```

```js
{% for item in products %}[{{ item }}],{%- endfor %}
```
