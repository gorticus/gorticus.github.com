---
layout: post
title: "Site updates"
date: 2012-09-16 00:14
comments: true
categories: misc tex markdown
---

A few updates:

- [MathJax][L0] with help from
  - [chico][L1]: [Octopress with MathJax by kramdown][L2]
  - [Gregory Lussier][L3]: 
      [How to Integrate MathJax LaTeX Mathematics Markup in Octopress][L4]
  - [Steven Shaw][L5]: [Hello MathJax][L6]
- New theme
  - [Alessandro Melandri][L7]: [darkstripes][L8] (as [submodule][L9])

One annoying thing that occurred with

{% codeblock lang:bash Installing darkstripes theme %}
$ rake install['darkstripes']
{% endcodeblock %}

was the over-writing of all my custom `sass`, e.g., styles, etc.  This
seems a little unnecessary, since it's already labeled *custom*.  Why not
leave it, or move it out of the main theme, so it's not stomped on theme
switch.  If your custom changes message the theme, that should be up to
you to fix.  Nuking things is never a good idea, unless we're talking
microwave.

[L0]: http://www.mathjax.org/
[L1]: http://oblita.com/blog/
[L2]: http://oblita.com/blog/2012/07/06/octopress-with-mathjax-by-kramdown/
[L3]: http://greglus.com/
[L4]: http://greglus.com/blog/2011/11/29/integrate-MathJax-LaTeX-and-MathML-Markup-in-Octopress/
[L5]: http://steshaw.org/
[L6]: http://steshaw.org/blog/2012/02/09/hello-mathjax/
[L7]: http://melandri.net/
[L8]: https://github.com/amelandri/darkstripes
[L9]: http://git-scm.com/book/en/Git-Tools-Submodules
