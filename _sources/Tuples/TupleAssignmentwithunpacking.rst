..  Copyright (C)  Brad Miller, David Ranum, Jeffrey Elkner, Peter Wentworth, Allen B. Downey, Chris
    Meyers, and Dario Mitchell.  Permission is granted to copy, distribute
    and/or modify this document under the terms of the GNU Free Documentation
    License, Version 1.3 or any later version published by the Free Software
    Foundation; with Invariant Sections being Forward, Prefaces, and
    Contributor List, no Front-Cover Texts, and no Back-Cover Texts.  A copy of
    the license is included in the section entitled "GNU Free Documentation
    License".

.. qnum::
   :prefix: tuples-4-
   :start: 1

.. index::
    single: assignment; tuple 
    single: tuple; assignment 

Tuple Assignment with unpacking
-------------------------------

Python has a very powerful **tuple assignment** feature that allows a tuple of variable names on the left of an 
assignment statement to be assigned values from a tuple on the right of the assignment. Another way to think of this 
is that the tuple of values is **unpacked** into the variable names.

.. sourcecode:: python

    (name, surname, birth_year, movie, movie_year, profession, birth_place) = julia

This does the equivalent of seven assignment statements, all on one easy line. One requirement is that the number of 
variables on the left must match the number of elements in the tuple. 

Once in a while, it is useful to swap the values of two variables. With conventional assignment statements, we have to 
use a temporary variable. For example, to swap ``a`` and ``b``:

.. sourcecode:: python

    temp = a
    a = b
    b = temp

Tuple assignment solves this problem neatly:

.. sourcecode:: python

    (a, b) = (b, a)

The left side is a tuple of variables; the right side is a tuple of values. Each value is assigned to its respective 
variable. All the expressions on the right side are evaluated before any of the assignments. This feature makes
tuple assignment quite versatile.

Naturally, the number of variables on the left and the number of values on the right have to be the same.

.. sourcecode:: python

    (a, b, c, d) = (1, 2, 3) # ValueError: need more than 3 values to unpack 

Earlier we were demonstrating how to use tuples as return values when calculating the area and circumference of a 
circle. Here we can unpack the return values after calling the function.

.. activecode:: ac12_4_1
    
    def circleInfo(r):
        """ Return (circumference, area) of a circle of radius r """
        c = 2 * 3.14159 * r
        a = 3.14159 * r * r
        return c, a

    print(circleInfo(10))
    
    circumference, area = circleInfo(10)
    print(circumference)
    print(area)

    circumference_two, area_two = circleInfo(45)
    print(circumference_two)
    print(area_two)

Python even provides a way to pass a single tuple to a function and have it be unpacked for assignment to the named 
parameters. 

.. activecode:: ac12_4_2

    def add(x, y):
        return x + y
        
    print(add(3, 4))
    z = (5, 4)
    print(add(*z)) # this line will cause the values to be unpacked
    print(add(z)) # this line causes an error

If you run this, you will be get an error caused by line 7, where it says that the function add is expecting two 
parameters, but you're only passing one parameter (a tuple). In line 6 you'll see that the tuple is unpacked and 5 is 
bound to x, 4 to y. 

Don't worry about mastering this idea yet. But later in the course, if you come across some code that someone else has 
written that uses the * notation inside a parameter list, come back and look at this again.

**Check your Understanding**

.. mchoice:: question12_4_1
   :topics: Tuples/TupleAssignmentwithunpacking
   :multiple_answers:
   :answer_a: Make the last two lines of the function be "return x" and "return y"  
   :answer_b: Include the statement "return [x, y]" 
   :answer_c: Include the statement "return (x, y)"
   :answer_d: Include the statement "return x, y"
   :answer_e: It's not possible to return two values; make two functions that each compute one value.
   :feedback_a: As soon as the first return statement is executed, the function exits, so the second one will never be executed; only x will be returned
   :feedback_b: return [x,y] is not the preferred method because it returns x and y in a list and you would have to manually unpack the values. But it is workable.
   :feedback_c: return (x, y) returns a tuple.
   :feedback_d: return x, y causes the two values to be packed into a tuple.
   :feedback_e: It is possible, and frequently useful, to have one function compute multiple values.
   :correct: b,c,d

   If you want a function to return two values, contained in variables x and y, which of the following methods will work?

.. mchoice:: question12_4_2
   :topics: Tuples/TupleAssignmentwithunpacking
   :answer_a: You can't use different variable names on the left and right side of an assignment statement.
   :answer_b: At the end, x still has it's original value instead of y's original value.
   :answer_c: Actually, it works just fine!
   :feedback_a: Sure you can; you can use any variable on the right-hand side that already has a value.
   :feedback_b: Once you assign x's value to y, y's original value is gone.
   :feedback_c: Once you assign x's value to y, y's original value is gone.
   :correct: b

   Consider the following alternative way to swap the values of variables x and y. What's wrong with it?
   
   .. code-block:: python 
        
        # assume x and y already have values assigned to them
        y = x
        x = y   

.. activecode:: ac12_4_3
   :language: python
   :autograde: unittest
   :chatcodes:

   **3.** With only one line of code, assign the variables water, fire, electric, and grass to the values "Squirtle", "Charmander", "Pikachu", and "Bulbasaur"
   ~~~~

   =====

   from unittest.gui import TestCaseGui

   class myTests(TestCaseGui):

      def testOne(self):
         self.assertEqual(water, "Squirtle", "Testing that water is assigned to the correct value.")
         self.assertEqual(fire, "Charmander", "Testing that fire is assigned to the correct value.")
         self.assertEqual(electric, "Pikachu", "Testing that electric is assigned to the correct value.")
         self.assertEqual(grass, "Bulbasaur", "Testing that grass is assigned to the correct value.")

   myTests().main()
   
.. activecode:: ac12_4_4
   :language: python
   :autograde: unittest
   :chatcodes:

   **4.** With only one line of code, assign four variables, ``v1``, ``v2``, ``v3``, and ``v4``, to the following four values: 1, 2, 3, 4.
   ~~~~

   =====

   from unittest.gui import TestCaseGui

   class myTests(TestCaseGui):

      def testOne(self):
         self.assertEqual(v1, 1, "Testing that v1 was assigned correctly.")
         self.assertEqual(v2, 2, "Testing that v2 was assigned correctly.")
         self.assertEqual(v3, 3, "Testing that v3 was assigned correctly.")
         self.assertEqual(v4, 4, "Testing that v4 was assigned correctly.")

   myTests().main()