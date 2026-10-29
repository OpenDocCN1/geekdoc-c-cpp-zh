+   a. In Display 8.7, replace the private char members first and second with an array of char of size 100 and a private data member named size.
+   
+      Provide a default constructor that initializes size to 10 and sets the first 10 of the char positions to '#'. (This only uses 10 of the possible 100 slots.)
+   
+      Provide an accessor function that returns the value of the private member size.
+   
+      Test.

+   b. Add an operator[] member that returns a char& that allows the user to access or to set any member of the private data array using a non-negative integer index that is less than size.
+   
+      Test.

+   c. Add a constructor that takes an int argument, sz, that sets the first sz members of the char array to '#'.
+   
+      Test.

+   d. Add a constructor that takes an int argument, sz, and an array of char of size sz. The constructor should set the first sz members of the private data array to the sz members of the argument array of char.
+   
+      Test.

NOTES: When you test, you should test with known good values, with data on boundaries and with deliberately bad values. You are not required to put checks for index out of bounds errors in your code, but that would be a nice touch. Error handling alternatives: Issue an error message then die (that is, call exit(1)) or give the user another chance to make a correct entry.