
```cpp
cout << "Line 17: Quotient = " << quotient
     << endl;                         //Line 17
}
catch (int)                              //Line 19
{
    cout << "Line 21: Division by 0." << endl; //Line 21
}

return 0;                                //Line 23
}                                        //Line 24
```

**Sample Run 1:** In this sample run, the user input is shaded.

```text
Line 8: Enter the dividend: 26
Line 11: Enter the divisor: 7
Line 17: Quotient = 3
```

**Sample Run 2:** In this sample run, the user input is shaded.

```text
Line 8: Enter the dividend: 52
Line 11: Enter the divisor: 0
Line 21: Division by 0.
```

This program works as follows. The statement in Line 5 declares the `int` variables dividend, divisor, and quotient. The `try` block starts at Line 6. The statement in Line 8 prompts the user to enter the value for the dividend; the statement in Line 9 stores this number in the variable dividend. The statement in Line 11 prompts the user to enter the value for the divisor, and the statement in Line 12 stores this number in the variable divisor. The statement in Line 14 checks whether the value of divisor is 0. If the value of divisor is 0, the statement in Line 15 throws the constant value 0. The statement in Line 16 calculates the quotient and stores it in quotient. The statement in Line 17 outputs the value of quotient.

The `catch` block starts in Line 19 and catches an exception of type `int`.

In Sample Run 1, the program does not throw any exception.

In Sample Run 2, the entered value of `divisor` is 0. Therefore, the statement in Line 15 throws 0, which is caught by the `catch` block starting in Line 19. The statement in Line 21 outputs the appropriate message.

The program in Example 14-6 is the same as the program in Example 14-5, except that the `throw` statement throws the value of the variable `divisor`.

### EXAMPLE 14-6

```cpp
// Handling division by zero exception.

#include <iostream>                         //Line 1
using namespace std;                    //Line 2
```

**Sample Run 1:** In this sample run, the user input is shaded.

```text
Line 10: Enter the dividend: 21
Line 13: Enter the divisor: 8
Line 23: Quotient = 2
```

**Sample Run 2:** In this sample run, the user input is shaded.

```text
Line 10: Enter the dividend: 19
Line 13: Enter the divisor: -2
Line 31: Negative divisor.
```

**Sample Run 3:** In this sample run, the user input is shaded.

```text
Line 10: Enter the dividend: 24
Line 13: Enter the divisor: y
Line 31: The input stream is in the fail state.
```

In this program, the statements in Lines 6 and 7 declare the variables used in the program. Notice that the string object `inpStr` is also initialized.

The statements in Lines 10 through 15 input the data into the variables `dividend` and `divisor`. The statement in Line 16 checks whether `divisor` is 0, the statement in Line 18 checks whether `divisor` is negative, and the statement in Line 20 checks whether the standard input stream is in the fail state.

The statement in Line 17 throws the variable `divisor`, the statement in Line 19 throws an anonymous string object with the string "Negative divisor.", and the statement in Line 21 throws the object `inpStr`.

The `catch` block in Line 25 catches an exception of type `int`, and the `catch` block in Line 29 catches an exception of type `string`. If the exception is thrown by the statement in Line 17, it is caught and processed by the `catch` block in Line 25. If the exception is thrown by the statements in Lines 19 or 21, it is caught and processed by the `catch` block in Line 29.

In Sample Run 1, the program does not encounter any problems. In Sample Run 2, division by a negative number occurs. In Sample Run 3, the standard input stream enters the fail state.

## Using C++ Exception Classes

C++ provides support to handle exceptions via a hierarchy of classes. The class `exception` is the base of the classes designed to handle exceptions. Among others, this class contains the function `what`. The function `what` returns a string containing an appropriate message. All derived classes of the class `exception` override the function `what` to issue their own error messages.

Two classes are immediately derived from the class `exception`: `logic_error` and `runtime_error`. Both of these classes are defined in the header file `stdexcept`.

To deal with logical errors in a program, such as a string subscript out of range or an invalid argument to a function call, several classes are derived from the class `logic_error`. For example, the class `invalid_argument` is designed to deal with illegal arguments used in a function call. The class `out_of_range` deals with the string subscript out of range error. If a length greater than the maximum allowed for a string object is used, the class `length_error` deals with this error. For example, recall that every string object has a maximum length (see Chapter 7). If a length larger than the maximum length allowed for a string is used, then the `length_error` exception is generated. If the operator `new` cannot allocate memory space, this operator throws a `bad_alloc` exception.

The class `runtime_error` is designed to deal with errors that can be detected only during program execution. For example, to deal with arithmetic overflow and underflow exceptions, the classes `overflow_error` and `underflow_error` are derived from the class `runtime_error`.

Examples 14-8 and 14-9 illustrate how C++’s exception classes are used to handle exceptions in a program.

The program in Example 14-8 shows how to handle the exceptions `out_of_range` and `length_error`. Notice that in this program, these exceptions are thrown by the string functions `substr` and the string concatenation operator +. Because the exceptions are thrown by these functions, we do not include any `throw` statement in the try block.

### EXAMPLE 14-8

```cpp
// Handling out_of_range and length_error exceptions.

#include <iostream>                                      //Line 1
#include <string>                                       //Line 2

using namespace std;                                     //Line 3

int main()                                             //Line 4
{
                                                       //Line 5
    string sentence;                                    //Line 6
    string str1, str2, str3;                            //Line 7

    try                                                //Line 8
    {                                                  //Line 9
        sentence = "Testing string exceptions!";       //Line 10
        cout << "Line 1: sentence = " << sentence
             << endl;                                   //Line 11
        cout << "Line 12: sentence.length() = "
             << static_cast<int>(sentence.length())
             << endl;                                      //Line 12

        str1 = sentence.substr(8, 20);                    //Line 13
        cout << "Line 14: str1 = " << str1 << endl;      //Line 14

        str2 = sentence.substr(28, 10);                   //Line 15
        cout << "Line 16: str2 = " << str2 << endl;      //Line 16

        str3 = "Exception handling. " + sentence;         //Line 17
        cout << "Line 18: str3 = " << str3 << endl;      //Line 18

    }                                                 //Line 19
    catch (out_of_range re)                            //Line 20
    {                                                 //Line 21
        cout << "Line 22: In the out_of_range catch" //Line 22
             << " block: " << re.what() << endl;     //Line 23
    }                                                 //Line 24
    catch (length_error le)                            //Line 25
    {                                                 //Line 26
        cout << "Line 26: In the length error catch" //Line 26
             << " block: " << le.what() << endl;     //Line 27
    }                                                 //Line 27

    return 0;                                         //Line 28
}                                                     //Line 29
```

**Sample Run:**

```text
Line 11: sentence = Testing string exceptions!
Line 12: sentence.length() = 26
Line 14: str1 = string exceptions!
Line 22: In the out_of_range catch block: invalid string position
```

In this program, the statement in Line 13 uses the function substr to determine a substring in the string object sentence. The length of the string sentence is 26. Because the starting position of the substring is 8, which is less than 26, no exception is thrown. However, in the statement in Line 15, the starting position of the substring is 28, which is greater than 26 (the length of sentence). Therefore, the function substr throws an out_of_range exception, which is caught and processed by the catch block in Line 20. Notice that in the statement in Line 22, the object re uses the function what to return the error message, invalid string position.

The program in Example 14-9 illustrates how to handle the exception bad_alloc thrown by the operator new.
