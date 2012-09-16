---
layout: post
title: "Uninstalling MacTeX 2011"
date: 2012-09-15 17:47
comments: true
categories: tex admin
---

Before starting, ***read*** the disclaimer below.

## Long live $\TeX$!

If you are a Mac and $\TeX$ user, you are likely a [MacTeX][L0] user.  If
you've been using it for a while, you have probably accumulated a fair
number of versions, since it is on a roughly yearly release cycle.  To
remove the cruft before installing a new release, I've taken to removing
the old installation.  If you've tried this, you may have looked at the
uninstall instructions, e.g. for [2011][L1], and found them to be, well,
somewhat lacking, e.g. [stackexchange][L2].  The last part, where the
instructions suggest using *Show Files* from the installer, not
particularly useful, given the number of files involved, and the fact
there didn't seem to be a way (on 10.7.4) to export the file list.

## What's installed

Like the uninstall procedure expects, you'll need access to the 2011
`MacTeX.mpkg.zip` file. Make a directory and unzip the file
{% codeblock lang:bash Decompress the old installer package %}
$ mkdir cleanup
$ cd cleanup
$ unzip /path/to/MacTeX.mpkg.zip
{% endcodeblock %}
which could create a `MacTeX.mpkg` directory in your `pwd`.  Now you can
build a table of contents from the archives included, assuming `bash`
{% codeblock lang:bash Generate TOC %}
for a in $(find MacTeX.mpkg -name Archive.pax.gz); do
  pax -zvf $a | awk '{print $9}' | sed -e 's/^.//'
done > mactex.toc
{% endcodeblock %}
Relax, it may take some time, on the order of a minute or two.

## Dirs and files

From the `toc`, the files and dirs can be separated.  We know two
directories whose individual files and sub-directories will be removed
wholesale
{% codeblock lang:bash Complete directory trees to be removed %}
/Applications/TeX
/usr/local/texlive/2011
{% endcodeblock %}
These trees are filtered from the toc to reduce the noise in the output.
A small script will `test` if a line is a directory (`-d`) or a regular
file (`-f`)
{% codeblock lang:bash getem.sh: Filter toc for remaining files or dirs %}
#!/bin/bash

I='mactex-2011-toc.txt'
P=( \
  "^\/usr\/local\/texlive\/2011\/.+$" \
  "^\/Applications\/TeX\/.+$" \
)

case "$1" in
  -d) O='mdirs.txt';;
  -f) O='mfiles.txt';;
   *) echo "usage: getem.sh [-d|-f]"; exit 1;;
esac

for l in $(sed -E -e "/${P[0]}|${P[1]}/d" < $I); do
  test "$1" "$l" && echo "$l"
done | sort -u > $O
{% endcodeblock %}
The `P` var holds the `sed` patterns to filter everything below the tree
heads identified above.  For my install, the directories output were
{% codeblock lang:bash Example directories culled %}
/Applications
/Applications/TeX
/Library
/Library/Fonts
/usr
/usr/local
/usr/local/bin
/usr/local/lib
/usr/local/lib/ImageMagick-6.6.9
/usr/local/lib/ImageMagick-6.6.9/modules-Q16
/usr/local/lib/ImageMagick-6.6.9/modules-Q16/coders
/usr/local/lib/ImageMagick-6.6.9/modules-Q16/filters
/usr/local/share
/usr/local/share/ghostscript
/usr/local/share/ghostscript/9.02
/usr/local/share/ghostscript/9.02/doc
/usr/local/share/ghostscript/9.02/examples
/usr/local/share/ghostscript/9.02/examples/cjk
/usr/local/share/ghostscript/9.02/lib
/usr/local/share/man
/usr/local/share/man/de
/usr/local/share/man/de/man1
/usr/local/share/man/man1
/usr/local/texlive
/usr/local/texlive/2011
{% endcodeblock %}
Clearly, there are some directories that should not be removed!  My
revised dir list was
{% codeblock lang:bash mdirs-short.txt: Realistic dirs to remove %}
/Applications/TeX
/usr/local/texlive/2011
/usr/local/lib/ImageMagick-6.6.9
/usr/local/share/ghostscript
{% endcodeblock %}

So, in addition to the two trees we already expected to prune, the
additional installed `ImageMagick` and `ghostscript` dirs will be
removed.  These were removed by invoking
{% codeblock lang:bash Remove the realistic dirs %}
$ cat mdirs-short.txt | xargs sudo rm -rf
{% endcodeblock %}
where `sudo` is necessary, as it was installed as `root`.  On to the
files, like removing the dirs, invoke
{% codeblock lang:bash Removing remaining files %}
$ cat mfiles.txt | xargs sudo rm -f
{% endcodeblock %}
Once complete, you should feel about 1.7 GB lighter for the full install.

## The preference pane

To remove the old preference pane from System Preferences
{% codeblock lang:bash Remove the preference pane %}
$ sudo rm -rf /Library/PreferencePanes/TeXDistPrefPane.prefPane
{% endcodeblock %}

## Comments

If you instead installed the smaller package, or also added the extras,
use the same process once you obtain a `toc` from the files.

## Now the upgrade

Out with the old and in with the new.  The old cruft is gone and you can
install the [new release][L3].  Happy $\TeX$-ing.

## Disclaimer

This is the process I used to clean-up Mac$\TeX$ 2011.  Use it at your own
risk.  This procedure is provided *AS-IS* and without warranty of any
kind.  In no event will I be liable for any damages arising out of the
use or inability to use this process.  For example, if it causes wild
flying monkeys to burst from your bum, proceed to rend your citadel
down around your ears, put your old floppy disk into your toaster and
use it to set fire to the detritus of your keep and salt the very earth,
all while you watch from the last remaining parapet: your problem, not
mine.

[L0]: http://www.tug.org/mactex/
[L1]: http://www.tug.org/mactex/2011/uninstalling.html
[L2]: http://tex.stackexchange.com/q/26165
[L3]: http://www.tug.org/mactex/
