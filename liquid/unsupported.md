---
title: Unsupported Liquid Syntaxes
description: Unsupported Liquid syntaxes on this site.
---
{% capture nav_liquid %}{% include_relative nav_liquid.md %}{% endcapture %}
<nav>{{ nav_liquid | markdownify }}<hr/></nav>

# {{ page.title }}

###### echo

Github Pages does not support `echo` at the moment.

```liquid
{% raw %}{% echo 'echo' %}{% endraw %}
```

###### render

Github Pages does not support `render` at the moment. 

```liquid
{% raw %}{% render 'snippet', 
  card_title: "Coffee Maker", 
  card_description: "Brews perfect coffee every time." 
%}{% endraw %}
```

---
{: .mt-6 }

{% include_relative nav_liquid.md %}