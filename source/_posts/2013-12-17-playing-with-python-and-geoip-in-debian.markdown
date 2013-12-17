---
layout: post
title: "Playing with Python and GeoIP in Debian"
date: 2013-12-17 11:25
comments: true
categories: python, debian, geoip, network
---
Sometime ago I needed to find out the origin country of an hostname (actually a list of hostnames). As
Debian has a GeoIP database available via aptitude, I could accomplish that using this database and the
Python's GeoIP module.

First of all I installed the required packages:

    $ aptitude install geoip-database python-geoip


And used the following small script that configures the Python's GeoIP module to use the Debian's GeoIP database:

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    #
    # written by Arthur Furlan <afurlan@afurlan.org>

    import re
    import sys
    import GeoIP

    ## oops, check the usage! :)
    if len(sys.argv) != 2:
        print 'Usage: %s ADDRESS' % sys.argv[0]
        sys.exit(1)

    ## geoip database from "geoip-database" debian package
    GEOIP_DATABASE = '/usr/share/GeoIP/GeoIP.dat'
    geoip = GeoIP.open(GEOIP_DATABASE, GeoIP.GEOIP_STANDARD)

    ## get the country name based on the given address
    if re.match('^[0-9]{1,3}(\.[0-9]{1,3}){3}$', sys.argv[1]):
        response = geoip.country_name_by_addr(sys.argv[1])
    else:
        response = geoip.country_name_by_name(sys.argv[1])

    ## print the response if there is any response
    if response:
        print response


Some tests to check if it is really working... and looks like it is. :)

    $ python address_country.py configr.com
    Brazil
    $ python address_country.py debian.org
    United States
    $ python address_country.py mandriva.com
    France
    $ python address_country.py some-nonexistent-domain.org
    $
