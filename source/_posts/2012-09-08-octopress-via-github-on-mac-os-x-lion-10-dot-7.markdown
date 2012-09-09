---
layout: post
title: "Octopress via GitHub on Mac OS X Lion (10.7)"
date: 2012-09-08 19:04
comments: true
categories: 
---

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

Description            | Provider | Version   | Comment
Xcode                  | Apple    | 4.4.1     | build version 4F1003
CLI tools, `llvm-gcc`  | Apple    | 4.2.1     | LLVM build 2336.11.00
gcc                    | MacPorts | 4.5.4     | MacPorts gcc45 4.5.4_1
clang                  | Apple    | 4.0       | LLVM 3.1svn
ruby                   | Apple    | 1.8.7     | 2011-12-28 patchlevel 357
keychain               | MacPorts | 2.7.1_1   | 
git                    | Apple    | 1.7.9.6   | Apple Git-31.1
git                    | MacPorts | 1.7.11.5  | 
bash                   | Apple    | 3.2.48(1) | 
Terminal               | Apple    | 2.2.3     | 303.2


## Setup and pitfalls

In addition to the [Octopress
documentation](http://octopress.org/docs/setup/), there are many
excellent guides to setting up Octopress hosted via GitHub, e.g.,
- [Getting Started With Octopress](http://www.zhubert.com/blog/2012/04/26/getting-started-with-octopress/)
- [Custom Domain With Octopress and Github Pages](http://robdodson.me/blog/2012/04/30/custom-domain-with-octopress-and-github-pages/)
- [How I built my blog in one day](http://erjjones.github.com/blog/How-I-built-my-blog-in-one-day/)

Studying these guides closely provided the outline for setting up my
particularly instance.

### Git

[Git](http://git-scm.com/) is the fashionable revision control

### Ruby

Octopress requires 

### GitHub

First, as mentioned in all guides, sign up for a [free GitHub
account](https://github.com/signup/free), and then create a repository
for as indicated for [User
Pages](https://help.github.com/articles/user-organization-and-project-pages).
The repository nameing scheme is `username/username.github.com`.  As
yet, I have not yet setup a _custom domain_, but a portion of the process is described [here](https://help.github.com/articles/setting-up-a-custom-domain-with-pages).

