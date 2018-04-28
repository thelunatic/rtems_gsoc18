---
title: Building rtems-tools 
permalink: /codes/building_rtemstools/
---

The following instruntion shows how to build the rtems-tool from the master branch of RTEMS/rtems-tools.



```bash
$cd development/rtems
$mkdir test
$cd test
$git clone https://github.com/RTEMS/rtems-tools.git
 ...
$cd rtems-tools

$./waf configure --prefix=$HOME/development/rtems/5
 ...
$./waf build install


```

