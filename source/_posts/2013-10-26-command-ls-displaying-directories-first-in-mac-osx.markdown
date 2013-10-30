---
layout: post
title: "Displaying directories first in Mac OSX"
date: 2013-10-26 08:35
comments: true
categories: mac unix compatibility terminal brew
---
I'm a linux user which recently moved to Mac. Most of the time I'm using the Terminal application
and something I really miss in the commad **`ls`** of Mac is that it does not have
the option **`--group-directories-first`**.

    $ ls --group-directories-first
    /bin/ls: illegal option -- -


Installing commands from coreutils
----------------------------------
First of all, you need to install the command  **`ls`** from coreutils, what is the same package that
runs in all common linux distributions. You can use **`brew`** you install **`coreutils`**:

    $ brew install coreutils

By default, all the commands will be installed using the prefix "g" so now you have the following:

    $ gls --group-directories-first
    
If you, like me, want to always use the standard **`ls`** command from coreutils, you can add the following
alias at your **`$HOME/.bashrc`** file:

    alias ls='gls --color=auto --group-directories-first'
