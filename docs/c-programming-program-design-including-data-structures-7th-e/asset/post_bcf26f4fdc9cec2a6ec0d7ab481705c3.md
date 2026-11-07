
**Sample Run 1:** In this sample run, the user input is shaded.  
Line 4: Enter the dividend: 23  
Line 7: Enter the divisor: 6  
Line 17: Quotient = 3

**Sample Run 2:** In this sample run, the user input is shaded.  
Line 4: Enter the dividend: 34  
Line 7: Enter the divisor: -6  
Line 21: Negative divisor.

**Sample Run 3:** In this sample run, the user input is shaded.  
Line 4: Enter the dividend: 34  
Line 7: Enter the divisor: 0  
Line 21: The input stream is in the fail state.

In this program, the statements in Lines 1 and 2 declare the variables used in the program. Notice that the string object inpStr is also initialized.

The statements in Lines 4 through 9 input the data into the variables dividend and divisor. The statement in Line 10 checks whether divisor is 0, the statement in Line 12 checks whether divisor is negative, and the statement in Line 14 checks whether the standard input stream is in the fail state.

The statement in Line 11 throws the variable divisor, the statement in Line 13 throws an anonymous string object with the string "Negative divisor.", and the statement in Line 15 throws the object inpStr.

The catch block in Line 18 catches an exception of type int, and the catch block in Line 20 catches an exception of type string. If the exception is thrown by the statement in Line 11, it is caught and processed by the catch block in Line 18. If the exception is thrown by the statements in Lines 13 or 15, it is caught and processed by the catch block in Line 20.

In Sample Run 1, the program does not encounter any problems. In Sample Run 2, division by a negative number occurs. In Sample Run 3, the standard input stream enters the fail state.

## Using C++ Exception Classes

C++ provides support to handle exceptions via a hierarchy of classes. The `class exception` is the base of the classes designed to handle exceptions. Among others, this class contains the function what. The function what returns a string containing an appropriate message. All derived classes of the `class exception` override the function `what` to issue their own error messages.

Two classes are immediately derived from the `class exception`: `logic_error` and `runtime_error`. Both of these classes are defined in the header file `stdexcept`.

To deal with logical errors in a program, such as a string subscript out of range or an invalid argument to a function call, several classes are derived from the `class logic_error`. For example, the `class invalid_argument` is designed to deal with illegal arguments used in a function call. The `class out_of_range` deals with the string subscript out of range error. If a length greater than the maximum allowed for a string object is used, the `class length_error` deals with this error. For example, recall that every string object has a maximum length (see Chapter 7). If a length greater than the maximum length allowed for a string is used, then the `length_error` exception is generated. If the operator `new` cannot allocate memory space, this operator throws a `bad_alloc` exception.

The `class runtime_error` is designed to deal with errors that can be detected only during program execution. For example, to deal with arithmetic overflow and underflow exceptions, the `class overflow_error` and `underflow_error` are derived from the `class runtime_error`.

Examples 14–8 and 14–9 illustrate how C++’s exception classes are used to handle exceptions in a program.

The program in Example 14–8 shows how to handle the exceptions `out_of_range` and `length_error`. Notice that in this program, these exceptions are thrown by the string functions `substr` and the string concatenation operator `+`. Because the exceptions are thrown by these functions, we do not include any `throw` statement in the `try` block.

### EXAMPLE 14-8

```cpp
// Handling out_of_range and length_error exceptions.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string sentence;                              //Line 1
    string str1, str2, str3;                      //Line 2

    try                                          //Line 3
    {
        sentence = "Testing string exceptions!"; //Line 4
        cout << "Line 5: sentence = " << sentence
             << endl;                             //Line 5
        cout << "Line 6: sentence.length() = "
             << static_cast<int>(sentence.length())        //Line 6
             << endl;

        str1 = sentence.substr(8, 20);                     //Line 7
        cout << "Line 8: str1 = " << str1
             << endl;                                      //Line 8

        str2 = sentence.substr(28, 10);                    //Line 9
        cout << "Line 10: str2 = " << str2
             << endl;                                      //Line 10

        str3 = "Exception handling. " + sentence;         //Line 11
        cout << "Line 12: str3 = " << str3
             << endl;                                      //Line 12
    }
    catch (out_of_range re)                            //Line 13
    {
        cout << "Line 14: In the out_of_range "
             << "catch block: " << re.what()
             << endl;                                  //Line 14
    }
    catch (length_error le)                            //Line 15
    {
        cout << "Line 16: In the length_error "
             << "catch block: " << le.what()
             << endl;                                  //Line 16
    }

    return 0;                                          //Line 17
}
```

**Sample Run:**

```text
Line 5: sentence = Testing string exceptions!
Line 6: sentence.length() = 26
Line 8: str1 = string exceptions!
Line 14: In the out_of_range catch block: invalid string position
```

In this program, the statement in Line 7 uses the function substr to determine a substring in the string object sentence. The length of the string sentence is 26. Because the starting position of the substring is 8, which is less than 26, no exception is thrown. However, in the statement in Line 9, the starting position of the substring is 28, which is greater than 26 (the length of sentence). Therefore, the function substr throws an out_of_range exception, which is caught and processed by the catch block in Line 13. Notice that in the statement in Line 14, the object re uses the function what to return the error message, invalid string position.

The program in Example 14-9 illustrates how to handle the exception bad_alloc thrown by the operator new.

### EXAMPLE 14-9

```cpp
// Handling bad_alloc exception thrown by the operator new.

#include <iostream>

using namespace std;

int main()
{
    int *list[100];                              //Line 1

    try
    {                                            //Line 2
        for (int i = 0; i < 100; i++)            //Line 3
        {
            list[i] = new int[50000000];         //Line 4
            cout << "Line 4: Created list[" << i
                 << "] of 50000000 components."
                 << endl;                        //Line 5
        }
    }
    catch (bad_alloc be)                         //Line 6
    {
        cout << "Line 7: In the bad_alloc catch "
             << "block: " << be.what() << "."   //Line 7
             << endl;
    }

    return 0;                                    //Line 8
}
```

**Sample Run:**

```text
Line 4: Created list[0] of 50000000 components.
Line 4: Created list[1] of 50000000 components.
Line 4: Created list[2] of 50000000 components.
Line 4: Created list[3] of 50000000 components.
Line 4: Created list[4] of 50000000 components.
Line 4: Created list[5] of 50000000 components.
Line 4: Created list[6] of 50000000 components.
Line 4: Created list[7] of 50000000 components.
Line 7: In the bad_alloc catch block: bad allocation.
```

The preceding program works as follows. The statement in Line 1 declares list to be an array of 100 pointers. The body of the *for* loop in Line 3 is designed to execute 100 times. For each iteration of the *for* loop, the statement in Line 4 uses the operator new to allocate an array of 50000000 components of type *int*. As shown in the sample run, the operator new is able to create eight arrays of 50000000 components each. In the ninth iteration, the operator new is unable to create the array and throws a bad_alloc.
