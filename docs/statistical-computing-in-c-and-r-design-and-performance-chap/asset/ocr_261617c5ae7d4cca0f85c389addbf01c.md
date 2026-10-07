# A SKETCH OF C++

will the compiler to lodge a complaint of the form

```
typeError.cpp: In function int main() :
typeError.cpp:4: error: 'x' was not declared in this scope
```

Note that this is the typical form of an error message returned by the Gnu C++ compiler tells us the name of the file where the error occurred (i.e., typeError.cpp), the name of
t function in the file which contains the error (i.e., main) and gives the line number in
t program (specifically, line 4 in the file typeError.cpp) where the error was detected.

In C there is a distinction between a declaration and a statement with the former having
t purpose of informing storage requirements while the latter executes an
a (or actions) on a variable (or variables), performs writing operations, etc. Under the
der C standards, declarations and statements cannot be mixed. There is more flexibility
in C++ that declarations are also viewed as statements which allows them to be mixed
 executable statements. For example, the snippet

```
int main() {
int x, y;
x = 0; y = 0;
int z = x + y;
return 0;
}
```

is legal in C++. However, the fourth line of code int z = x + y; is illegal in some versions
of C*. The ability to mix declarations and code will feature prominently in C++ for loops
as seen in Section 3.4.

As another example of C++ code, the listing below is the obligatory "Hello World"
program that writes a greeting to standard output (typically the shell).

```
//hello.cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
string s;
s = "Hi ya'll";
cout << s << endl;
return 0;
}
```

The optional arguments (argv and argc) to main, that were not needed in this instance,
have been omitted. Then, a variable (although more precisely, a data object in case)
type string is used to hold the output phrase before it is directed to the shell by the
out stream object cin introduced in Section 2.2. The string class will be discussed in
detail in Section 3.8.5. For now we note that an include statement has been
used to make the class available and the double quotes are needed to define a string
object.

As in Chapter 2, to run the program from a Unix environment the Gnu C++ compiler
in invoked from the shell command line

```
$ gcc -Wall hello.cpp -o hello
```

* Actually this code will compile without error, e.g., the Gnu C compiler gcc. Using gcc with the
-pedantic option will produce the warning that the ISO (International Organization for Standardization)
C90 standard "forbids mix declarations and code"