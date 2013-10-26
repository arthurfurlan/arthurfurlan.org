---
layout: post
title: "Converting plaintext files using VIM"
date: 2013-09-09 21:33
comments: true
categories: vim unix dos debian ubuntu terminal
---
I work with mixed environments: some people using Windows, some people using Linux (or Mac).
If you are in the same situation, a common scenario is to be working on a remote linux server
and to find a file in **DOS** format, or running a `git pull` command and receiving a file in
this format from someone who uses Windows.


Converting the file format
--------------------------

If you have the [tofrodos](http://packages.ubuntu.com/tofrodos) package installed, this problem
is easily solved with `fromdos` command ... but if you don't, you can use **vim** to convert the
format by simply openning the file, setting the [file format](http://vim.wikia.com/wiki/File_format)
and then saving it:

    :set ff=unix
    :wq

and that's it, now the file os converted to unix format.


Converting the file encoding
----------------------------

Another great feature of vim and which also saves lots of time is: *encoding conversion*. As
I live in Brazil, it's common to find **ISO-8859-1** files and when it happens, converting it
back to **UTF-8** is as simple as openning the file on vim, setting the file encoding and
saving it:

    :set fenc=utf-8
    :wq

Actually, I'm used to convert file encodings using vim, but the file format I just discovered this
week and it saved a lot of time. It's nice to see how usefull one single tool can be! :)
