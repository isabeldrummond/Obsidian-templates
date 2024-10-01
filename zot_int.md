---
citekey: "@{{citekey}}"
---
{% if title %}
# "{{title}}"
{% endif %}


> [!Metadata]
> - **Title**:: {% if title %}{{title}} {% endif %} {% if publicationTitle %}
> - **Publication**:: {{publicationTitle}} {% endif %}
{%- if authors %}
> - **Authors**:: {{authors}}
{%- endif -%}
{%- if date %}
> - **Date**:: {{date | format("YYYY")}}
{%- endif -%} 
{%- if importDate %} 
> - **Import date**:: {{importDate |  format("YYYY-MM-DD")}}
{%- endif -%}.    
> - **Links:**  [online]({{uri}}) , [local]({{desktopURI}}) {%- for attachment in attachments | filterby("path", "endswith", ".pdf") %}, [pdf](file://{{attachment.path | replace(" ", "%20")}}) {% if loop.last %} {% endif %} {%- endfor -%} 
{%- if hashTags %}
> - **Tags**:: {{hashTags}}
{%- endif %}


>[!Abstract]
**Abstract**:: {%- if abstractNote %}
>  {{abstractNote}} {%- endif -%}.  


> [!Synthesis]
> **Contribution**::  
> **Related**:

{% if title %}
## Notes 
{% endif %}
{% macro heading(color) -%}
{%- if color == "#ff6666" -%}
💭 Objectives & research questions
{%- elif color == "#f06292" -%}
💭 Type (qualitative, quantitative, conceptual, literature review (including meta-analysis)
{%- elif color == "#5fb236" -%}
💭 Theory & frameworks
{%- elif color == "#2ea8e5" -%}
💭 Research design
{%- elif color == "#ffd400" -%}
💭 Key findings and conclusions
{%- elif color == "#a28ae5" -%}
💭 Call for future research & gaps
{%- elif color == "#f19837" -%}
💭 Quotes and keywords
{%- elif color == "#aaaaaa" -%}
💭 Other notes
{%- endif -%}
{%- endmacro -%}
{% if annotations.length > 0 %}
{% for color, annotations in annotations | groupby("color") -%}
## {{ heading(color) | safe }}

{%- for annotation in annotations -%}
{%- if annotation.imageRelativePath %}
![[{{ annotation.imageRelativePath }}]]
{%- endif %}

{%- if annotation.comment %}
**{{ annotation.comment }}:**

>{{ annotation.annotatedText | nl2br }} [(p. {{ annotation.pageLabel }})](zotero://open-pdf/library/items/{{ annotation.attachment.itemKey }}?page={{ annotation.pageLabel }}&annotation={{ annotation.id }}) 
{% if annotation.hashTags %}
{{ annotation.hashTags }}
{% endif %}

{%- elif annotation.annotatedText %}
{{ annotation.annotatedText | nl2br }} [(p. {{ annotation.pageLabel }})](zotero://open-pdf/library/items/{{ annotation.attachment.itemKey }}?page={{ annotation.pageLabel }}&annotation={{ annotation.id }}) 

{% if annotation.hashTags %}
{{ annotation.hashTags }}

{% endif %}
{%- endif -%}
{%- endfor %}

{% endfor -%}
{% endif %}

