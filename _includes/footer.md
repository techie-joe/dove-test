{% capture footer %}
**Proto's**
&bull; [Repository](https://github.com/techie-joe/proto)
&bull; [Pages](pages)
&bull; [Posts](posts)
&bull; [Variables](vars)
{%- endcapture %}

{% if page.use_footer == false %}
{%- else %}
  {% if not page.use_footer contains 'edit_link_only' %}
  <hr/>{{ footer }}
  {%- endif %}
  {% if site.github.private != true and site.github.license %}
  <hr/><div class="text-right text-gray">This site is open source. {% github_edit_link "Improve this page" %}.</div>
  {%- endif %}
{%- endif %}