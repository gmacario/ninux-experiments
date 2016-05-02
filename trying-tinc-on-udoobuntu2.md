# Trying TINC on UDOObuntu2 on UDOO Neo Full

Prerequisites:

* One UDOO NEO Full connected to Internet 
* UDOObuntu2 installed

Login to udooneo-gm via Remote Terminal (i.e. browse http://100.84.248.76:8000/)

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
