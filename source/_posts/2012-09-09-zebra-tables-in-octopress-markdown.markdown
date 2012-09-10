---
layout: post
title: "Zebra tables in Octopress markdown"
date: 2012-09-09 23:09
comments: true
categories: css octopress markdown
---

## The problem: post-local CSS

In a recent post, I wanted to add a zebra table ([[1][L0]],[[2][L1]])
via the CSS3 `tr:nth-child` selectors, see [StackOverflow][L2].  But
the default Octopress [markdown][L3] drove me crazy by wrapping
everything in `<p></p>` which killed my `<style>` attempts.  After a
quick glance at the [markdown syntax doc][L4] suggested I could use
`<div>` to get around this.
[L0]: http://en.wikipedia.org/wiki/Zebra_striping#CSS
[L1]: http://www.alistapart.com/articles/zebratables/
[L2]: http://stackoverflow.com/a/2765557
[L3]: https://github.com/rtomayko/rdiscount
[L4]: http://daringfireball.net/projects/markdown/syntax#precode


## An example

It is useful to define the style locally since a global definition
may not fit all circumstances.  In the style below, we define a the
table class `ztab1` along with a few other style elements to dress up
the table.

``` css zebra table in default markdown
<div>
  <style>
     table.ztab1 {
        margin: auto;
        font-size: 70%;
        border: 1px solid black;
      }

      table.ztab1 th {
        font-weight: bold;
        background-color: steelblue;
        text-align: center;
        border-bottom: 2px solid black;
      }

      table.ztab1 th,td {
        padding: 4px 5px;
      }

      table.ztab1 tr:nth-of-type(odd) {
        background-color: lightsteelblue;
      }

      table.ztab1 tr:nth-of-type(even) {
        background-color: cornflowerblue;
      }
  </style>
</div>

```

<div>
  <style>
     table.ztab1 {
        margin: auto;
        font-size: 70%;
        border: 1px solid black;
      }

      table.ztab1 th {
        font-weight: bold;
        background-color: steelblue;
        text-align: center;
        border-bottom: 2px solid black;
      }

      table.ztab1 th,td {
        padding: 4px 5px;
      }

      table.ztab1 tr:nth-of-type(odd) {
        background-color: lightsteelblue;
      }

      table.ztab1 tr:nth-of-type(even) {
        background-color: cornflowerblue;
      }
  </style>
</div>

## The result

Using the `ztab1` table class defined above allows us to input raw HTML
table to produce

<table class="ztab1">
  <tr>
    <th>Counter</th>
    <th>Animal</th>
    <th>Collective Name</th>
  </tr>
  <tr>
    <td style="text-align: center;">1</td>
    <td>apes</td>
    <td>shrewdness</td>
  </tr>
  <tr>
    <td style="text-align: center;">2</td>
    <td>bees</td>
    <td>grist</td>
  </tr>
  <tr>
    <td style="text-align: center;">3</td>
    <td>mules</td>
    <td>rake</td>
  </tr>
  <tr>
    <td style="text-align: center;">4</td>
    <td>owls</td>
    <td>parliament</td>
  </tr>
</table>
&nbsp;

The first column entries are centered by 
``` css Center first column entry
<td style="text-align: center;">1</td>
```

# Conclusion

Using a `<div>` tag wrapper prevents the default Octopress markdown from
eating `<style>` definitions.  However a better solution would be to
change the markdown parser, as suggested by [Chico][L5] and [Aral Balkan][L6].
[L5]: http://oblita.com/blog/2012/07/06/octopress-with-mathjax-by-kramdown/
[L6]: http://www.whatwherewhy.me/blog/2012/01/15/changing-the-markdown-processor-in-octopress/
