---
layout: post
title: "Using IPython as your default shell"
date: 2009-10-29 11:47
comments: true
categories: python ipython bash shell linux sysadmin
---
If you are a shell addicted person and like [Python](http://python.org), then the [IPython](http://ipython.org)
was made just for you. The IPython
provides a very usefull feature (that may look a bit strange at first) of mixing Python and Shell commands
in a easy and intuitive way. I don't pretend to say why you should use IPython instead of your current shell
but I believe that if you know Python, you should prefer to write Python code instead of Bash code.

I'll assume that you already have the IPython installed, but if you don't take a look at
[IPython's documentation to see how to install it](http://ipython.org/install.html). I'm running Debian, so
this setup is focused on it. It should work for the most of the others linux distros but if you are running
a different system, I'm sorry but you may have to adapt some commands and/or paths. :)

Configuring the IPython's prompt
--------------------------------

The first time you run IPython, it displays a warning about the creation of your personal configuration directory.
One of the most important parts of this warning is about the new configuration file: `~/.ipython/ipy_user_conf.py`.
So let's configure this file and the IPython's prompt to make it looks exactly like the Debian's prompt. Edit your
configuration file and change the following settings as below:

    ...
    import ipy_profile_sh
    ...
    o.prompt_in1 = r'\C_Normal\u@\H:\Y2$ '
    o.prompt_in2 = r'\C_Normal... '
    ...

The first option, `import ipy_profile_sh`, avoid you to have to escape all the Bash commands. The second and
third options, `o.prompt_in1` and `o.prompt_in2`, change the IPython's prompt. And now start the IPython as follow:

    afurlan@wetzel:~$ ipython -nosep -nobanner -noconfirm_exit
    afurlan@wetzel:~$
    afurlan@wetzel:~$ 
    afurlan@wetzel:~$ print 'hello python!'
    hello python!
    afurlan@wetzel:~$ echo 'hello bash!'
    hello bash!


Great, now you're able to run Python commands in your iPython shell:

    afurlan@wetzel:~$ for line in file('domains.txt'):
                  ...     print line
                  ...    
                  ...    
    arthurfurlan.org
    
    configr.com

And a mixed of Python and Bash commands:

    afurlan@wetzel:~$ for line in file('domains.txt'):
                  ...     echo "$line"
                  ...    
                  ...    
    arthurfurlan.org
    
    configr.com

    afurlan@wetzel:~$ for line in file('domains.txt'):
              ...     echo "$line.strip()"
              ...    
              ...    
    arthurfurlan.org
    configr.com


Setting the IPython as your default shell
-----------------------------------------

Actually I don't like to set the IPython as my default shell... I use to run screen so I prefer to configure it to open five IPython sessions by default, but if you really like to set it as your default shell, you can add the following line at the end of your ~/.bashrc file:

    ...
    exec ipython -nosep -nobanner -noconfirm_exit


If you're a screen user like me, you can add the following lines at your ~/.screenrc:

    ...
    ## open 5 ipython sessions by default
    screen -t p 1 ipython -nosep -nobanner -noconfirm_exit
    screen -t p 2 ipython -nosep -nobanner -noconfirm_exit
    screen -t p 3 ipython -nosep -nobanner -noconfirm_exit
    screen -t p 4 ipython -nosep -nobanner -noconfirm_exit
    screen -t p 5 ipython -nosep -nobanner -noconfirm_exit
    ...

Or, if you like, you can also get my current [.screenrc](https://github.com/arthurfurlan/personal/blob/master/.screenrc) file.
