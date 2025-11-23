---
title: Variables
description: Variables on this site.
use_footer: false
---
# {{ page.title }}

```yml
page.title         : {{ page.title | default: '(undefined)' }}
page.description   : {{ page.description | default: '(undefined)' }}
page.layout        : {{ page.layout | default: '(undefined)' }}
```

```yml
site.title         : {{ site.title | default: '(undefined)' }}
site.description   : {{ site.description | default: '(undefined)' }}
```

```yml
layout             : {{ layout | jsonify }}
```