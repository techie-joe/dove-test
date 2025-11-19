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
layout        : {{ layout.layout }}
```

```yml
site.title         : {{ site.title }}
site.description   : {{ site.description }}
```

###### assign

{% assign nick = 'nik' | append: 'ahmad' %}
{% assign layout.zee = 'zakwan' %}
{% assign page.title = 'New Title' %}
```yml
undefined  : {{ undefined | default: '(undefined)' }}
nick       : {{ nick }}
layout.zee : {{ nick }}
```