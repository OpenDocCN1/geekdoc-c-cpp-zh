# 2.9 YOUR FIRST C++ PROGRAM

```
/*PROG 2.1 PRINTS HELLO C++ ON THE SCREEN */

#include <iostream.h>
int main()
{
    cout << " Hello C++";
    return 0;
}

OUTPUT :
Hello C++
```

![](bbox=[0.303, 0.383, 0.698, 0.466])

Figure 2.3. Output screen of program 2.1.

EXPLANATION: In the first line #include is a preprocessor directive, iostream.h is a header file which is written enclosed in < and > or in "". "io" in iostream stands for input output, .h stands for header file. The file iostream.h has to be included in every C++ program. There may be space between #include and <iostream.h>. Next line is the function main () due to symbol () which is known as function symbol. This function must be present in every C++ file you make because execution of your C++ program starts from this main (). {is the opening braces for main function and } is the closing brace. All the statements, instructions are written inside the main function. The int before main is treated as its return type. cout is the predefined object of class iostream_withassign which is defined in iostream.h. The symbol << is an operator known as put to or insertion operator. The combined effect of cout << is that whatever is written after it is in double quotes is printed onto the screen, so the output. Every statement in a C++ program has to end with; (semicolon). C++ is case sensitive programming language, so whatever you use that is in-built in C++ has to be in lower case. The line return 0; is simply for the omission of warning. If you do not write return 0; you will not get any error but a warning. The above program can be modified as (with a little change in return type of function main).

```
void main()
{
    cout << "Hello C++";
}
```