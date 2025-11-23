---
title: Home
use_header: false
use_nav: false
---
{% include_relative README.md %}

```yml
# _config.yml
version      : {{ site.version | default: '(undefined)' }}
revision     : {{ site.revision | default: '(undefined)' }}{{'.'}}{{ site.github.build_revision | default: '(undefined)' }}
title        : {{ site.title | default: '(undefined)' }}
description  : {{ site.description | default: '(undefined)' }}
```

---
{: .mt-6 }

###### Testing

- [techie-joe.github.io](techie-joe.github.io)
- [Liquid](liquid)

###### Projects

- [Dove themes](https://techie-joe.github.io/dove)

&nbsp;
{: .mt-0 }

{% include footer.md %}