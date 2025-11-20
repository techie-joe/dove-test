---
title: Basic Liquid Syntaxes
description: Basic Liquid syntaxes on this site.
---
# {{ page.title }}


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
{% if '' == blank %}Check an blank string with the `blank` object.{%- endif %}
{% if undefined == empty %}Compare with `empty` to check whether an object exists before accessing any of its attributes.{%- endif %}
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
