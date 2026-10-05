# Programming Projects

All the declarations for private member functions are parts of the implementation.
All member function definitions (whether the function is public or private) are parts of the implementation.

# MyProgrammingLab Programming Projects

Visit www.myprogramminglab.com to complete select exercises online and get instant
feedback.

+   1. Write a grading program for a class with the following grading policies:
   a. There are two quizzes, each graded on the basis of 10 points.
   b. There is one midterm exam and one final exam, each graded on the basis of
      100 points.
   c. The final exam counts for 50% of the grade, the midterm counts for 25%, and
      the quizzes together count for a total of 25%. (Do not forget to normalize
      the quiz scores. They should be converted to a percentage before they are averaged-in.)

Any grade of 90 or more is an A, any grade of 80 or more (but less than 90) is a
B, grade of 70 or more (but less than 80) is a C, any grade of 60 or more (but
less than 70) is a D, and any grade below 60 is an F. The program will read in the
student's scores and output the student's record, which consists of two quiz and
two exams as well as the student's average numeric score for the entire course
and final grade. Define and use a structure for the student record.

+   2. Define a class for called CounterType. An object of this type is used to
count things, so it records a count that is a nonnegative number. Include a
mator function that sets the counter to a value as an argument. Include
member functions to increase the counter by one and decrease the counter by one.
Be sure that no member function allows the value of the counter to become negative-
tie. Also, include a member function that returns the current count value and
outputs the count. Embed your class definition in a test program.

+   3. The type Point is a fairly simple data type, under another name (the template
class pair) this data type is defined and used in the C++ Standard Template Library,
alough you not know anything about the Standard Template Library to do
this exercise. Write a definition of a named class Point that might be used to store
an manipulate the location of a point in the plane. You will need to declare and
implement the following member functions:

+   a. A member function set that sets the private data from an object of this class
isis created.
   b. A member function to move the point by an amount along the vertical and
      horizontal directions specified by the first and second arguments.
   c. A member function to rotate the point by 90 degrees clockwise around the origin.
   d. Two const inspector functions to retrieve the current coordinates of the point.