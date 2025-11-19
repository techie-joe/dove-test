---
title: Liquid
description: Liquid on this site.
use_nav: false
use_footer: false
---
# {{ page.title }}

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

Be carefull when closing the `raw` tag.  
Closing with `%-` cause build error.  

```liquid
{% raw %} assign: {% assign x = 'x' %} {% endraw %}

{% assign product = {
    title: 'Product Title',
    description: 'Product description.',
  }
%}
{% raw %} product.title : {{ product.title | default: 'undefined' }} {% endraw %}
{% raw %} product.description : {{ product.description | default: 'undefined' }} {% endraw %}
```

###### echo

Github Pages did not support the `echo` tag at the moment.

```
{% raw %} {% echo 'echo' %} {% endraw %}
```

###### render

Github Pages did not support the `render` tag at the moment. 

```
{% raw %}
{% render 'snippet', 
  card_title: "Coffee Maker", 
  card_description: "Brews perfect coffee every time." 
%}
{% endraw %}
```

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
Default         : {{ default | default: '(default)' }}
Capitalize      : {{ 'capitalize' | capitalize }}
Uppercase Name  : {{ my_name | upcase }}
Date Format     : {{ today | date: "%B %d, %Y" }}
List Size       : {{ list | split: "," | size }}
Chained Filters : {{ my_name | downcase | replace: "james", "robert" }}
```

###### jsonify

{% assign object = {'key': 'value'} %}
{% assign values = [ 'key' => 'value' ] %}
{% assign arrays = ['array', 1, 2 ] %}

```yml
object: {{ object | jsonify }}
values: {{ values | jsonify }}
arrays: {{ arrays | jsonify }}
```

###### controls

```
{% assign condition = 'yes' %}
{% if condition %}
if.condition :{{ condition }}
{%- endif %}

{% assign condition_2 = 'no' %}
{% if condition_ %}
{%- elsif condition_2 %}
elsif.condition_2 :{{ condition_2 }}
{%- endif %}

{% assign condition_3 = 'idk' %}
{% if condition_ %}
{%- else %}
else.condition_3 :{{ condition_3 }}
{%- endif %}

{% assign condition_4 = 'unique' %}
{% unless condition_4 == 'unique' %}condition_4 :{{ condition_4 }}{%- endunless %}

{% assign condition_5 = 'when-b' %}
{% case condition_5 %}
case :
{%- when 'when-a' %}condition_5 : {{ condition_5 }}
{%- when 'when-b' %}condition_5 : {{ condition_5 }}
{%- endcase %}
```

###### loop

```
{% assign collection = [3,4,6,7] %}
{% for item in collection %}item: {{ item }},{%- endfor %}

{% for item in collection limit:5 %}
- item: {{ item }}
{%- endfor %}

# there is also break and continue.
```