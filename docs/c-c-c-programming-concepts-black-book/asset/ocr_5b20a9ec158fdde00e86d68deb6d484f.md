```
~~~cpp
try
{
    if (b == 0)
    {
        throw exceptionCode;
    }
    result = a/b;
}
catch (int e)
{
    if (e == 25)
    {
        cout<< "Divide by zero exception has occured" << endl;
        cout<< "Hence terminating..." << endl;
    }
    else
    {
        cout<< "Exception of unknown type has been found" << endl;
        cout<< "Hence terminating..." << endl;
    }
}
cout<< "Exiting the program..." << endl;
return 0;
}
~~~
```

The exception thrown in the preceding program is of type int. The catch block consists of a logic to decode this particular value and print a suitable error message. This is bad design since it requires the catch block. Moreover, a programmer needs to understand the possible exception rules and put into action the possibly complex logic. It is noteworthy to note that exception can be any kind of object. As we can throw any kind of object, let's attempt throwing an error message string, rather than an exception. Consider the following code:

```
~~~cpp
#include <iostream>
using namespace std;
int main()
{
    int a = 6;
    int b = 0;
    int result;
    try {
        if (b == 0) {
            throw "Divide by zero";
        }
        result = a/b;
    } // try block ends here
    catch (char *x) {
        cout<<x<< endl;
    }
    cout<< "Exiting the program..." << endl;
    return 0;
}
~~~
```

The preceding code is a better design. The catch block no more needs the detailed understanding of the exception. The code that throws the exception is passing information on the exception, which, in this case, is an error message. Suppose we have to bundle information, exception code, and the values of variables within the actual exception. Using a user-defined exception class may be ideal in this situation. Moreover, using a class object as an exception is regular for C++. Let's see how it is done in the following example: