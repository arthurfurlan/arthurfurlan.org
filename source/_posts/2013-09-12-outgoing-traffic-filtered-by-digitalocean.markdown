---
layout: post
title: "Outgoing traffic filetered by DigitalOcean!?"
date: 2013-09-12 01:05
comments: true
categories: sysadmin firewall network mail
---
I usually host my machines on [Linode](http://www.linode.com/?r=3ce91ceda1f3059c009e913fe993fd0ef39601d8)
but today I helped a friend of mine to configure his brand new server on **DigitalOcean**.

We were using [Configr](http://configr.com) to provide the services deployment and just
after the initial configuration, we setup *Mandrill Add-On* in order to improve
the email deliverability rate. Everything configured and properly deployed, so it's
time to test the environment... and we got no emails delivered. =/

The error message from exim log was:

    routing defer (-51): retry time not reached

Going deeper on the problem, we double checked that we had no firewall rules being
applied in our server but we noticed that we still weren't able to connect with [Mandill](http://mandrillapp.com)
servers:

    $ telnet smtp.mandrillapp.com 587
    Trying 54.235.146.179...
    Trying 54.234.14.176...
    Trying 54.235.146.152...
    Trying 50.16.10.62...
    telnet: Unable to connect to remote host: Connection timed out

How is it possible? Every other well-known network ports was working correctly...
So looks like someone is filtering our outgoing traffic.

After some time spent with support tickets on [Digital Ocean]( https://www.digitalocean.com/?refcode=5d44b3372429)
and more tests asked by support team, we got this final answer from them:

> Greetings,
> It appears that your account was mistakenly blocked by our backend system after some automated abuse triggers. The abuse triggers erroneously marked your account as a spam account.
> I apologise deeply for this inconvenience. The block has been removed and full connectivity should be restored.
> Please let me know if you have any more questions.

That said, our emails started to be delivery *automagically*... What great initial
user experience huh!?
