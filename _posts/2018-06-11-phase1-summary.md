---
layout : post
title : Summarizing Phase 1
comments : true
author : Vijay K. Banerjee (thelunatic)
---
Hello everyone!

Today I'm going to summarize the works done during the whole Phase 1 and today
is the phase 1 deadline. It was really amazing to work with such a helpful and
supportive community. Everyday was filled with unique challenges and each of 
them brought new direction and ideas to the project. Each line of the code had
to be carefully written and upto the coding standards, just making it work isn't
enough, it had to be made sure that the produced code doesn't break something that
works fine. The feedback and suggestions from the mentors always helped me
understand the issues in the code and how to solve those without breaking
something.

---------
##### History

The objective of the phase one was to complete the project of adding a script to
the tester that generate html coverage analysis reports with the output
generated from covoar. Two students have worked before me in the project. 
Krzysztof Miesowicz started this in 2014 and brought the concept of a coverage
script to generate an html summary of the covoar reports. It was then continued
by Cillian O'Donnell (Who is one of my mentors ) who integrated Couverture-Qemu to
rtems and also reworked a lot of portions in the script to parse the config
files and run covoar from the script. This year I picked up the project where 
Cillian left and finally got it merged ! 

------

##### Technical details of the Project

All the works of phase 1 has been commited to RTEMS-TOOLS master repo.
The commit can be found in this [link.](https://github.com/thelunatic/rtems-tools/commit/b762312fae672e1ae8b47e4581f445020d47245f)

The patch adds coverage support to the tester, when the tester is run with a
supported bsp, then it will run coverage for it and generate an html report with
the summary of the covoar output for each symbol or subsystem.

Suppose the bsp we're running for is `leon3-qemu` then the config file for the bsp with
coverage support is leon3-qemu-cov. the covoar output will be stored in
`leon3-qemu-coverage/` directory under the directory where the test is run. The
html coverage summary can be found in leon3-qemu-reports.html

---

##### What's next

The covoar can generate reports for one symbol properly, we take that as our
baseline and move towards the next part of the project. Now that we have html
coverage reports the next part of the project is to add support in covoar to
generate gcov/lcov report. The approach is like this.

* Compile with gcc flag -ftest-coverage that generates the .gcno file.
* Instrumentation of the code by covoar, then dump it in .gcda files.
* Run gcov/lcov to generate reports with the note files.
* Wrtie script to automate the running of lcov to generate html report.

---

###### Thanks to my mentors Dr. Joel Sheryll, Chris Jhons and Cillian O'Donnel for guiding and helping me throughout the phase.
