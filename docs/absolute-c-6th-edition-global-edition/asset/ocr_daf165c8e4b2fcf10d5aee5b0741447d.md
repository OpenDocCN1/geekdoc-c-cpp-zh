All the declarations for private member functions are parts of the implementation. All member function definitions (whether the function is public or private) are parts of the implementation.

# Programming Projects

+   1. Write a rating program for a software development firm with the following rating policies.
+   
+   a. Core competency – This parameter measures an employee’s involvement, innovation, and passion toward their assigned tasks, and is graded on 10 points.
+   
+   b. Performance evaluation – This parameter measures an employee’s performance over the year, and is graded on 30 points.
+   
+   c. Ideation – An employee is measured on their patent submissions, patents awarded, technical papers presented, etc. and is graded on 10 points.
+   
+   d. The performance evaluation accounts for 50% of an employee’s final rating, core competency accounts for 30%, and ideation accounts for 20%.
+   
+   The total points obtained by an employee are summed up and normalized. Employees with points of 80 or more are rated a 1, those between 60 to 79 are rated a 2, those between 50 to 59 are rated a 3, and those less than 50 are rated a 4.
+   
+   The program will read an employee’s points against the three criteria and output the total points obtained on a scale of 100, and the final rating point. Define and use a structure for the employee records.

+   2. Define a class for a type called Circle. An object of type Circle is used to display the area, diameter, and circumference of a circle based on the radius of that object. Include a mutator function that sets the radius to a value given as an argument. Include member function to calculate the area, diameter, and circumference of the circle. Also include a member function that returns the radius of the circle. Embed your class definition in a test program.

+   3. The type Point is a fairly simple data type, but under another name (the template class pair) this data type is defined and used in the C++ Standard Template Library, although you need not know anything about the Standard Template Library to do this exercise. Write a definition of a class named Point that might be used to store and manipulate the location of a point in the plane. You will need to declare and implement the following member functions:
+   
+   a. A member function set that sets the private data after an object of this class is created.
+   
+   b. A member function to move the point by an amount along the vertical and horizontal directions specified by the first and second arguments.
+   
+   c. A member function to rotate the point by 90 degrees clockwise around the origin.
+   
+   d. Two const inspector functions to retrieve the current coordinates of the point.