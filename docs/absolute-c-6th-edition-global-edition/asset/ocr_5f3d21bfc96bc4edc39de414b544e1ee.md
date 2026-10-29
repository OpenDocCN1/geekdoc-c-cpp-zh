+   15. The `PFArrayD` before the `::` is the name of the class. The `PFArrayD` right after the `::` is the name of the member function. (Remember, a constructor is a member function that has the same name as the class.) The `PFArrayD` inside the parentheses is the type for the parameter `pfArrayObject`.
+   
+   16.
+      a. A destructor is a member function of a class. A destructor’s name always begins with a tilde, `~`, followed by the class name.
+      b. A destructor is called when a class object goes out of scope.
+      c. A destructor actually does whatever the class author programs it to do!
+      d. A destructor is *supposed* to delete dynamic variables that have been allocated by constructors for the class. Destructors may also do other clean-up tasks.
+   
+   17. In the case of the assignment operator `=` and the copy constructor, if there are only built-in types for data, the copy mechanism is exactly what you want, so the default works fine. In the case of the destructor, no dynamic memory allocation is done (no pointers), so the default do-nothing action is again what you want.

# Programming Projects

+   1. Reread the code in Display 10.9. Then, write a class `TwoD` that implements the two-dimensional dynamic array of doubles using ideas from this display in its constructors. You should have a private member of type pointer to double to point to the dynamic array, and two `int` (or unsigned int) values that are `MaxRows` and `MaxCols`.
+   
+      You should supply a default constructor for which you are to choose a default maximum row and column sizes and a parameterized constructor that allows the programmer to set maximum row and column sizes.
+   
+      Further, you should provide a `void` member function that allows setting a particular row and column entry and a member function that returns a particular row and column entry as a value of type double.
+   
+      Remark: It is difficult or impossible (depending on the details) to overload `[ ]` so it works as you would like for two-dimensional arrays. So simply use accessor and mutator functions using ordinary function notation.
+   
+      Overload the `+` operator as a friend function to add two two-dimensional arrays. This function should return the `TwoD` object whose `i`th row, `j`th column element is the sum of the `i`th row, `j`th column element of the left-hand operand `TwoD` object and the `i`th row, `j`th column element of the right-hand operand `TwoD` object.
+   
+      Provide a copy constructor, an overloaded operator `=`, and a destructor.
+   
+      Declare class member functions that do not change the data as `const` members.
+   
+   2. Using dynamic arrays, implement a polynomial class with polynomial addition, subtraction, and multiplication.