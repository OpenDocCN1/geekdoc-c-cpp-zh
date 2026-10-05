
## 718 Introduction to C++

management easier to read and control. Let's see the syntax of a typical example how to throw and catch exceptions:

```cpp
f()
{
    try {
        g();
    } catch(type exc_1) {
        ...
    }
    catch(type exc_2) {
    }
    catch(...) // catches any type of exception {
    
}
}
g()
()
{
    ...
    if (error_occurs) {
        throw exception; // g() creates an exception.
    }
}
```

The idea is that if an error occurs in a function (e.g., g()) and the function cannot handle the error, it can use the throw statement to create an exception that informs the calling function for the error. In order to catch the exception, the call of the function that can create exceptions must be placed in a block that begins with the try statement. The code that handles exceptions is placed right after the try statement and pass to one or more blocks that begin with the catch keyword. Note that it is not allowed to put any code between the try block and the first catch or between successive catch blocks; the program will not compile. Each catch specifies the type of exception it can catch. Because it handles, it is also referred to as an exception handler. The type can be a basic type or a user-defined type. It is identified by a single parameter within parentheses after the catch keyword.

The basic concept of exceptions is being able when "exceptional" occurs in one part of the program (e.g., g()), this part is able to inform another part (e.g., f()) of this "exceptional" event and pass to that information related to the event. The programmer determines what is "exceptional". Note that the "exceptional" event does not always have to be catastrophic, the programmer should specify its seriousness, it may be the inability to perform a task. Taskally, creating an exception is a way for the program that cannot locally handle an "exceptional" event (e.g., g()) to forward it to a higher level (e.g., f()) that may be able to handle it.

## Catching Exceptions

The throw statement creates an exception and its argument specifies the type of the thrown exception. The throw terminates the execution of the current function (e.g., g()) and the execution of the program is transferred to the calling function (e.g., f()). There, the program examines sequentially the catch statements to see if one matches the type of the thrown exception. For example, the statement throw creates an exception of int and passes the value 20. If there is a catch statement for integer exceptions, such as catch(int a), it will catch the exception, the value of a will become 20 and the code in the block will be executed. The exception will not be caught because the compiler does not perform the usual arithmetic. The conversions are limited. In particular, it supports type conversions const specifiers. For example, a non-const integer of the throw can match a const integer argument of the catch. It also ports from a derived type to a base class type, as well as the conversion of an array or function to the respective pointer.

The catch block may contain code to fix the problem, if it can be fixed. If not, the programmer may decide to terminate the program. The remaining blocks are not checked. Whether it is necessary to declare parameter names, we can write catch(int). Usually, the argument passed to the catch statement provides information related to the exception, so the catch parameter is used to hold this statement.

The catch(...) is optional and catches all types of exceptions. It catches an exception that is not caught by any of the previous catch blocks. It is a bit like the default case in the switch statement. Notice that it should be placed at the end of the catch block. If it is placed in another place, it catches all the exceptions, which the catch statement says after won't be checked. If we discuss about exception forwarding, the exception is passed on to main(), until a matching catch block is found. If no block is found to catch the exception, the program terminates.

The catch(...) is particularly useful when we do not know what the calling function throws exceptions. For example, if we do not know that g() or a function that g() calls exceptions (nor of their types), we can catch them in the catch(...) block. Since the catch(...) catches exceptions of any type someone could say why not to use only this block and all exceptions except wasting time to add separate catch blocks for every possible exception. That is, to write something like this:

```cpp
try
{
  g();
}
catch(...)
{
}
```

Yes, you can do that, but this approach does not provide any information about the exception in order to handle properly and identify the problem. If you know possible exception types it is preferable to separate catch blocks that explicitly state which exceptions may be thrown. Then, you can handle each exception, which may need more specific handling, individually. Also, when we discuss about exceptions, we'll see that we can use general information to aid in handling and detecting the error.

If no exception is thrown in the try block, the catch blocks are skipped and the program continues with the statement following the try-catch statement if it is valid.

```cpp
#include <iostream> // Example 22.1
#include <string>

using std::cout;
using std::cin;
using std::string;
```

int check_pswd(const string& str);

int main() {
    string pswd;

    while(1) {
        try {
            cout << "Enter password: ";
            cin >> pswd;
            if (pswd == "end") break;
            check_pswd(pswd);
        } catch (const string& msg) {
            cout << "Error: " << msg << endl;
        } catch (int code) {
            cout << "Error code: " << code << endl;
        } catch (...) {
            cout << "Unknown error" << endl;
        }
    }
    return 0;
}

void check_pswd(const string& str) {
    bool found = false;
    int dig = 0;
    int len = str.size();

    for (int i = 0; i < len; i++) {
        if (str[i] >= '0' && str[i] <= '9') {
            dig++;
        } else if (str[i] == '!' || str[i] == '$' || str[i] == '#') {
            found = true;
        }
    }

    if (len < 6) {
        throw string("Short length!");
    }
    if (dig < 3) {
        throw 10;
    }
    if (!found) {
        throw string("Missing special characters!");
    }
    cout << "Password accepted!" << endl;
}
