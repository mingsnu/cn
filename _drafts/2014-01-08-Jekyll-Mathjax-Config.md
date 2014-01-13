---
title: Jekyll Mathjax Configuration
layout: post
categories: 技术笔记
tags:
  - Jekll
  - Mathjax
  - Configuration
---

To enable the MathJax support for jekyll, you should add the following code to the `default.html` file of your jekyll theme (layout).

{% highlight javascript %}
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  jax: ["input/TeX", "output/HTML-CSS"],
  tex2jax: {
    inlineMath: [['$', '$']],
    displayMath: [['$$', '$$']],
    processEscapes: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
  },
  messageStyle: "none",
  "HTML-CSS": { preferredFont: "TeX", availableFonts: ["STIX","TeX"] }
});
</script>
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>
{% endhighlight %}

By default Jekyll uses `maruku` as the default markdown render, there are also other markdown renders can be used, such as `rdiscount`, `redcarpet` and `kramdown`. Check [here](http://jekyllrb.com/docs/configuration/) for details.

Here are some issues need to be noticed:

1. According to my experience, `maruku` and `redcarpet` don't support long formula block well, such as equation alignment, but `kramdown` does well.


**Reference**
Math support in Maruku: http://maruku.rubyforge.org/math.xhtml
MathJax basic tutorial and quick reference: http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference
MathJax Sample: http://www.mathjax.org/demos/tex-samples/
Writing Math Equations on Octopress: http://www.idryman.org/blog/2012/03/10/writing-math-equations-on-octopress/
