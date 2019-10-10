# ESXI-ipmitool
Build instructions for ipmitool static binary

These instructions will allow you to build a static ipmitool binary for 64-bit ESXi and may work for other systems as well.

The following build was completed under 64-bit Ubuntu 18.04.3 LTS but should be possible on any Linux given the buildutils are installed.

```
curl -L -o ipmitool_1.8.14.tar.gz http://http.debian.net/debian/pool/main/i/ipmitool/ipmitool_1.8.14.orig.tar.gz
tar xvf ipmitool_1.8.14.tar.gz
CC=gcc CFLAGS=-m64 LDFLAGS=-static ./configure
make
../libtool --silent --tag=CC --mode=link gcc -m64 -fno-strict-aliasing -Wreturn-type -all-static -o ipmitool.static ipmitool.o ipmishell.o ../lib/libipmitool.la plugins/libintf.la
```

Find your statically compiled file in src/ipmitool.static

Instructions adapted from Ewen McNeill's blog post at https://ewen.mcneill.gen.nz/blog/entry/2015-07-09-static-ipmitool-on-vmware-esxi/
