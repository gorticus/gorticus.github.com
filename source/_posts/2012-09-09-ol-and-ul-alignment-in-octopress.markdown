---
layout: post
title: "OL and UL alignment in Octopress"
date: 2012-09-09 13:01
comments: true
categories: octopress css markdown
---

<div>
  <style>
    ul.octo_default {
      padding-left: 0em;
    }
  </style>
</div>
The default [Octopress][L0] style does not indent OL and UL lists, i.e.,

<ul class="octo_default">
  <li>flight of bees</li>
  <li>lodge of beavers</li>
  <li>rabble of butterflies</li>
  <li>murder of crows</li>
</ul>

I dislike this very much, and prefer
<ul>
  <li>flight of bees</li>
  <li>lodge of beavers</li>
  <li>rabble of butterflies</li>
  <li>murder of crows</li>
</ul>

After a quick search, Octopress [Issue #417][L1] provided the the simple 
solution: add
{% codeblock lang:css Custom css in `sass/custom/_styles.scss` https://github.com/imathis/octopress/issues/417#issuecomment-3950721 Issue #417 %}
article {
  ol, ul {
    padding-left: 3em;
  }
}

{% endcodeblock %}
or any other custom css to `sass/custom/_styles.scss`.

[L0]: http://www.octopress.com/
[L1]: https://github.com/imathis/octopress/issues/417#issuecomment-3950721
