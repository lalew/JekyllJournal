---
layout: post
title: Markdown & Liquid Cheatsheet
date:   2016-08-08
tags: [liquid, markdown]
---
Markdown and Liquid Cheatsheet!
<!--more-->
**Block-level Elements - Main Structural Elements**

{% highlight bash %}
Paragraphs              (/n)
Headers                 (#)
Blockquotes             (>)
Code                    (`)
HR                      (***---)
Lists                   (1,*,-,+)
Definition Lists        (: )
Tables                  (|,|:,|-,|=)
HTML                    ({::options parse_block_html="true" /})

Block Attri       {: title="val"},{: .class #id}
                  {:refdef: .c1 #id .c2 title="title"}
                  {: refdef title="override"}
Extension   {::comment} {:/comment}
            {::nomarkdown}{:/}
            {::options auto_ids="false" /}
{% endhighlight %}

**Span-Level Elements - Text Modifiers**

{% highlight bash %}
  *em*
  **strong**
  Links:
        [link](in a tag)
        [link][variable alt]
        [var]: content "alt"

  Image         ( ![gras](img/image.jpg) )
  Code          (``,`)
  Footnotes     ([^1],[^1:])
  Abbrev        (*[abbr]: Replacement)
  Inline Attr   (*content*{: attri="val"})
{% endhighlight %}

**Be very careful with spacing with liquid syntax!**
**For example, DO NOT SEPARATE the line below with spaces/newlines**
{% highlight shell %}
  {% capture site_tags %}{% for tag in site.tags %}{{ tag | first }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
{% endhighlight %}