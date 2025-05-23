.. This file is part of the OpenDSA eTextbook project. See
.. http://opendsa.org for more details.
.. Copyright (c) 2012-2020 by the OpenDSA Project Contributors, and
.. distributed under an MIT open source license.

.. avmetadata::
   :title: Comparing Algorithms
   :author: Cliff Shaffer
   :institution: Virginia Tech
   :requires: problems; algorithms
   :satisfies: growth rate
   :topic: Algorithm Analysis
   :keyword: Algorithm Analysis; Growth Rate
   :naturallanguage: en
   :programminglanguage: N/A
   :description: An introduction to how algorithms are compared, including the concept of growth rates.


Comparing Algorithms
====================

Comparing Algorithms
--------------------

Introduction
~~~~~~~~~~~~

How do you compare two algorithms for solving some problem in terms
of efficiency?
We could implement both algorithms as computer programs and then
run them on a suitable range of inputs, measuring how much of the
resources in question each program uses.
This approach is often unsatisfactory for four reasons.
First, there is the effort involved in programming and testing two
algorithms when at best you want to keep only one.
Second, when empirically comparing two algorithms there
is always the chance that one of the programs was "better written"
than the other, and therefore the relative qualities of the underlying
algorithms are not truly represented by their implementations.
This can easily occur when the programmer has a bias
regarding the algorithms.
Third, the choice of empirical test cases might unfairly favor one
algorithm.
Fourth, you could find that even the better of the two algorithms does
not fall within your resource budget.
In that case you must begin the entire process again with yet another
program implementing a new algorithm.
But, how would you know if any algorithm can meet the resource budget?
Perhaps the problem is simply too difficult for any implementation to
be within budget.

These problems can often be avoided by using
asymptotic analysis.
Asymptotic analysis measures the efficiency of an algorithm, or its
implementation as a program, as the input size becomes large.
It is actually an estimating technique
and does not tell us anything about the relative merits of two
programs where one is always "slightly faster" than the other.
However, asymptotic analysis has proved useful
to computer scientists who must determine if a particular algorithm
is worth considering for implementation.

The critical resource for a program is most often its running
time.
However, you cannot pay attention to running time alone.
You must also be concerned with other factors such as the space
required to run the program (both main memory and disk space).
Typically you will analyze the *time* required for an
*algorithm* (or the instantiation of an algorithm in the form
of a program), and the *space* required for a
*data structure*.

Many factors affect the running time of a program.
Some relate to the environment in which the program
is compiled and run.
Such factors include the speed of the computer's CPU, bus, and
peripheral hardware.
Competition with other users for the computer's (or the network's)
resources can make a program slow to a crawl.
The programming language and the quality of code generated by a
particular compiler can have a significant
effect.
The "coding efficiency" of the programmer who converts the algorithm
to a program can have a tremendous impact as well.

If you need to get a program working within time and space
constraints on a particular computer, all of these factors can be
relevant.
Yet, none of these factors address the differences between
two algorithms or data structures.
To be fair, if you want to compare two programs derived from two
algorithms for solving the same problem, they should both be compiled
with the same compiler and run on the same computer under the same
conditions.
As much as possible, the same amount of care should be taken in
the programming effort devoted to each program to make the
implementations "equally efficient".
In this sense, all of the factors mentioned above should cancel
out of the comparison because they apply to both algorithms equally.

If you truly wish to understand the running time of an algorithm,
there are other factors that are more appropriate to consider than
machine speed, programming language, compiler, and so forth.
Ideally we would measure the running time of the algorithm under
standard benchmark conditions.
However, we have no way to calculate the running time reliably other
than to run an implementation of the algorithm on some computer.
The only alternative is to use some other measure as a surrogate for
running time.

Basic Operations and Input Size
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Of primary consideration when estimating an algorithm's performance
is the number of :term:`basic operations <basic operation>` required by
the algorithm to process an input of a certain size.
The terms "basic operations" and "size" are both
rather vague and depend on the algorithm being analyzed.
Size is often the number of inputs processed.
For example, when comparing sorting algorithms
the size of the problem is typically measured by the number of
records to be sorted.
A basic operation must have the property that its time to
complete does not depend on the particular values of its operands.
Adding or comparing two integer variables are examples of basic
operations in most programming languages.
Summing the contents of an array containing :math:`n` integers is not,
because the cost depends on the value of :math:`n`
(i.e., the size of the input).

.. _SeqMax:

.. topic:: Example

   Consider a simple algorithm to solve the problem of finding the
   largest value in an array of :math:`n` integers.
   The algorithm looks at each integer in turn, saving the position of
   the largest value seen so far.
   This algorithm is called the *largest-value sequential search*
   and is illustrated by the following function:

   .. codeinclude:: Misc/LargestTest
      :tag: Largest

   Here, the size of the problem is ``A.length``,
   the number of integers stored in array ``A``.
   The basic operation is to compare an integer's value to that
   of the largest value seen so far.
   It is reasonable to assume that it takes a fixed amount of time to
   do one such comparison, regardless of the value of the two
   integers or their positions in the array.

   Because the most important factor affecting running time is
   normally size of the input, for a given input size :math:`n` we
   often express the time :math:`\mathbf{T}` to  run the algorithm as
   a function of :math:`n`, written as :math:`\mathbf{T}(n)`.
   We will always assume :math:`\mathbf{T}(n)` is a non-negative
   value.

   Let us call :math:`c` the amount of time required to compare two
   integers in function ``largest``.
   We do not care right now what the precise value of :math:`c` might
   be.
   Nor are we concerned with the time required to increment
   variable :math:`i` because this must be done for each value in the
   array, or the time for the actual assignment when a larger value is
   found, or the little bit of extra time taken to initialize
   ``currlarge``.
   We just want a reasonable approximation for the time taken to
   execute the algorithm.
   The total time to run ``largest`` is therefore approximately
   :math:`cn`, because we must make :math:`n` comparisons,
   with each comparison costing :math:`c` time.
   We say that function ``largest``
   (and by extension, the largest-value sequential search algorithm for
   any typical implementation) has a running time expressed
   by the equation

   .. math::

      \mathbf{T}(n) = cn.

   This equation describes the growth rate for the running time of the
   largest-value sequential search algorithm.

.. topic:: Example

   The running time of a statement that assigns the first value of an
   integer array to a variable is simply the time required to copy the
   value of the first array value.
   We can assume this assignment takes a constant amount of time
   regardless of the value.
   Let us call :math:`c_1` the amount of time necessary to copy an
   integer.
   No matter how large the array on a typical computer
   (given reasonable conditions for memory and array size), the time
   to copy the value from the first position of the array is always
   :math:`c_1`.
   Thus, the equation for this algorithm is simply

   .. math::

      \mathbf{T}(n) = c_1,

   indicating that the size of the input :math:`n` has no effect on
   the running time.
   This is called a :term:`constant running time`.

.. topic:: Example

   Consider the following code:

   .. codeinclude:: Misc/Anal
      :tag: Analp1

   What is the running time for this code fragment?
   Clearly it takes longer to run when :math:`n` is larger.
   The basic operation in this example is the
   increment operation for variable ``sum``.
   We can assume that incrementing takes constant time;
   call this time :math:`c_2`.
   (We can ignore the time required to initialize ``sum``,
   and to increment the loop counters ``i`` and ``j``.
   In practice, these costs can safely be bundled into time
   :math:`c_2`.)
   The total number of increment operations is :math:`n^2`.
   Thus, we say that the running time is
   :math:`\mathbf{T}(n) = c_2 n^2`.

Growth Rates
~~~~~~~~~~~~

The :term:`growth rate` for an algorithm is the rate at which the cost
of the algorithm grows as the size of its input grows.
The following figure shows a graph for six equations,
each meant to describe the running time for a particular program or
algorithm.
A variety of growth rates that are representative of typical
algorithms are shown.

.. _RunTimeGraph:

.. inlineav:: GrowthRatesCON dgm
    :links: AV/AlgAnal/GrowthRatesCON.css
    :scripts: DataStructures/Plot.js AV/AlgAnal/GrowthRatesCON.js
    :align: center
   :keyword: Algorithm Analysis; Growth Rate

.. inlineav:: GrowthRatesZoomCON dgm
   :links: AV/AlgAnal/GrowthRatesZoomCON.css
   :scripts: DataStructures/Plot.js AV/AlgAnal/GrowthRatesZoomCON.js
   :align: center
   :keyword: Algorithm Analysis; Growth Rate

   Two views of a graph illustrating the growth rates for
   six equations.
   The bottom view shows in detail the lower-left portion
   of the top view.
   The horizontal axis represents input size.
   The vertical axis can represent time, space, or any other measure of
   cost.

The two equations labeled :math:`10n` and :math:`20n` are graphed by
straight lines.
A growth rate of :math:`cn` (for :math:`c` any positive constant) is
often referred to as a :term:`linear growth rate` or running time.
This means that as the value of :math:`n` grows, the running time of
the algorithm grows in the same proportion.
Doubling the value of :math:`n` roughly doubles the running time.
An algorithm whose running-time equation has a highest-order term
containing a factor of :math:`n^2` is said to have a
:term:`quadratic growth rate`.
In the figure, the line labeled :math:`2n^2`
represents a quadratic growth rate.
The line labeled :math:`2^n` represents an
:term:`exponential growth rate`.
This name comes from the fact that :math:`n` appears in the exponent.
The line labeled :math:`n!` also grows exponentially.

As you can see from the figure,
the difference between an algorithm whose running time has cost
:math:`\mathbf{T}(n) = 10n` and another with cost
:math:`\mathbf{T}(n) = 2n^2` becomes tremendous as :math:`n` grows.
For :math:`n > 5`, the algorithm with running time
:math:`\mathbf{T}(n) = 2n^2` is already much slower.
This is despite the fact that :math:`10n` has a greater constant
factor than :math:`2n^2`.
Comparing the two curves marked :math:`20n` and :math:`2n^2` shows
that changing the constant factor for one of the equations only shifts
the point at which the two curves cross.
For :math:`n>10`, the algorithm with cost :math:`\mathbf{T}(n) = 2n^2`
is slower than the algorithm with cost :math:`\mathbf{T}(n) = 20n`.
This graph also shows that the equation
:math:`\mathbf{T}(n) = 5 n \log n`
grows somewhat more quickly than both :math:`\mathbf{T}(n) = 10 n` and
:math:`\mathbf{T}(n) = 20 n`, but not nearly so quickly as the
equation :math:`\mathbf{T}(n) = 2n^2`.
For constants :math:`a, b > 1, n^a` grows faster than either
:math:`\log^b n` or :math:`\log n^b`.
Finally, algorithms with cost :math:`\mathbf{T}(n) = 2^n` or
:math:`\mathbf{T}(n) = n!` are prohibitively expensive for even modest
values of :math:`n`.
Note that for constants :math:`a, b \geq 1, a^n` grows faster than
:math:`n^b`.

We can get some further insight into relative growth rates for various
algorithms from the following table.
Most of the growth rates that appear in typical algorithms are shown,
along with some representative input sizes.
Once again, we see that the growth rate has a tremendous effect on the
resources consumed by an algorithm.

.. _GrowthTable:

.. topic:: Table

   Costs for representative growth rates.

   .. math::

      \begin{array}{c|c|c|c|c|c|c|c}
      \mathsf{n} & \mathsf{\log \log n} & \mathsf{\log n} & \mathsf{n} &
      \mathsf{n \log n} & \mathsf{n^2} & \mathsf{n^3} & \mathsf{2^n}\\
      \hline
      \mathsf{16} & \mathsf{2} & \mathsf{4} & \mathsf{2^{4}} &
      \mathsf{4 \cdot 2^{4} = 2^{6}} &
      \mathsf{2^{8}} & \mathsf{2^{12}} & \mathsf{2^{16}}\\
      \mathsf{256} & \mathsf{3} & \mathsf{8} & \mathsf{2^{8}} &
      \mathsf{8 \cdot 2^{8} = 2^{11}} &
      \mathsf{2^{16}} & \mathsf{2^{24}} & \mathsf{2^{256}}\\
      \mathsf{1024} & \mathsf{\approx 3.3} & \mathsf{10} & \mathsf{2^{10}} &
      \mathsf{10 \cdot 2^{10} \approx 2^{13}} &
      \mathsf{2^{20}} & \mathsf{2^{30}} & \mathsf{2^{1024}}\\
      \mathsf{64 {\rm K}} & \mathsf{4} & \mathsf{16} & \mathsf{2^{16}} &
      \mathsf{16 \cdot 2^{16} = 2^{20}} &
      \mathsf{2^{32}} & \mathsf{2^{48}} & \mathsf{2^{64 {\rm K}}}\\
      \mathsf{1 {\rm M}} & \mathsf{\approx 4.3} & \mathsf{20} & \mathsf{2^{20}} &
      \mathsf{20 \cdot 2^{20} \approx 2^{24}} &
      \mathsf{2^{40}} & \mathsf{2^{60}} & \mathsf{2^{1 {\rm M}}}\\
      \mathsf{1 {\rm G}} & \mathsf{\approx 4.9} & \mathsf{30} & \mathsf{2^{30}} &
      \mathsf{30 \cdot 2^{30} \approx 2^{35}} &
      \mathsf{2^{60}} & \mathsf{2^{90}} & \mathsf{2^{1 {\rm G}}}\\
      \end{array}

.. avembed:: Exercises/AlgAnal/CompareGrowth.html ka
   :long_name: Comparing Growth Rates Exercise
   :keyword: Algorithm Analysis; Growth Rate

Growth Rates Ordering Exercise
------------------------------

.. avembed:: Exercises/AlgAnal/GrowthRatesPRO.html ka
   :long_name: Growth Rates Ordering Exercise
   :keyword: Algorithm Analysis; Growth Rate

.. todo::
   :type: AV

   To make students more engaged in the GrowthRates exercise, we may
   need a tool that allows students to input two growth rate functions.
   Then the tool should plot the graph of both functions and mark
   their crossing point. The student also should be allowed to play
   with the constant values for both functions and see that this only
   changes the crossing point but doesn't change which function grows
   faster than the other.
