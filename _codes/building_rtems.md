---
title: Building RTEMS from RSB 
permalink: /codes/building_rtems/
---

The RTEMS User Manual gives a very clear Idea of the basic set up :

[RTEMS user manual - QUick Start](https://docs.rtems.org/branches/master/user/start/index.html).

We'll use the manual to build leon3 kernel using the RSB .

**1.** Creating a workspace (avoid doing it as root) :

```bash
$ cd
$ mkdir -p development/rtems
$ cd development/rtems
$ git clone git://git.rtems.org/rtems-source-builder.git rsb
  ...
$ cd rsb
$ ./source-builder/sb-check
  ...
$ cd rtems
$ ../source-builder/sb-set-builder \
    --prefix=/usr/home/lunatic/development/rtems/5 5/rtems-sparc
  ...
```


**2.** Building the RTEMS kernel by cloning the repository and runnint the bootstrap procedure.

```bash
$ export PATH=$HOME/development/rtems/5/bin:$PATH
$ cd
$ cd development/rtems
$ mkdir kernel
$ cd kernel
$ git clone git://git.rtems.org/rtems.git rtems
  ...
$ cd rtems
$ ./bootstrap -c && $HOME/development/rtems/rsb/source-builder/sb-bootstrap
  ...
```

**2.** Building and installing the kernel 

```bash
$ cd ..
$ mkdir leon3
$ cd leon3
$ $HOME/development/rtems/kernel/rtems/configure --prefix=$HOME/development/rtems/5 \
                   --target=sparc-rtems5 --enable-rtemsbsp=leon3 --enable-posix --enable-tests
  ...
$ make -j 8
  ...
$ make install
```



