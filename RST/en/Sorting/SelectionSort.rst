.. This file is part of the OpenDSA eTextbook project. See
.. http://opendsa.org for more details.
.. Copyright (c) 2012-2020 by the OpenDSA Project Contributors, and
.. distributed under an MIT open source license.

.. avmetadata::
   :title: Selection Sort
   :author: Cliff Shaffer
   :institution: Virginia Tech
   :requires: sorting terminology; comparison; bubble sort
   :satisfies: selection sort
   :topic: Sorting
   :keyword: Sorting; Selection Sort
   :naturallanguage: en
   :programminglanguage: N/A
   :description:  Presentation of Selection Sort including visualizations, code, and self-test questions and exercises.

.. index:: ! Selection Sort


Selection Sort
==============

Selection Sort
--------------

Consider again the problem of sorting a pile of phone bills for the
past year.
Another intuitive approach might be to look through the pile until you
find the bill for January, and pull that out.
Then look through the remaining pile until you find the bill for
February, and add that behind January.
Proceed through the ever-shrinking pile of bills to select the next
one in order until you are done.
This is the inspiration for
our last :math:`\Theta(n^2)` sort,
called :term:`Selection Sort`.
The :math:`i`'th pass of Selection Sort "selects" the :math:`i`'th
largest key in the array, placing that record at the end of the array.
In other words, Selection Sort first finds the largest key in an
unsorted list, then the next largest, and so on.
Its unique feature is that there are few record swaps.
To find the next-largest key value requires searching through
the entire unsorted portion of the array, but only one swap is
required to put the record into place.
Thus, the total number of swaps required will be :math:`n-1`
(we get the last record in place "for free").

Here is an implementation for Selection Sort.

.. codeinclude:: Sorting/Selectionsort 
   :tag: Selectionsort

Consider the example of the following array.

.. inlineav:: selectionsortS1CON ss
   :long_name: Selection Sort First Pass
   :links: 
   :scripts: AV/Sorting/selectionsortS1CON.js
   :output: show
   :keyword: Sorting; Selection Sort

Now we continue with the second pass.
However, since the largest record is already at the right end,
we will not need to look at it again.

.. inlineav:: selectionsortS2CON ss
   :long_name: Selection Sort Second Pass
   :links: 
   :scripts: AV/Sorting/selectionsortS2CON.js
   :output: show
   :keyword: Sorting; Selection Sort

Selection Sort continues in this way until the entire array is sorted.

The following visualization puts it all together.

.. avembed:: AV/Sorting/selectionsortAV.html ss
   :long_name: Selection Sort Visualization
   :keyword: Sorting; Selection Sort

Now try for yourself to see if you understand how Selection Sort works.

.. avembed:: Exercises/Sorting/SelsortPRO.html ka
   :long_name: Selection Sort Proficiency Exercise
   :keyword: Sorting; Selection Sort


Selection Sort Analysis
-----------------------

Any algorithm can be written in slightly different ways.
For example, we could have written Selection Sort to find the smallest
record, the next smallest, and so on.
We wrote this version of Selection Sort to mimic the behavior of our
Bubble Sort implementation as closely as possible.
This shows that Selection Sort is essentially a Bubble Sort
except that rather than repeatedly swapping adjacent values to get
the next-largest record into place, we instead remember the position
of the record to be selected and do one swap at the end.

This visualization analyzes the number of
comparisons and swaps required by Selection Sort.

.. inlineav:: SelectionSortAnalysisCON ss
   :long_name: Selection Sort Analysis Slideshow
   :links: AV/Sorting/SelectionSortAnalysisCON.css
   :scripts: AV/Sorting/SelectionSortAnalysisCON.js
   :output: show
   :keyword: Sorting; Selection Sort

Pointer Swapping
----------------

.. _PointerSwap:

.. inlineav:: ptrSwapCON ss
   :long_name: Pointer Swap Optimization Slideshow
   :links: AV/Sorting/ptrSwapCON.css
   :scripts: AV/Sorting/ptrSwapCON.js
   :output: show
   :keyword: Sorting; Selection Sort

Here are some review questions to check how well you understand
Selection Sort.

.. avembed:: Exercises/Sorting/SelsortSumm.html ka
   :long_name: Selection Sort Summary Exercise
   :keyword: Sorting; Selection Sort
