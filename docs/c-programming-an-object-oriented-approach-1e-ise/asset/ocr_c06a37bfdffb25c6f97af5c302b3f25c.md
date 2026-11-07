# Programs

+   **PRG-1.** Instead of using fundamental data types as the type of exception to be thrown, we can use objects of a class type. Rewrite Program 14.5, and use a class named *DivByZero* to throw an exception object instead of an integer. The class does not need any data member or member functions.

+   **PRG-2.** Rewrite PRG-1, but define a constructor and a member function *what()* for the class DivByZero.

+   **PRG-3.** Rewrite PRG-2 with the DivByZero class inherited from the standard exception class *invalid_argument*, which is an appropriate class for this purpose. When we divide two integers, we are calling the library operator (/), in that the second argument is an integer which should not be zero.

+   **PRG-4.** Write a program that prompts the user to enter a duration of time in the form hours, minutes, and seconds. The program then calculates the duration in seconds. The program must throw three different exceptions objects: HExcept (if hours is negative), MExcept (if minutes are not between 0 and 59), and SExcept (if seconds are not between 0 and 59). Create three exceptional classes that inherit from the *out_of_range* standard exception class. Use polymorphism (catch-by-reference) and one catch clause to handle all cases.

+   **PRG-5.** The <string> library throws an exception of type *out_of_range* when the *at* function tries to access a character not in the range. Write a program that creates a string out of uppercase letters in English and prints the character when the index is given. Use the *try-catch* block to catch an error if the user enters an index less than 1 or greater than 26. Note that we do not need the *throw* statement in this case because the library throws an exception; we just need to catch it.