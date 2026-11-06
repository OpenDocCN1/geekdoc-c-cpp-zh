There really isn’t any difference between the two examples. After all, you can use the following two lines of code either after the overloaded functions (without the type parameters) or after the function template:

```
cout << AbsoluteValue<int>(n) << endl;
cout << AbsoluteValue<float>(x) << endl;
```

In this case, n is an int and x is a float. However, the template is a better choice. If you use the overloaded form and try this code, you see an error:

```
cout << AbsoluteValue(10.5) << endl;
```

Even though 10.5 is a float you see an error message like this:

```
error: call of overloaded 'AbsoluteValue(double)' is ambiguous
```

The message contains AbsoluteValue(double), which means that the compiler thinks that 10.5 is a double, not a float. You can pass a double into either a function that takes an int or a function that takes a float. The compiler will just convert it to an int or a float, whichever it needs. Because the compiler thinks that 10.5 is a double, it can pass the value to either overloaded function version. So that leaves you with a choice: You can cast it to a float using (float)10.5; declare it a float using 10.5f; or create a third overloaded version of the function, one that takes a double.

Creating a template is easier than overcoming these sorts of errors. The second reason the template version is better: If you want a new type of the function, you don’t need to write another version of the function.

However, you can also overload a function template. The OverloadedFunction—Template example, shown in Listing 5–10, contains an overloaded function template.

# LISTING 5-10: **Overloading a Function Template**

```
#include <iostream>

using namespace std;

template <typename T> T AbsoluteValue(T x) {
    cout << "(using first)" << endl;
```