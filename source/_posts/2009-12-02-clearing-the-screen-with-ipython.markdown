---
layout: post
title: "Clearing the screen with IPython"
date: 2009-12-02 12:20
comments: true
categories: python, ipython, bash, shell, clear
---
Some time ago I [changed my default shell to use IPython](#) instead of Bash. The [IPython](http://ipython.org) is a
really great as a shell and IMHO has great advantages but for those who, like me, are completely addicted to the `clear`
command, the IPython's clear is a huge disadvantage.

In IPython, the clear command clear varios data like input, output and directory histories but it *doesn't clear the screen*!
You can take a look at the documentation of the default function for the clear command in IPython below and see how it works:

    $ from IPython.Extensions.clearcmd import clear_f
    $ print clear_f.__doc__
     Clear various data (e.g. stored history data)

        %clear out - clear output history
        %clear in  - clear input history
        %clear shadow_compress - Compresses shadow history (to speed up IPython)
        %clear shadow_nuke - permanently erase all entries in shadow history
        %clear dhist - clear dir history

So I created a new function to extend the first one by adding the option to clear the screen when no args were passed. If
you'd like to do the same, just add the following lines in your `~/.IPython/ipy_user_conf.py`:

    def new_clear_f(*args, **kwargs):
        ''' Extend the default clear function adding the option to
        clear the screen when no args were passed.'''
        if not args[1]:
            ip.system('clear')
        else:
            from IPython.Extensions.clearcmd import clear_f
            clear_f(*args, **kwargs)
            ip.expose_magic('clear', new_clear_f)
    ip.expose_magic('clear', new_clear_f)

And now it all seems to be the standard clear again. :)
