---
title: Liquid basics
description: Basic Liquid syntaxes.
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

###### number

{% assign number = 0 %}

```yml
increment: {% increment number %}{{ number }}
decrement: {% decrement number %}{{ number }}
```

###### strings

{% assign string   = 'jAmEs r pEtErSoN' %}
{% assign color    = 'blue' %}

```yml
string        : {{ string }} [{{ string | size | append: ' characters' }}]
upcase        : {{ string | upcase }}
downcase      : {{ string | downcase }}
capitalize    : {{ string | capitalize }}
replace       : {{ string | capitalize | replace: "peterson", "Rodney" }}
truncate      : {{ string | truncate: 7 }}
# remove 'r'  : {{ string | remove: 'r' }}
# remove 'r ' : {{ string | remove: 'r ' }}
prepend       : {{ string | prepend: 'Mr.' }}
append        : {{ string | append: '(Senior)' }}

color : {{ color }}{{' > '}}{% assign color = "green" %}{{ color }}
```

###### date

{% assign date     = '2005-03-09T20:10:30' %}

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
if true : {% if true -%}then{%- endif %}
elsif true : {% if false -%}{%- elsif true -%}then{%- endif %}
else : {% if false -%}{%- else -%}means (others){%- endif %}

unless false : {% unless false %}means (other than false){%- endunless %}

case 'a' : {% case 'a' -%}
{%- when 'a' -%}is A
{%- endcase %}

# Check a blank string with the `blank` object.
{% if '' == blank -%} works {%- else -%} not working {%- endif %}

# Compare with `empty` to check whether an object exists before accessing any of its attributes.
{% if undefined == empty -%} works {%- else -%} not working {%- endif %}
```

###### arrays

{% assign numbers = (1..9) %}
{% assign arrays  = '[ "pen", 0.9, true ]' | parse_json | jsonify %}
{% assign values  = '[ "key" => "value" ]' | parse_json | jsonify %}
{% assign objects = '{ "key" :  "value" }' | parse_json | jsonify %}

```yml
numbers  : {{ numbers | jsonify }} [{{ numbers | size | append: ' items' }}]
arrays   : {{ arrays  | jsonify }} [{{ arrays  | size | append: ' items' }}]
values   : {{ values  | jsonify }} [{{ values  | size | append: ' items' }}]
objects  : {{ objects | jsonify }} [{{ objects | size | append: ' items' }}]
```

###### loops

{% assign _limit = 5 %}

{% comment %}
{% for i in numbers limit:_limit %}{{ i }} {% cycle 'odd', 'even' %}, {% endfor %}
{% endcomment %}

```
{% for i in numbers limit:_limit %}{{ i }} {% cycle 'odd', 'even' %}, {% endfor %}
else in for : {% for i in undefined -%} not working {%- else -%} works {%- endfor %}
```

> Use {% raw %}`{% break %}` and `{% continue %}` to get out of a loop.{% endraw %}

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

Comment block will not appear in the rendered Markdown.

---
{: .mt-6 }

{% include_relative _nav.md %}