
```cpp
cout << "Line 13: secondNum = " << secondNum
     << endl;                                      //Line 13

firstNum = firstNum + NUMBER + 2 * secondNum;     //Line 14

cout << "Line 15: The new value of "
     << "firstNum = " << firstNum << endl;         //Line 15
}
return 0;                                          //Line 16
                                                    //Line 17
```

**Sample Run:** In this sample run, the user input is shaded.

```text
Line 9: firstNum = 18
Line 10: Enter an integer: 15

Line 13: secondNum = 15
Line 15: The new value of firstNum = 60
```

The preceding program works as follows: The statement in Line 1 includes the header file iostream so that program can perform input/output. The statement in Line 2 uses the using namespace statement so that identifiers declared in the header file iostream, such as cin, cout, and endl, can be used without using the prefix std::. The statement in Line 3 declares the named constant NUMBER and sets its value to 12. The statement in Line 4 contains the heading of the function main, and the left brace in Line 5 marks the beginning of the function main. The statements in Lines 6 and 7 declare the variables firstNum and secondNum.

The statement in Line 8 sets the value of firstNum to 18, and the statement in Line 9 outputs the value of firstNum. Next, the statement in Line 10 prompts the user to enter an integer. The statement in Line 11 reads and stores the integer into the variable secondNum, which is 15 in the sample run. The statement in Line 12 positions the cursor on the screen at the beginning of the next line. The statement in Line 13 outputs the value of secondNum. The statement in Line 14 evaluates the expression:

```text
firstNum + NUMBER + 2 * secondNum
```

and assigns the value of this expression to the variable firstNum, which is 60 in the sample run. The statement in Line 15 outputs the new value of firstNum. The statement in Line 16 contains the return statement. The right brace in Line 17 marks the end of the function main.

## Debugging: Understanding and Fixing Syntax Errors

The previous sections of this chapter described the basic components of a C++ program. When you type a program, typos and unintentional syntax errors are likely to occur. Therefore, when you compile a program, the compiler will identify the syntax error. In this section, we show how to identify and fix syntax errors.

Consider the following C++ program:

```cpp
#include <iostream>

using namespace std;

int main()
{
    int num

    num = 18;

    tempNum = 2 * num;

    cout << "Num = " << num << ", tempNum = " << tempNum << endl;

    return;
}
```

(Note that the numbers 1 to 16 on the left side are not part of the program. We have numbered the statements for easy references.) This program contains syntax errors. When you compile this program, the compiler produces the following errors: (This program is compiled using Visual C++ Express 2008.)

```text
Example2_Syntax_Errors.cpp
c:\chapter 2 source code\example2_syntax_errors.cpp(9) : error C2146: syntax error :
missing ';' before identifier 'num'
c:\chapter 2 source code\example2_syntax_errors.cpp(11) : error C2065: 'tempNum' :
undeclared identifier
c:\chapter 2 source code\example2_syntax_errors.cpp(13) : error C2065: 'tempNum' :
undeclared identifier
c:\chapter 2 source code\example2_syntax_errors.cpp(13) : error C2563: mismatch in formal
parameter list
c:\chapter 2 source code\example2_syntax_errors.cpp(13) : error C2568: '<<': unable to
resolve function overload
    c:\program files\microsoft visual studio 9.0\vc\include\ostream(974): could be
'std::basic_ostream<_Elem,_Traits> & std::endl(std::basic_ostream<_Elem,_Traits> &)'
    with
        [
            _Elem=wchar_t,
            _Traits=std::char_traits<wchar_t>
        ]
    c:\program files\microsoft visual studio 9.0\vc\include\ostream(966): or
'std::basic_ostream<_Elem,_Traits> & std::endl(std::basic_ostream<_Elem,_Traits> &)'
    with
        [
            _Elem=char,
            _Traits=std::char_traits<char>
        ]
c:\program files\microsoft visual studio 9.0\vc\include\ostream(940): or
' std::basic_ostream<_Elem,_Traits> &std::endl(std::basic_ostream<_Elem,_Traits> &)'
c:\chapter 2 source code\example2_syntax_errors.cpp(15) : error C2561: 'main' : function
must return a value
    f:\vc1 c++ fifth edition\chapter 2\chapter 2 source code and prog ex\chapter 2
source code\example2_syntax_errors.cpp(5) : see declaration of 'main'
Build log was saved at "file:///C:\Documents and Settings\DM\My
Documents\Proj1\Proj1\Debug\BuildLog.htm"
Proj1 - 6 error(s), 0 warning(s)
========== Rebuild All: 0 succeeded, 1 failed, 0 skipped ==========
```

First, consider the following error:

```text
c:\chapter 2 source code\example2_syntax_errors.cpp(9) : error C2146:
syntax error : missing ';' before identifier 'num'
```

The expression example2_syntax_errors.cpp(9) indicates that there is an error in Line 9. The remaining part of this error specifies that there is a missing ; before the identifier num. If we look at Line 7, we find that there is a missing semicolon at the end of the statement int num. Therefore, we must insert ; at the end of the statement in Line 7.

Next, consider the second error:

```text
c:\chapter 2 source code\example2_syntax_errors.cpp(11) : error C2065: 'tempNum' :
undeclared identifier
```

This error occurs in Line 11, and it specifies that the identifier tempNum is undeclared. When we look at the code, we find that this identifier has not been declared. So we must declare tempNum as an int variable.

The error:

```text
c:\chapter 2 source code\example2_syntax_errors.cpp(13) : error C2065: 'tempNum' :
undeclared identifier
```

occurs in Line 13, and it specifies that the identifier tempNum is undeclared. As in the previous error, we must declare tempNum. Note that once we declare tempNum and recompile, this and the previous error will disappear.

The next error is:

```text
c:\chapter 2 source code\example2_syntax_errors.cpp(13) : error C2563: mismatch
in formal parameter list
```

This error occurs in Line 13, and it indicates that some formal parameter list is mismatched. For a beginner, this error is somewhat hard to understand. (In Chapter 15, we will explain the formal parameter list of the operator <<.) However, as you practice, you will learn how to interpret and correct syntax errors. This error becomes clear if you look at the next error, the part of which is:

```text
c:\chapter 2 source code\example2_syntax_errors.cpp(13) : error C2568: '<<' :
unable to resolve function overload
```

It tells us that this error has something to do with the operator `<<`. When we carefully look at the statement in Line 13, which is:

```cpp
cout << "Num = " << num << ", tempNum = " << tempNum << endl;
```

we find that in the expression `< tempNum`, we have unintentionally used `<` in place of `<<`. So we must correct this error.

Let us look at the last error, which is:

```text
c:\chapter 2 source code\example2_syntax_errors.cpp(15) : error C2561: 'main' :
        function must return a value
            c:\chapter 2 source code\example2_syntax_errors.cpp(5) : see declaration
        of 'main'
```

This error occurs in Line 15. However, at this point, the explanation given, especially for a beginner, is somewhat unclear. However, if you look at the statement `return ;` in Line 15 and remember the syntax of the function main as well as all the programs given in this book, we find that the number 0 is missing, that is, this statement must be `return 0;`

From the errors reported by the compiler, we see that the compiler not only identifies the errors, but it also specifies the line numbers where the errors occur and the types of the errors. We can effectively use this information to fix syntax error.

After correcting all of the syntax errors, a correct program is:

```cpp
#include <iostream>

using namespace std;

int main()
{
    int num;
    int tempNum;

    num = 18;

    tempNum = 2 * num;

    cout << "Num = " << num << ", tempNum = " << tempNum << endl;

    return 0;
}
```

The output is:

```text
Num = 18, tempNum = 36
```

As you learn C++ and practice writing and executing programs, you will learn how to spot and fix syntax errors. It is possible that the list of errors reported by the compiler is longer than the program itself. This is because a syntax error in one line can cause syntax errors in subsequent lines. In situations like this, correct the syntax errors in the order they
