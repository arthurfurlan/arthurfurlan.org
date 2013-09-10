---
layout: post
title: "Converting plaintext files using VIM"
date: 2013-09-09 21:33
comments: true
categories: vim unix dos debian ubuntu
---
I work with mixed environments: some people using Windows, some people using Linux (or Mac).
If you are in the same situation, a common scenario is to be working on a remote linux server
and to find a file in **DOS** format, or running a `git pull` command and receiving a file in
this format from someone who uses Windows.


Converting the file format
--------------------------

If you have the [tofrodos](http://packages.ubuntu.com/tofrodos) package installed, this problem
is easily solved with `fromdos` command ... but if you don't, you can use the vim to convert the
format by simply openning the file on it and setting the [file format](http://vim.wikia.com/wiki/File_format):

    :set ff=unix

and that's it, the file is converted to unix format.


Converting the file encoding
----------------------------

Another great feature of vim and which also saves lots of time is the encoding conversion. As
I'm from Brazil, it's common to find **ISO-8859-1** files and when it happens, converting it
back to **UTF-8** is as simple as openning the file on vim and setting the file encoding:

    :set fenc=utf-8

I'm used to convert file encodings using vim, but the file format I just discovered this week.
It's nice to see how usefull one single tool can be! :)
