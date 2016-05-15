# Trying TINC on UDOObuntu2 on UDOO NEO Full

Prerequisites:

* One [UDOO NEO Full](http://www.udoo.org/udoo-neo/) connected to Internet via Ethernet
* Booting from Micro SD Card written from file `udoobuntu-udoo-neo-desktop_2.0rc2.img`

Login to udooneo-gm via Remote Terminal (i.e. browse http://100.84.248.76:8000/) - or via the [serial console](http://gmacario.github.io/howto/udoo/neo/embedded/software/development/2015/11/08/connecting-to-udoo-neo-serial-console.html)

Logged as udooer@udooneo-gm

```
$ sudo apt-get update && sudo apt-get -y dist-upgrade
$ sudo apt-get -y install tinc
```

Verify the correct installation of tinc

```
$ dpkg -l tinc
$ dpkg -L tinc
```

TODO

<!-- EOF -->
