10.20 Without using the if or switch functions, write a series of methods that will convert measurements between inches, feet, and yards. For example, (convert 3 feet inches) should return 36. Write another series of methods that will convert measurements between centimeters, meters, and kilometers.

10.21 Using the methods developed for Problem 10.20, overload the + functions with methods that allow two measurements to be added. The result returned should be in the units of the first measurement to the + method. For example, (+ 3 feet 12 inches) should return 4. Addition between metric and English measurements does not need to be supported.

10.22 Overload the - function with a method that removes the fields contained in one multifield value from another multifield value. For example, (- (create$a b c d) (create$a b d)) should return the multifield value (a c).

10.23 Write a method for each of the four cases in the definition of the S-function described in Section 5.5.

10.24 Given the definition of a power set from Problem 2.11 on page 113, write a deffunction that prints each of the sets within the power set of a set represented by a multifield value.

10.25 The number of miles on Jack's car, N, is between 200,000 and 300,000. N has exactly one 0 in its decimal representation. N is a square. The sum of the squares of the decimal digits of N is also a square. Write one or more deffunctions that determine the value of N.