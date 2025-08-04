---
阅读情况: 
代码: 
标签: 
发表时间: 
期刊:
---


### 关键词
{% persist "keywords" %}


{% endpersist %}

### 关键句
{% persist "keysentenses" %}


{% endpersist %}


---
# 参考网站
{% persist "references" %}


{% endpersist %}

---


# Self Notes
{% persist "notes" %}{% if isFirstImport %}
## 概述

## 概念理解

## 公式理解
{% endif %}
{% endpersist %}

---

# Reading notes
{% persist "annotations" %}

{%-
    set zoteroColors = {
	    "#2ea8e5": "blue",
        "#5fb236": "green",
        "#a28ae5": "purple",
        "#ff6666": "red",
        "#ffd400": "yellow",
        "#f19837": "orange",
        "#aaaaaa": "grey",
        "#e56eee": "magenta"
    }
-%}

{%-
   set colorHeading = {
		"purple": "💡 灵感",
		"blue": "😮 以前人们发现",
		"orange": "🙈 其他论文的弊端或不足之处",
		"purple": "💡 灵感",
		"red": "😎 主要任务和重要发现",
		"magenta": "📒 对模型的解释",
		"grey": "😵 难以理解的地方",
		"green": "⭐ 将来可能有用的地方；需要理解和记住的",
		"yellow": "✍️ 对写作有帮助的"
   }
-%}

{%- macro calloutHeader(type) -%}
    {%- switch type -%}
        {%- case "highlight" -%}
        Highlight
        {%- case "image" -%}
        Image
        {%- default -%}
        Note
    {%- endswitch -%}
{%- endmacro %}

{%- set newAnnot = [] -%}
{%- set newAnnotations = [] -%}
{%- set annotations = annotations | filterby("date", "dateafter", lastImportDate) %}

{% if annotations.length > 0 %}
*Imported: {{importDate | format("YYYY-MM-DD HH:mm")}}*

{%- for annot in annotations -%}

    {%- if annot.color in zoteroColors -%}
        {%- set customColor = zoteroColors[annot.color] -%}
    {%- elif annot.colorCategory|lower in colorHeading -%}
    	{%- set customColor = annot.colorCategory|lower -%}
    {%- else -%}
	    {%- set customColor = "other" -%}
    {%- endif -%}

    {%- set newAnnotations = (newAnnotations.push({"annotation": annot, "customColor": customColor}), newAnnotations) -%}

{%- endfor -%}

{#- INSERT ANNOTATIONS -#}
{#- Loops through each of the available colors and only inserts matching annotations -#}
{#- This is a workaround for inserting categories in a predefined order (instead of using groupby & the order in which they appear in the PDF) -#}

{%- for color, heading in colorHeading -%}
{%- for entry in newAnnotations | filterby ("customColor", "startswith", color) -%}
{%- set annot = entry.annotation -%}

{%- if entry and loop.first %}

### {{colorHeading[color]}}
{%- endif %}

> [!quote{{"|" + color if color != "other"}}]+ {{calloutHeader(annot.type)}} ([page. {{annot.pageLabel}}](zotero://open-pdf/library/items/{{annot.attachment.itemKey}}?page={{annot.pageLabel}}&annotation={{annot.id}}))

{%- if annot.annotatedText %}
> {{annot.annotatedText|nl2br}} {% if annot.hashTags %}{{annot.hashTags}}{% endif -%}
{%- endif %}

{%- if annot.imageRelativePath %}
> ![[{{annot.imageRelativePath}}]]
{%- endif %}

{%- if annot.ocrText %}
> {{annot.ocrText}}
{%- endif %}

{%- if annot.comment %}
> - **{{annot.comment|nl2br}}**
{%- endif -%}

{%- endfor -%}
{%- endfor -%}
{% endif %}
{% endpersist %}


