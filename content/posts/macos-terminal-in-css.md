---
date: "2018-07-25"
title: "Sick and tired of terminal screenshots?"
tags: [ "hugo", "techblog" ]
subscribe: true
comments: true
share: true
image: "macos-terminal.png"
---

When you blog about technology, you have to explain a lot of stuff you do on the command line. I never really found a good way of illustrating what you do on the command line in a blog post. So I have built a solution myself.

<!--more-->

You'll agree that screenshots are not a good solution, because then your readers can't copy-paste the commands. [Highlight.js](https://highlightjs.org) is a good solution for syntax highlighting, but it does not support command line syntax (yet). 

Until I find someting better, I have created my own solution with HTML and CSS. It looks pretty neat, it is really easy to manage and it loads in the blink of a eye. 

{{< terminal "~/Sites/jiridj.be" >}}
$ ls -l ~
total 40
drwx------+  8 jiri  staff    272 Mar 21 14:30 Desktop
drwx------+ 11 jiri  staff    374 Mar 21 16:47 Documents
drwx------+ 10 jiri  staff    340 Mar 22 13:36 Downloads
drwx------@ 70 jiri  staff   2380 Mar 15 12:44 Library
drwx------+  8 jiri  staff    272 Feb 14 04:54 Movies
drwx------+  5 jiri  staff    170 Oct 19 17:07 Music
drwx------+  9 jiri  staff    306 Feb  3 10:26 Pictures
drwxr-xr-x+  5 jiri  staff    170 Oct 19 14:23 Public
$ _
{{< /terminal >}}

## Again, why did you build this?

As far as I know there are two ways that are commonly used to illustrate command line actions. And I don't like either way. 

A lot of people use screenshots. But screenshots come with a lot of downsides: 

- They have **limited real estate**, so you can show only so much. 
- They make your page **slower to load**. 
- Worst of all, your readers **can't copy-paste commands from a screenshot**.

A really good solution for syntax highlighting is [Highlight.js](https://highlightjs.org). Unfortunately highlight.js has **no support for command line syntax**. Its bash support comes close, but it really isn't meant for this. 

That's when I decided to create my own solution. I got the inspiration from a blog post on [creating a Mac Terminal lookalike in CSS](http://www.codechewing.com/library/mac-terminal-shell-css-html). I refined the MacOS titlebar looks with tips I got from a pen on [creating an OSX window with CSS](https://codepen.io/JohJakob/pen/YPxgwo). **Kudos to Peter and Jakob!**

## How to get it?

The code behind the example above is really simple. It's just a few CSS-styled ```<div>```'s, ```<a>```'s and ```<li>```'s. Each line in the terminal is actually an entry in an unordered list.

You can obviously embed this in any web page, but since I use the [Hugo static site generator](https://gohugo.io), I've created a shortcode to make it really easy. The shortcode has been written in such a way that you can simply copy and paste the output of your terminal between the shortcode start and end tag. 

You can get the html, css and hugo shortcode from GitHub: [Hugo shortcode for MacOS Terminal](https://github.com/jiridj/hugo-macos-terminal). Have fun! :smile:

## Isn't life beautiful?

{{< terminal "~/southpark" >}}
$ ./print.sh
   _O_        _____         _<>_          ___  
 /     \     |     |      /      \      /  _  \
|==/=\==|    |[/_\]|     |==\==/==|    |  / \  |
|  O O  |    / O O \     |   ><   |    |  |"|  |
 \  V  /    /\  -  /\  ,-\   ()   /-.   \  X  /
 /'---'\     /'---'\   V( '-====-' )V   /'---'\
 O'_:_'O     O'M|M'O   (_____:|_____)   O'_|_'O 
  -- --       -- --      ----  ----      -- --   
$ _
{{< /terminal >}}