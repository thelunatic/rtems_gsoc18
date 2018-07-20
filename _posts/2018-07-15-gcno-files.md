---
layout: post
title : "Note it : The gcno files"
comments: true
author: Vijay K. Banerjee (thelunatic)
---
Hello everyone!

In my previous post I have given the basic outline of the workflow that we have
planned to follow for generating the gcov coverage reports from covoar. The 
plan is interesting but certainly not that simple, there are few challenges 
in this project which are a bit difficult to tackle down. 

The very fist of the callenges is the mystery of the GCNO and the GCDA files.
According to plan, the `covoar` tool will read the gcno files along with the
qemu trace to generate the gcno files. But... The structure of the gcno file 
is still a mystery to us and without solving that mystery, it is not possible 
to go ahead with the gcov support without understanding the format of the file 
we are working with.

To deal with this we have planned to create a `GCNO_DUMPER` program to dump
the contents of the gcno files into a human readeable txt format. I have 
already started the dumper project and it can be followed in the following
repository.

[https://github.com/thelunatic/gcno_dumper](https://github.com/thelunatic/gcno_dumper)


It already produces some visible and understandable txt file, the work is
in progress and will soon (hopefully) be ready to dump the contents of any gcno
file.

In the next post I will describe each fields in the txt file that is generated so
far that will demystify the gcno mystery to some extent. 

Thank you for giving it a read! :) 
