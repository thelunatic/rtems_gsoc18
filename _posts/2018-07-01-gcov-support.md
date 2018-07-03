---
layout: post
title : Getting started with Gcov support
comments: true
author : Vijay K. Banerjee (thelunatic) 
---

Hello eveyone!

Hope you all are having good time, this post is after a long time because it
actually took me time to understand the Code for Gcov support in RTEMS and also
the workflow.

In this phase and the next phase my objective is to get Gcov reports for RTEMS
source files using the qemu traces. This actually sounds a bit over ambitious 
goal in the given time frame. But I am determined to take it as far as it goes
and then continue working on it post GSoC as well.

There has been previous attempts to do this and as told to me by my mentor
Dr. Joel Sherrill, someone did manage to generate the gcov reports at some 
point though it was not 100% correct but it was close enough. So my starting 
point is definitely where he left, but the challenge is that there had been a 
lot of changes in RTEMS since then, making the code of Gcov support a bit 
rotted.

##### Workflow of generating gcov reports in gcc

* gcc produces `gcno` files at compile time using `-ftest-coverage` flag
* gcc produces instrumentation in the `.o` files at compile time using 
  `-fprofile-arcs` flag.
* executable dumps the coverage data into gcda files at run-time
* gcov processes gcno and gcda files to produce the coverage reports.

##### An outline of our planned workflow to generate gcov reports.

* gcc generates the `.gcno` notes file at the compile time 
* covoar reads these gcno files and the trace files from qemu and
  produces the gcda files that can be processed by `gcov`.
* gcov processes gcno and gcda files to produce coverage reports.

##### Why a different approach is needed

Basically the following two factors make us choose a different path

* We don't have a way to get the information off the target environment
* covoar follows a rule to "test as you fly and fly as you test".

Considering these factors/rules we are supposed to do all test and debug on
the exact code that we deploy and hence we can't take the approach of the
compile time instrumentation of the object file by gcc.


This stuff has been under development fo quite some time and needs some good
documentations, this blog is a good place to outline everything. So I'm hoping
to come up with more technical articles soon.

Thank you for stopping by !
