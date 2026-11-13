the name of a person in your class. The function determines whether there is a path of acquaintances from person to Dor. Hint: This problem is similar to the maze problem in Section 9.2. But beware of potential infinite recursion! One way to avoid infinite recursion is to include a bag of student names, which keeps track of the names of the students you have already visited on your search for a path to Dor.

+   12 A pretty print program takes a program, which may not be indented in any particular way, and produces a copy with the same program indented so that bracket pairs ({ and }) line up with inner pairs indented more than outer pairs, so that if-else statements are indented as we have been doing, and so that other indenting is as we have been doing. Write a program that reads a C++ program from one text file and produces a pretty version of the program in a second text file. To make it easier, simply do this for the body of the program, ignoring the declarations, and assume that all substatements of complex statements (other than compound statements themselves) are compound statements (that is, are enclosed by brackets).

+   13 Rewrite the recursive pow function from Figure 9.11 on page 465, so that the time to compute pow(x, n) is log(n). Hint: Use the formula x^n = x^t * x^t.

+   14 Write a recursive function to convert a character string of digits to an integer. Example: convert("1234") returns 1234. Hint: To convert a character to a number, subtract the ASCII value '0' from the character. For example, if the string s has but one character, then the function can return the value s[0] - '0'.

+   15 Ackermann's function, named after the German mathematician Wilhelm Ackermann, is used in the theory of recursive functions. There are several variants of this function. Their common properties are that the function takes two parameters (x and y) and grows very fast (much faster than polynomials or exponentials). Here is one

+   variant:
+   1. If x = 0 then Ackermann(x, y) = 2y
+   2. If x >= 1 and y = 0 then Ackermann(x, y) = 0
+   3. If x >= 1 and y = 1 then Ackermann(x, y) = 2
+   4. If x >= 1 and y >= 2 then Ackermann(x, y) = Ackermann(x-1, Ackermann(x, y-1))

Implement this variant of Ackermann's function with a recursive function.

+   16 Write a program that asks the user to think of an integer between 1 and 1,000,000, and then guesses the number through a series of yes/no questions. To guess the number, the program calls a recursive function guess that has two parameters, low and high. The precondition for the function requires that the user's number lie in the range low..high so that the program's initial call is to guess(1, 1000000). What is a good starting case for guess, when it can guess the user's number with little or no work? Answer: If (low == high), then there is only one possible number, and the function can guess that number. On the other hand, if (low < high), then the function should calculate a point near the middle of the range:
+   midpoint = (low + high) / 2;
+   Then the function asks the user whether the midpoint is the correct number. If so, the function is finished. On the other hand, if the midpoint is not the user's number, then the function asks whether the correct number is larger than midpoint. If so, the function knows that the user's number lies in the range midpoint + 1 to high, and a recursive call can be made to solve the smaller problem of finding a user's number in the range midpoint + 1 to high. On the other hand, if the user's number is not larger than midpoint, then a recursive call can be made to solve the smaller problem of finding a user's number in the range low to midpoint - 1. This method of searching is called binary search, which we will explore further in Chapter 12.