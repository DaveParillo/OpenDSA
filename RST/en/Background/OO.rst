
.. Copyright (c) 2015 by Dave Parillo
.. This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License.

.. avmetadata::
   :author: Dave Parillo
   :satisfies: OO Intro
   :topic: Introduction

Introduction to Object Orientation
==================================

Object-oriented programming (OOP) is a programming paradigm based on the 
concept of :term:`objects <object>`, which are :term:`data structures <data structure>` that contain data, 
in the form of fields (or attributes) 
and code, in the form of procedures, (or methods). 
A distinguishing feature of objects is that an object's procedures 
provide access to and modify the its fields.

In object-oriented programming, computer programs are designed by making them 
out of objects that interact with one another. 
There is significant diversity in object-oriented programming, 
but most popular languages are class-based, meaning that objects are instances of classes, 
which typically also determines their type.

Comparisons to Procedural Programming
-------------------------------------
Object orientation is an outgrowth of procedural programming.
Procedural programming is a programming paradigm, derived from structured programming, 
based upon the concept of the procedure call. Procedures, also known as routines, subroutines, 
or methods define the computational steps to be carried out.

Any given procedure might be called at any point during a program's execution, 
including by other procedures or itself. 
Procedural programming is a list or set of instructions telling a 
computer what to do step by step and how to perform from the first 
code to the second code. 
Procedural programming languages include C, Fortran, Pascal, and BASIC.

The focus of procedural programming is to break down a programming task into 
a collection of variables, data structures, and subroutines, 
whereas in object-oriented programming it is to break down a programming task into 
:term:`objects <object>` that expose behavior (methods) and data (fields) using interfaces. 
The most important distinction is that while procedural programming uses procedures 
to operate on data structures, object-oriented programming bundles the two together, 
so an **object**, which is an **instance of a class**, operates on its "own" data structure.


Principles of Object Orientation
--------------------------------

There are many views on the main features and motivations for object oriented programming [#]_ [#]_.
There are 4 principles that apply to most:

:Encapsulation:
    
    Encapsulation refers to the creation of self-contained modules (classes)
    that bind processing functions to the data. 
    The data within each class is kept private.
    Each class defines rules for what is publicly visible and
    what modifications are allowed.

:Inheritance:
    
    Classes are created in hierarchies, and inheritance lets the 
    structure and methods in one class pass down the :term:`class hierarchy`. 
    By *inheriting* code, complex classes can be constructed 
    through the reuse of code in a parent class.
    If a step is added at the bottom of a hierarchy, 
    only the processing and data associated with that unique step must be added. 
    Everything else above that step is inherited. 
    The ability to reuse existing objects is considered a major advantage 
    of object technology.


:Polymorphism:
    
    Object-oriented programming lets programmers create procedures for 
    objects whose exact type is not known until runtime. 
    For example, a screen cursor may change its shape from an arrow to a 
    line depending on the program mode. 
    The routine to move the cursor on screen in response to mouse movement can 
    be written for "cursor", and polymorphism lets that cursor take simulating 
    system behaviour. 
    It can be also described as many shapes of same object.

:Abstraction:
    
    An abstraction denotes the essential characteristics of an object that distinguish it from all
    other kinds of object and thus provide crisply defined conceptual
    boundaries, relative to the perspective of the viewer. [Booch91]_

    Abstraction denotes a model, a view, or some other focused representation 
    for an actual item. Its the development of a software object to represent 
    an object we can find in the real world. 
    Encapsulation hides the details of that implementation.


Encapsulation
.............

Consider the following example:

.. codeinclude:: Background/BadEncapsulation

It's clearly a bad idea to allow people to set the shipping weight to a negative value.
How can you change this class to prevent problems like this from happening?
Your only choice is to make the *weight* private and write a method that allows
the class to set limits on weight.  But since you have already declared *weight*
to be **public**, as soon as you make this 'fix', you break every class that
currently uses it!

The ability to change your code without breaking every class that uses it is one
of the key benefits of encapsulation.
By limiting access and hiding the implementation details of your class to the maximum
extent possible, you make it possible to change, fix, extend, or rework your class
without requiring changes in any of the code that uses your class.

How do we ensure our code remains flexible and maintainable?

- Keep fields hidden using a *private* access modifier
- Make *public accessor methods* and force callers to use them
  by hiding your fields.

Compare our first example with the following:

.. codeinclude:: Background/Encapsulation

The alert among you might be thinking 
"Hey! How is this any better than the first example?"
We added a setter and getter, but added no new capability.  
What have we gained?

We have gained quite a bit.
Now we are free to change our minds about how weight values are set and retrieved.
Even though we aren't doing anything now, we are free to change the implementation
later and no calling class will know.

Good OO design demands thinking about the future.
Which brings us to our final example.
No classes would need to be modified to add the new capability below.

.. codeinclude:: Background/GoodEncapsulation

Inheritance
...........

Consider the following example:

.. codeinclude:: Background/Inheritance

when run, produces the following output:

  'test1' does not equal 'test2'.
  'test1' is an Object.

Where did the *equals* method come from?
It was *inherited* from the class *Object*.
In Java (and some other languages as well), every class is a subclass of the class Object.
In Java, every class inherits methods for 
equals, hashCode, toString, and a few others.

Why?
The creators of the language assumed it would be very common to be able to determine
if two objects were equal, or to produce a String representation of an object.
If these methods were not in the Object class, then every programmer would have to 
create their own solution for this problem. 
More importantly, every programmer might implement a different *interface* for basic
needs currently satisfied by 'equals' and 'toString', which would complicate
the implementation of these common functions between developers.


More generically, inheritance promotes code reuse.
An excellent example is the InputStream class.
The *InputStream* class is the base class (superclass) of 
all input streams in the Java IO API. 
*InputStream* subclasses include the *FileInputStream*, *BufferedInputStream* 
and the *PushbackInputStream* among others.

Java InputStream's are used for reading data, one byte at a time, for example:

.. codeinclude:: Background/InputStreamExample

Which creates a new FileInputStream instance. 
FileInputStream is a subclass of InputStream so it is safe to assign an instance of 
FileInputStream to an InputStream variable (the inputstream variable). 

The *InputStream* class exposes common methods which all subclasses of *InputStream* inherit.

:void available(): 
    Returns an estimate of the number of bytes that can be 
    read (or skipped over) from this input stream without blocking by the next 
    invocation of a method for this input stream.
:int close(): 
    Closes this input stream and releases any system resources associated with the stream.
:mark(int readlimit): 
    Marks the current position in this input stream.
:boolean markSupported(): 
    Tests if this input stream supports the mark and reset methods.
:abstract int read(): 
    Reads the next byte of data from the input stream.
:int read(byte[] b): 
    Reads some number of bytes from the input stream and stores them into the buffer array b.
:int read(byte[] b, int off, int len): 
    Reads up to len bytes of data from the input stream into an array of bytes.
:void reset(): 
    Repositions this stream to the position at the time the mark method was last 
    called on this input stream.
:long skip(long n): 
    Skips over and discards n bytes of data from this input stream.

The *FileInputStream* class inherits all of the methods from *InputStream* and offers two more:

:FileChannel getChannel(): 
    Returns the unique FileChannel object associated with this file input stream.
:FileDescriptor getFD(): 
    Returns the FileDescriptor object that represents the connection to the 
    actual file in the file system being used by this FileInputStream.


In contrast, the *AudioInputStream* class offers two completely different methods:

:AudioFormat getFormat():
    Obtains the audio format of the sound data in this audio input stream.
:long getFrameLength():
    Obtains the length of the stream, expressed in sample frames rather than bytes.

The above examples illustrate that both the AudioInputStream and FileInputStream objects have an
**IS-A** relationship with InputStream.  That is, an AudioInputStream **IS-A** InputStream
and a FileInputStream **IS-A** InputStream.

The **IS-A** relationship in Java is expressed using the keywords *extends* for class inheritance
and *implements* for interface implementations.

This is different from extending classes through :term:`composition`.

Not only does inheritance promote code reuse, but it provides a means to use 
polymorphism in our code.


Polymorphism
............



Abstraction
...........



Notes
-----

.. [#] See https://en.wikipedia.org/wiki/Object-oriented_programming#Fundamental_features_and_concepts
.. [#] _SOLID: http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29





