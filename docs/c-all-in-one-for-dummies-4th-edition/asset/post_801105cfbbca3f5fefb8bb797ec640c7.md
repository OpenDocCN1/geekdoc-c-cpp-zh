
## Creating Classes with Templates

```cpp
int main() {
  Base<int> base_int;
  Base<double> base_double;

  Derived<int> derived_int;
  Derived<double> derived_double;

  TestInt(&base_int);
  TestInt(&derived_int);
  TestDouble(&base_double);
  TestDouble(&derived_double);

  //TestDouble(&derived_int);
  return 0;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_648_0.png)

The example has two functions, each taking a different class — and each class based on the first template, called Base. The first takes Base<int> * as a parameter, and the second takes Base<double> * as a parameter. When a function, such as TestInt() or TestDouble(), takes a pointer to a class, it can legally pass a pointer to an instance of a derived class, which means that you can create this variable:

```cpp
Derived<int> derived_int;
```

You pass this variable to the function that takes a Base<int> and it compiles. That means that Derived<int> is derived from Base<int>. In the same way, Derived<double> is derived from Base<double>. When you run this code, it outputs four numbers: two int values and two double values.

To see how Derived<int> relies on Base<int>, uncomment the line TestDouble(&derived_int). When you do this, and you try to compile the listing, you see this message:

```text
error: cannot convert 'Derived<int>*' to 'Base<double>*' for
argument '1' to 'void TestDouble(Base<double>*)'
```

The error message says you can't pass a pointer to Derived<int> to a function that takes a pointer to Base<double>. That's because Derived<int> isn't derived from Base<double>.

or other types. Instead of having a separate function for double and a separate function for every other type, you can use a template like this:

```cpp
template <typename T> T AbsoluteValue(T x) {
    if (x >= 0)
        return x;
    else
        return -x;
}
```

Now you need only one version of the function, which handles any numeric type, including double. The users of the function can, effectively, create their own versions of the function as needed. For example, to use an integer version of this function, you put the typename, int, inside angle brackets after the function name when calling the function:

```cpp
int n = -3;
cout << AbsoluteValue<int>(n) << endl;
```

If you want to use the function for a float, you do this:

```cpp
float x = -4.5;
cout << AbsoluteValue<float>(x) << endl;
```

Note the function template declaration. The real difference between the function template and a standard function is in the header:

```cpp
template <typename T> T AbsoluteValue(T x)
```

Begin with the word template, a space, and an open angle bracket (that is, a less-than sign). These characters are followed by the word typename, a closing angle bracket (that is, a greater-than sign), and then an identifier name. Most people like to use the name T (because it’s the first letter in type). At this point, you add the rest of the function header, which, taken by itself, looks like this:

```cpp
T AbsoluteValue(T x)
```

T represents a type. Therefore, this portion of the function header shows a function called AbsoluteValue that takes T as a parameter and returns T. Creating a function based on this template by using an integer, means that the function takes an integer parameter and returns an integer. When the compiler encounters a line like this:

```cpp
cout << AbsoluteValue<float>(x) << endl;
```

It creates a function based on the template, substituting float anywhere it sees T. However, if you have two lines that use the same type, as in this:

```cpp
cout << AbsoluteValue<float>(x) << endl;
cout << AbsoluteValue<float>(10.0) << endl;
```

The compiler creates only a single function for both lines.

![](img/128ab511de4e7360e167e3b15cdd5dd0_650_0.png)

### Overloading and function templates

If you really want to go out on a limb and create flexibility in your application, you can use overloading with a function template. Remember, overloading a function means that you create two different versions of a single function. What you're doing is creating two separate functions that have different parameters (that is, either a different number of parameters or different types of parameters), but they share the same name. Look at these two functions found in the FunctionOverloadingAndTemplates example:

```cpp
int AbsoluteValue(int x) {
    if (x >= 0)
        return x;
    else
        return -x;
}

float AbsoluteValue(float x) {
    if (x >= 0)
        return x;
    else
        return -x;
}
```

These functions are an example of overloading. They take different types as parameters. (One takes an int; the other takes a float.) Of course, you could combine these functions into a template:

```cpp
template <typename T> T AbsoluteValue(T x) {
    if (x >= 0)
        return x;
    else
        return -x;
}
```

There really isn’t any difference between the two examples. After all, you can use the following two lines of code either after the overloaded functions (without the type parameters) or after the function template:

```cpp
cout << AbsoluteValue<int>(n) << endl;
cout << AbsoluteValue<float>(x) << endl;
```

In this case, n is an int and x is a float. However, the template is a better choice. If you use the overloaded form and try this code, you see an error:

```cpp
cout << AbsoluteValue(10.5) << endl;
```

Even though 10.5 is a float, you see an error message like this:

```text
error: call of overloaded 'AbsoluteValue(double)' is ambiguous
```

The message contains AbsoluteValue(double), which means that the compiler thinks that 10.5 is a double, not a float. You can pass a double into either a function that takes an int or a function that takes a float. The compiler will just convert it to an int or a float, whichever it needs. Because the compiler thinks that 10.5 is a double, it can pass the value to either overloaded function version. So that leaves you with a choice: You can cast it to a float using (float)10.5; declare it a float using 10.5f; or create a third overloaded version of the function, one that takes a double.

Creating a template is easier than overcoming these sorts of errors. The second reason the template version is better: If you want a new type of the function, you don’t need to write another version of the function.

However, you can also overload a function template. The OverloadedFunctionTemplate example, shown in Listing 5-10, contains an overloaded function template.

### LISTING 5-10: Overloading a Function Template

```cpp
#include <iostream>

using namespace std;

template <typename T> T AbsoluteValue(T x) {
    cout << "(using first)" << endl;
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_654_0.png)

You can make life a little easier by using a small trick. Most compilers let you leave out the type in angle brackets in the function template call itself. The compiler deduces what type of function to build from the template, based on the types that you pass into the function call. Here's an example main() that you can substitute for the main() in Listing 5-10:

```cpp
int main() {
    int n = -3;
    cout << AbsoluteValue(n) << endl;
    float x = -4.5;
    cout << AbsoluteValue(x) << endl;
    cout << AbsoluteValue(10.5) << endl;
    return 0;
}
```

This code replaces AbsoluteValue<int>(n) with AbsoluteValue(n). When you run the modified code, you see the same output as when you run Listing 5-10.

### Templatizing a method

When you write a template for a class, you can put function templates inside the class template. You simply declare a function template inside a class, as in the following found in the MemberFunctionTemplate example:

```cpp
class MyMath {
public:
    string name;
    MyMath(string aname) : name(aname) {}

    template <typename T> void WriteAbsoluteValue(T x) {
        cout << "Hello " << name << endl;
        if (x >= 0)
            cout << x << endl;
        else
            cout << -x << endl;
    }
};
```

The WriteAbsoluteValue() method is a template. It's preceded by the word template and a template parameter in angle brackets. Then it has a return type, void, the function name, and the function parameter.
