Appendix O: Solutions to Odd Numbered Review Questions 23

+   49. True

+   51. True

+   53. The first line of the class declaration should read

class Car : public Vehicle

Also, the class declaration should end in a semicolon.

+   55. The constructor function header should read

SnowMobile(int h, double w) : Vehicle(h)

Also, the constructor parameter w is not used.

+   57. The parameter list for the setContents functions must be different.

# Chapter 16

+   1. A throw point is a line in a program that contains a throw statement, thus throwing an exception.

+   3. A try block contains blocks of code executing any statements that might directly or indirectly cause an exception to be thrown. A catch block catches a specific exception and contains code to return it.

+   5. Once an exception has been thrown, the program cannot jump back to the throw point. The function that executes a throw statement will immediately terminate. If that function was called by another function, then the calling function will terminate as well. This process, known as unwinding the stack, continues for the entire chain of nested function calls, from the throw point, all the way back to the catch.

+   7. By catching the bad_alloc exception.

+   9. Because a class object passed to a function template must support all the operators of the function will use the object.

+   11. Sequence and associative.

+   13. throw point

+   15. catch

+   17. template prefix

+   19. specialized

+   21. associative

+   23. bad_alloc

```
25. char * allocBlock(int size)
{
  char *ptr;
  try {
    ptr = new char[size];
  }
```

©2012 Pearson Education, Inc. Upper Saddle River, NJ. All Rights Reserved.