---
layout: post
title: "The right Path : Getting path to build-directory"
comments: true
author: thelunatic
---

Hello everyone !

This is still the first week going and a lot of interesting stuffs are going in the project ! 
While working with the previous GSoC project along with my mentors to fix the issues, 
we came up with a very interesting problem. Basically I got it running again by parsing the 
bsp ini file from the script. After giving a good amount of time in understand the codebase 
and making addition to it for the parsing, it was really a great feeling to see it runnin and 
it felt like we can get it merged with the tester much before the phase 1 deadline and we can 
give more time to the gcov generation which cetainly demands a good amount of time and focus.

But wait ...

Here's some thing interesting. The rtems tester runs the tests with the following command :

```bash
$HOME/development/rtems/test/rtems-tools/tester/rtems-test --rtems-tools=$HOME/development/rtems/5 \
--log=coverage_analysis.log --rtems-bsp=leon3_qemu \
$HOME/development/rtems/kernel/leon3/sparc-rtems5/c/leon3/testsuites/samples
```

After the updates to the code to include the coverage and parsing of the code using the 
previous GSoC project, It would look like this

without coverage:
```bash
$HOME/development/rtems/test/rtems-tools/tester/rtems-test --rtems-tools=$HOME/development/rtems/5 \ 
--log=coverage_analysis.log --rtems-bsp=leon3_qemu \
--rtems-builddir=$HOME/development/rtems/kernel/leon3 \
sparc-rtems5/c/leon3/testsuites/samples
```
with coverage:
```bash
$HOME/development/rtems/test/rtems-tools/tester/rtems-test --rtems-tools=$HOME/development/rtems/5 \ 
--log=coverage_analysis.log --rtems-bsp=leon3_qemu --coverage \
--rtems-builddir=$HOME/development/rtems/kernel/leon3 \
sparc-rtems5/c/leon3/testsuites/samples
```

Did you spot the difference there?

Apart from and addition of the `--coverage` option, we made another difference in the command 
addition of `--rtems-builddir` option. It surely made the job simple for us as we could 
take the path to the build directory from the user but it changed the way how the tester works!
This would create so much confusion in whole userbase, it would need updating all the
documentations and manuals and still there would be so much confusions for the users
who would see a sudden change in the command line arguments of the tool they had been
using for long.

A very good lesson was learnt from this is that the user interface should not be compromised
for the ease of fixing an issue.

We got back to work, which followed a series of updates to covoar and the coverage script.
And then we arrived at a solution where only the addition of `--coverage` options makes
it work.

I'll be posting on the working of the coverage soon.

Thanks for stopping by!

