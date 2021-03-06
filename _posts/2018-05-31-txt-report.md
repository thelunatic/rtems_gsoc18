---
layout : post
title : Text Report of Coverage analysis
comments : true
author : Vijay K. Banerjee (thelunatic)
---

Hello Everyone!

My last post showed the html reports generated from the coverage script and covoar.
In this post I will be showing little exerpts from the text reports to show how they look
like.

`Note:` I'm running coverage on samples/ for score

The reports can be found in the directory where the coverage is being run, it's very
easy to browse through all the reports from the html generated by the coverage script.

-----------------------------------

##### _summary.txt_

```
Bytes Analyzed           : 28312
Bytes Not Executed       : 15192
Percentage Executed      : 46.34
Percentage Not Executed  : 53.66
Uncovered ranges found   : 263
Total branches found     : 600
Uncovered branches found : 192
   79 branches always taken
   113 branches never taken
```
This is the summary of the reports, the main page of the html parses this data to show the
percentages and other values through html table.

-----------------------------------

##### _uncovered.txt_

In the last post we saw an image of the html coverage report with the
Symbols, Range, File name, Size, classification, and an explanation when it is not referenced.

This coverage report is parsed from the uncovered.txt text file which looks something like this.

```
============================================
Index                : 1
Symbol               : TOD_TICKS_PER_SECOND_method (0x4001a8f0)
Starting Line        : coretodtickspersec.c:28 (0x4001a8f0)
Ending Line          : coretodtickspersec.c:28 (0x4001a917)
Size in Bytes        : 40
Size in Instructions : 10

Classification: NONE

Explanation:
No Explanation
============================================
============================================
Index                : 2
Symbol               : _API_Mutex_Is_owner (0x40006768)
Starting Line        : apimutexisowner.c:25 (0x40006768)
Ending Line          : apimutexisowner.c:26 (0x4000677b)
Size in Bytes        : 20
Size in Instructions : 5

Classification: NONE

Explanation:
No Explanation
============================================
============================================
Symbol        : _Bitfield_Leading_zeros

          *** NEVER REFERENCED ***

This symbol was never referenced by an analyzed executable.
Therefore there is no size or disassembly for this symbol.
This could be due to symbol misspelling or lack of a test for
this symbol.
\============================================
```
We can see above that the Symbol that was never referenced, shows an explanation and shows 
`*** NEVER REFERENCED ***`

-----------------------------------------

##### _annoted.txt_

This is the disassemply which is annoted with `NOT EXECUTED` , `ALWAYS TAKEN` and 
`NEVER TAKEN`
which lines were executed.

```
40006c84 <_Heap_Initialize>:

{

40006c84:	9d e3 bf 98 	save  %sp, -104, %sp

  Heap_Block *first_block = NULL;

40006c88:	c0 27 bf f8 	clr  [ %fp + -8 ]

{

40006c8c:	ba 10 00 18 	mov  %i0, %i5

  if ( page_size == 0 ) {

40006c90:	80 a6 e0 00 	cmp  %i3, 0

40006c94:	02 80 00 0c 	be  40006cc4 <_Heap_Initialize+0x40>
          <== NEVER TAKEN
40006c98:	c0 27 bf fc 	clr  [ %fp + -4 ]

  if ( remainder != 0 ) {

40006c9c:	82 8e e0 07 	andcc  %i3, 7, %g1

40006ca0:	02 80 00 05 	be  40006cb4 <_Heap_Initialize+0x30>
          <== ALWAYS TAKEN
40006ca4:	80 a6 e0 07 	cmp  %i3, 7

    return value - remainder + alignment;

40006ca8:	b6 06 e0 08 	add  %i3, 8, %i3
                              <== NOT EXECUTED
40006cac:	b6 26 c0 01 	sub  %i3, %g1, %i3
                            <== NOT EXECUTED
    if ( page_size < CPU_ALIGNMENT ) {

40006cb0:	80 a6 e0 07 	cmp  %i3, 7
                                   <== NOT EXECUTED
40006cb4:	18 80 00 06 	bgu  40006ccc <_Heap_Initialize+0x48>
         <== ALWAYS TAKEN
40006cb8:	82 10 20 10 	mov  0x10, %g1

      return 0;

40006cbc:	81 c7 e0 08 	ret
                                          <== NOT EXECUTED
40006cc0:	91 e8 20 00 	restore  %g0, 0, %o0
                          <== NOT EXECUTED
    page_size = CPU_ALIGNMENT;

40006cc4:	b6 10 20 08 	mov  8, %i3
                                   <== NOT EXECUTED
  uintptr_t remainder = value % alignment;

40006cc8:	82 10 20 10 	mov  0x10, %g1
                                <== NOT EXECUTED
40006ccc:	81 80 20 00 	wr  %g0, %y

40006cd0:	01 00 00 00 	nop

40006cd4:	01 00 00 00 	nop

40006cd8:	01 00 00 00 	nop

40006cdc:	84 70 40 1b 	udiv  %g1, %i3, %g2

40006ce0:	84 58 80 1b 	smul  %g2, %i3, %g2

  if ( remainder != 0 ) {

40006ce4:	82 a0 40 02 	subcc  %g1, %g2, %g1

40006ce8:	02 80 00 04 	be  40006cf8 <_Heap_Initialize+0x74>
          <== ALWAYS TAKEN
40006cec:	b8 10 20 10 	mov  0x10, %i4

    return value - remainder + alignment;

40006cf0:	b8 06 e0 10 	add  %i3, 0x10, %i4
                           <== NOT EXECUTED
40006cf4:	b8 27 00 01 	sub  %i4, %g1, %i4
                            <== NOT EXECUTED
  area_ok = _Heap_Get_first_and_last_block(

40006cf8:	9a 07 bf fc 	add  %fp, -4, %o5

40006cfc:	98 07 bf f8 	add  %fp, -8, %o4

40006d00:	96 10 00 1c 	mov  %i4, %o3

40006d04:	94 10 00 1b 	mov  %i3, %o2

40006d08:	92 10 00 1a 	mov  %i2, %o1

40006d0c:	7f ff ff b6 	call  40006be4 <_Heap_Get_first_and_last_block>

40006d10:	90 10 00 19 	mov  %i1, %o0

  if ( !area_ok ) {

40006d14:	80 a2 20 00 	cmp  %o0, 0

40006d18:	02 bf ff e9 	be  40006cbc <_Heap_Initialize+0x38>
          <== NEVER TAKEN
40006d1c:	94 10 20 68 	mov  0x68, %o2
```
In the Symbol _HEAP_Initialize we can see the three annotations to show which lines were
not executed. 

-----------------------------------------------

##### _SymbolSummar.txt_

In the beginning we saw a summary of all the symbols together. This one shows the 
symbolwise summary which looks something like this.

```
============================================
Symbol                            : TOD_TICKS_PER_SECOND_method
Total Size in Bytes               : 40
Total Size in Instructions        : 10
Total number Branches             : 0
Total Always Taken                : 0
Total Never Taken                 : 0
Percentage Uncovered Instructions : 100.00
Percentage Uncovered Bytes        : 100.00
============================================
============================================
Symbol                            : _API_Mutex_Is_owner
Total Size in Bytes               : 24
Total Size in Instructions        : 6
Total number Branches             : 0
Total Always Taken                : 0
Total Never Taken                 : 0
Percentage Uncovered Instructions : 83.33
Percentage Uncovered Bytes        : 83.33
============================================
============================================
Symbol                            : _API_Mutex_Lock
Total Size in Bytes               : 48
Total Size in Instructions        : 12
Total number Branches             : 1
Total Always Taken                : 0
Total Never Taken                 : 0
Percentage Uncovered Instructions : 0.00
Percentage Uncovered Bytes        : 0.00
============================================
============================================
Symbol                            : _API_Mutex_Unlock
Total Size in Bytes               : 48
Total Size in Instructions        : 12
Total number Branches             : 1
Total Always Taken                : 0
Total Never Taken                 : 0
Percentage Uncovered Instructions : 0.00
Percentage Uncovered Bytes        : 0.00
============================================
============================================
.
.
```
------------------------------------------

Other than the above there are two more txt reports, sizes.txt and ExplanationsNotFound.txt
The sizex.txt looks very messy, it's better to refer to the html report where it's nicely
shown with proper table.

Thank you for stopping by! 
