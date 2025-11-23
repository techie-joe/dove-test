---
title: Liquid basics
description: Basic Liquid syntaxes.
---
{% capture nav_liquid %}{% include_relative nav_liquid.md %}{% endcapture %}
<nav>{{ nav_liquid | markdownify }}<hr/></nav>

# {{ page.title }}

###### assign values

```liquid
{% raw %}{%- assign var = value_or_expression | filter: 'filter_expression' %}{% endraw %}
```

```yml
var     : {{ var | default: '(value_or_expression)' }}
default : {{ undefined | default: '(undefined)' }}
nil     : {{ nil | default: '(nil is false and renders nothing)' }}
```

###### strings

{%- assign string   = 'jAmEs  r  pEtErSoN .' %}

```yml
string        : {{ string }} [{{ string | size | append: ' characters' }}]

# replace: ' r ' | remove: '.'
{%- assign string = string | replace: ' r ', ' ' | remove: '.' | split: ' ' | join: ' ' %}
string        : {{ string }} [{{ string | size | append: ' characters' }}]
upcase        : {{ string | upcase }}
downcase      : {{ string | downcase }}
capitalize    : {{ string | capitalize }}

# replace: 'peterson' | capitalize | prepend: 'Mr. ' | append: ' (age 42)'
{%- assign string = string | downcase | replace: "peterson", "Rodney" | capitalize | prepend: 'Mr. ' | append: ' (age 42)' %}
string        : {{ string }} [{{ string | size | append: ' characters' }}]
truncate      : {{ string | truncate: 15 }}
```

###### date

{%- assign date     = '2005-03-09T20:10:30' %}

```yml
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

```liquid
if true : {% if true -%} when true {%- endif %}
elsif true : {% if false -%}  {%- elsif true -%} when true {%- endif %}
else : {% if false -%} when false {%- else -%} otherwise {%- endif %}

unless true  : {% unless true  -%} when not true {%- else -%} when true {%- endunless %}
unless false : {% unless false -%} when not false {%- else -%} when false {%- endunless %}

case 'a' : {% case 'a' -%}
{%- when 'a' -%} when 'a'
{%- else -%} otherwise 
{%- endcase %}
else : {% case 'a' -%}{%- else -%} otherwise 
{%- endcase %}

# Check a blank string with the `blank` object.
{% if '' == blank -%} works {%- else -%} not working {%- endif %}

# Compare with `empty` to check whether an object exists before accessing any of its attributes.
{% if undefined == empty -%} works {%- else -%} not working {%- endif %}
```

###### arrays

{%- assign numbers = (1..9) %}

```yml
numbers  : {{ numbers | jsonify }} [{{ numbers | size | append: ' items' }}]
```

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

###### loops

{%- assign _limit = 5 %}

{% comment %}
{% for i in numbers limit:_limit %}{{ i }} {% cycle 'odd', 'even' %}, {% endfor %}
{% endcomment %}

```
{% for i in numbers limit:_limit -%} [{{ i }}, {% cycle 'odd', 'even' %}] {% endfor %}
```

{% raw %}Use `{% break %}` and `{% continue %}` to get out of a loop. 
Use `{% else %}` to handle empty arrays.{% endraw %}

###### capture

{% capture block -%}
**captured block**{: .text-purple }
{%- endcapture %}

{{ block }}
{: .box.ba.text-center }

{% capture note_md -%}
Use `markdownify` to transform markdown to HTML, before using it inside an HTML block.'
{%- endcapture %}

<small>{{ note_md | markdownify }}</small>

###### comments

There’s a comment block below this line.

<!-- This HTML comment will not appear in the rendered Markdown -->

{% comment %}This Liquid comment will not appear in the rendered Markdown{%- endcomment %}
{% comment %}
in multiple
lines too
{%- endcomment %}

Comment block will not appear in the rendered Markdown.

###### raw

`raw` skips liquid rendering. 
Using **white-space modifier** `-` with it will cause build error.  

```liquid
{% raw %}product.title : {{ product.title }}{% endraw %}
{% raw %}{%- assign x = 'x' %}
{% comment %}comment{% endcomment %}{% endraw %}
```

---
{: .mt-6 }

{% include_relative nav_liquid.md %}