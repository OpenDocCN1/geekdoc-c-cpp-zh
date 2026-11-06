The program of Fig. 16.3 demonstrates rethrowing an exception. In main's try block (lines 29-34), line 32 calls function throwException (lines 8-24). The throwException function also contains a try block (lines 11-15), from which the throw statement in line 14 throws an instance of standard-library-class Exception. Function throwException's catch handler (lines 16-21) catches this exception, prints an error message (lines 18-19) and rethrows the exception (line 20). This terminates function throwException and returns control to line 32 in the try...catch block in main. The try block terminates (so line 33 does not execute), and the catch handler in main (lines 35-38) catches this exception and prints an error message (line 37). [Note: Since we do not use the exception parameters in the catch handlers of this example, we omit the exception parameter names and specify only the type of exception to catch (lines 16 and 35).]

```
1  // Fig. 16.3: Fig16_03.cpp
2  // Demonstrating exception rethrowing.
3  #include <iostream>
4  #include <exception>
5  using namespace std;
6
7  // throw, catch and rethrow exception
8  void throwException()
9  {
10     // throw exception and catch it immediately
11     try
12     {
13         cout << "  Function throwException throws an exception\n";
14         throw Exception(); // generate exception
15     } // end try
16     catch ( Exception & ) // handle exception
17     {
18         cout << "  Exception handled in function throwException"
19             << "\n  Function throwException rethrows exception";
20         throw; // rethrow exception for further processing
21     } // end catch
22
23     cout << "This also should not print\n";
24 } // end function throwException
25
26 int main()
27 {
28     // throw exception
29     try
30     {
31         cout << "\nmain invokes function throwException\n";
32         throwException();
33         cout << "This should not print\n";
34     } // end try
35     catch ( exception & ) // handle exception
36     {
37         cout << "\n\nException handled in main\n";
38     } // end catch
```

Fig. 16.3 | Rethrowing an exception. (Part 1 of 2.)