mod_evasive_x
=============

Added some features to evasive_module to use the correct client IP when using a reverse proxy or load balancer.

Currently only 2.x version is implemented. (Works with Apache 2.4.x)

Original mod_evasive is [here](http://www.zdziarski.com/blog/?page_id=442).

Used regex library [TRex](http://sourceforge.net/projects/tiny-rex/).


Additions
---------

`DOSXForwardedForAsRemoteIP` 0 or 1. Use X-Forwarded-For as remoteIP when 1. Defaults to 0.

`DOSTargetedURL` Regular expression of target URL, e.g. example.com:80/some.path  Multiple entries requires multiple lines.

`DOSUnTargetedURL` Regular expression of untargeted URL, e.g. example.com:80/some.path  Multiple entries requires multiple lines.

`DOSLogOnly` 0 or 1. Do not return 403 if 1. Defaults to 0.


Building
--------

You must include the Trex library when compiling the Apache2 module:

`apxs -i -a -c mod_evasive24.c trex.c`

If you cannot seem to get any log output, take a look at /var/log/syslog ;)


Sample Config
-------------

```
    DOSHashTableSize   3097
    DOSPageCount        5
    DOSSiteCount        50
    DOSPageInterval     1
    DOSSiteInterval     1
    DOSBlockingPeriod   120
    DOSXForwardedForAsRemoteIP 1
    DOSEmailNotify      someone@mail.org
    DOSSystemCommand    "su - someuser -c '/sbin/... %s ...'"
    DOSLogDir           "/var/log/apache2/mod_evasive"
```
