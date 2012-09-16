---
layout: post
title: "Octopress via GitHub on Mac OS X Lion (10.7)"
date: 2012-09-09 00:10
comments: true
categories: github ruby octopress setup
---

<div>
  <style>
    body {
      font-size: 95%;
    }
  </style>
</div>

Recently, as an educational experience, and a place to share lessons
learned, I decided to setup this [Octopress](http://octopress.org/) blog
hosted via [GitHub](http://github.com/).

## Configuration

While I have a Linux server at home, I do most of my work from my
_Early 2008_ MacBook.  Since I am a conditions to and a fan of the
[GNU tools](http://www.gnu.org/), I use
[Macports](http://www.macports.org/) to manage them and other useful
tools.  You will need a compiler, git, ruby, bash shell, and a terminal.
The following table summarizes my the various items I happen to have
installed.

<div>
  <style>
    table.tab1 {
      margin: auto;
      font-size: 70%;
      border: 1px solid black;
    }

    table.tab1 th {
      font-weight: bold;
      background-color: #909090;
      text-align: center;
      border-bottom: 2px solid black;
    }

    table.tab1 th,td {
      padding: 4px 5px;
    }

    table.tab1 tr:nth-of-type(odd) {
      background-color:#c0c0c0;
    }

    table.tab1 tr:nth-of-type(even) {
      background-color:#efefef;
    }

  </style>

  <table class="tab1">
    <thead>
      <tr>
        <th>Description</th>
        <th>Provider</th>
        <th>Version</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Xcode</td>
        <td>Apple</td>
        <td>4.4.1, build version 4F1003</td>
      </tr>
      <tr>
        <td>CLI tools, llvm-gcc</td>
        <td>Apple</td>
        <td>4.2.1, LLVM build 2336.11.00</td>
      </tr>
      <tr>
        <td>gcc</td>
        <td>MacPorts</td>
        <td>4.5.4, MacPorts gcc45 4.5.4_1</td>
      </tr>
      <tr>
        <td>clang</td>
        <td>Apple</td>
        <td>4.0, LLVM 3.1svn</td>
      </tr>
      <tr>
        <td>ruby</td>
        <td>Apple</td>
        <td>1.8.7, 2011-12-28 patchlevel 357</td>
      </tr>
      <tr>
        <td>keychain</td>
        <td>MacPorts</td>
        <td>2.7.1_1</td>
      </tr>
      <tr>
        <td>git</td>
        <td>Apple</td>
        <td>1.7.9.6, Apple Git-31.1</td>
      </tr>
      <tr>
        <td>git</td>
        <td>MacPorts</td>
        <td>1.7.11.5</td>
      </tr>
      <tr>
        <td>bash</td>
        <td>Apple</td>
        <td>3.2.48(1)</td>
      </tr>
      <tr>
        <td>Terminal.app</td>
        <td>Apple</td>
        <td>2.2.3, 303.2</td>
      </tr>
    </tbody>
  </table>
</div>


## Setup and pitfalls

In addition to the [Octopress documentation](http://octopress.org/docs/setup/), there are many
excellent guides to setting up Octopress hosted via GitHub, e.g.,

- [Getting Started With Octopress](http://www.zhubert.com/blog/2012/04/26/getting-started-with-octopress/)
- [Custom Domain With Octopress and Github Pages](http://robdodson.me/blog/2012/04/30/custom-domain-with-octopress-and-github-pages/)
- [How I built my blog in one day](http://erjjones.github.com/blog/How-I-built-my-blog-in-one-day/)
- [Setup Octopress Under Mac OS X Lion](http://panchoat.org/blog/2012/05/26/setup-octopress-under-mac-os-x-lion/)

Studying these guides closely provided the outline for setting up my
particularly instance.

Most of my difficulty came from order of operations.  I looked at the
instructions, and presumed I knew better, but order was important.  So,
I present the following items in the order that finally worked for me.


### Git

[Git](http://git-scm.com/) is the fashionable and powerful [revision control](http://goo.gl/Qy5fz) system.  [Get it](https://help.github.com/articles/set-up-git) and try it, even from
[your browser](http://try.github.com/).

If you are CLI-shy, try [GitHub for Mac](https://central.github.com/mac/latest).  There are several other
Mac GUI options, e.g.  [GitX](http://gitx.frim.nl/) or
[SourceTree](http://www.sourcetreeapp.com/).  GitX is flexible and works
well enough, particularly to visualize branching.  SourceTree certainly
looks glossy, however I have only toyed with it because I'm not a huge
fan of [Atlassian](http://atlassian.com/).


### Getting the right Ruby

Octopress requires Ruby v1.9.3+.  There are a number of ways to get to
v1.9.3 on the Mac: MacPorts, [Ruby Version Manager (RVM)](https://rvm.io/), [rbenv](https://github.com/sstephenson/rbenv).

Upgrading the Apple native v1.8.x is _highly_ discouraged.  Believe me.
I _know_.  I tried it, and it was _painful_ undoing what I did.


#### Ruby Version Manager

RVM seemed the best choice for me.  Being so tired after recovering my
native Ruby, I thought I could simply
{% codeblock lang:bash Bad install of RVM %}
$ sudo gem install rvm
{% endcodeblock %}
but after some issues, I uninstalled it from the native ruby environment
and followed the processes suggested on the [RVM quick install guide](https://rvm.io/rvm/install/)
{% codeblock lang:bash Better install of RVM %}
curl -L https://get.rvm.io | bash -s stable
{% endcodeblock %}
The first try, it failed with the error:
{% codeblock lang:bash Install error message %}
You requested building with 'gcc-4.2' but it is not in your path.
{% endcodeblock %}
and I discovered I had a `CC` environment variable set that pointed
elsewhere.  So an `unset CC` and `rm -rf ~/.rvm`, then the install again
was successful, however it warned me
{% codeblock lang:bash Another install error message %}
RVM is not a function, selecting rubies with 'rvm use ...' will not work.
You need to change your terminal settings to allow shell login.
Please visit https://rvm.io/workflow/screen/ for example.
{% endcodeblock %}
After checking the link, it all seemed unnecessarily complicated, but I
did verify the warning:
{% codeblock lang:bash Is rvm a function? %}
$ type rvm | head -n1
 -bash: type: rvm: not found.
{% endcodeblock %}
The was easily solved by issuing
{% codeblock lang:bash Sourcing rvm setup %}
[[ -r "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"
{% endcodeblock %}
Trying the check again,
{% codeblock lang:bash Is rvm a function yet? %}
$ type rvm | head -n1
rvm is a function
{% endcodeblock %}
things look good.  Simply adding it to your `.bash_profile` ensures it
will be loaded each time you do login.

My `rvm` install had already installed Ruby 1.9.3 selected selected it
as the default, however you can verify and ensure this by
{% codeblock lang:bash Ruby version check %}
$ ruby --version
ruby 1.9.3p194 (2012-04-20 revision 35410) [x86_64-darwin11.4.0]
$ rvm use 1.9.3
Using /Users/username/.rvm/gems/ruby-1.9.3-p194
Running /Users/username/.rvm/hooks/after_use
{% endcodeblock %}



### GitHub

First, as mentioned in all guides, sign up for a [free GitHub account](https://github.com/signup/free), and then create a repository
for as indicated for [User Pages](https://help.github.com/articles/user-organization-and-project-pages).
The repository naming scheme is `username/username.github.com`.  There
is no need to add anything to the repository, GitHub will recommend
adding a `README`.

I have yet to setup a _custom domain_, but a portion of the process is
described
[here](https://help.github.com/articles/setting-up-a-custom-domain-with-pages).


### Octopress

Clone the [Octopress repo](https://github.com/imathis/octopress/) with
{% codeblock lang:bash Cloning the Octopress repo %}
$ git clone git://github.com/imathis/octopress.git octopress.git
$ cd octopress.git  # trust the .rvmrc when asked, i.e. yes
{% endcodeblock %}
Next, install the [bundler](http://gembundler.com/) Ruby gem
{% codeblock lang:bash Install bundler via rvm %}
$ gem install bundler
$ bundler install
{% endcodeblock %}
which will installed a number of items.  Once complete, we can setup the
default _classic_ theme with
{% codeblock lang:bash %}
$ rake install
{% endcodeblock %}

This repo will hold both your content and the Octopress code.  To update
Octopress, see the [Updating Octopress](http://octopress.org/docs/updating/) guide.

### Connecting Octopress to GitHub

The [Deploying Octopress to GitHub Pages](http://octopress.org/docs/deploying/github/)
instructions clearly outline how to accomplish this.  In summary, from
the top of the `octopress.git` repo
{% codeblock lang:bash Connect repo to GitHub Page %}
$ rake setup_github_pages
{% endcodeblock %}
answering the questions as required, i.e., repo url is
`git@github.com:username/username.github.com.git`.  Then,
{% codeblock lang:bash Generate pages and publish to GitHub Pages %}
$ rake generate # generate the content from markdown
$ rake deploy   # copy the content to be deployed
{% endcodeblock %}
Commit and push your changes
{% codeblock lang:bash Commit changes %}
$ git add .
$ git commit -am 'initial import' # a very poor commit message :(
$ git push origin source
{% endcodeblock %}
The last line pushes _source_ to the _master_ branch of your GitHub repo.

### Waiting ...

Lastly comes the waiting.  GitHub recommends about 10 minutes.  My
experience is that it take 1-5 min to receive the e-mail that the
page(s) have been created, and 10-15 min for the site to appear
initially.  Afterwards, content appears much more quickly, at the 1-5
min range.

## Blogging

Finally, you are ready to generate content.  The [Octopress Blogging Basics](http://octopress.org/docs/blogging/) page enumerate the helper
functions and process to get your content to your GitHub repo.

So far, I have found the `rake preview` version useful.  In one
`Terminal.app` tab, I invoke
{% codeblock lang:bash Start preview on localhost %}
$ rake preview  # start local web server
{% endcodeblock %}
while in another, invoke
{% codeblock lang:bash Start change watcher for localhost %}
$ rake watch    # auto-regen on change
{% endcodeblock %}
while editing markdown in a third.  I verify my blog changes
via browser on `localhost:port`.  The port will be
listed on one of the first few `INFO` lines after _preview_ startup
{% codeblock lang:bash Finding the localhost port %}
$ rake preview
[2012-09-08 21:53:52] INFO  WEBrick 1.3.1
[2012-09-08 21:53:52] INFO  ruby 1.9.3 (2012-04-20) [x86_64-darwin11.4.0]
[2012-09-08 21:53:52] INFO  WEBrick::HTTPServer#start: pid=77869 port=4000
{% endcodeblock %}
and voil&agrave;, we see `port=4000`, so `http://localhost:4000` should
do it.


## Conclusion

This was a straightforward process, once I thought more carefully about
order of operations.  I also, unfortunately, messed up my repo to start
due to a typo, which caused my _source_ to push to a _source_ branch in
GitHub, rather than _master_.  This caused me no end of heartache as I
waited for my pages to be created, but of course they weren't because
there was no master branch.  After a few repo deletes, and typing
correctly, it finally worked.  Personally, I hope you have less trouble.
