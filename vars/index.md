---
title: Variables
description: Variables on this site.
use_nav: false
use_footer: false
---
# {{ page.title }}

```yml
page.title         : {{ page.title }}
page.description   : {{ page.description }}
page.layout        : {{ page.layout }}
```

```yml
layout: {{ layout | jsonify }}
```

```yml
site.title         : {{ site.title }}
site.description   : {{ site.description }}
```

###### assign

{% assign nick = 'nik' %}
{% assign layout.who = 'nik' | append: 'ahmad' %}
{% assign page.title = 'New Title' %}
```yml
nick       : {{ nick }}
layout.who : {{ layout.who }}
page.title : {{ page.title }}
```