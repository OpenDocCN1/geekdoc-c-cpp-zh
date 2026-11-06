
## Book IV: Chapter 5 — Creating Classes with Templates

```cpp
float AbsoluteValueFloat(float x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}
```

If the user of the functions needs to take the absolute value of an integer, he or she would use the AbsoluteValueInt() function. But to take the absolute value of a float, he or she would instead use the AbsoluteValueFloat() function. What about a double? Or some other numerical type?

But instead of having a separate function for double and a separate function for every other type, we would suggest using a template, as in this:

```cpp
template <typename T> T AbsoluteValue(T x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}
```

Now you need only one version of the function, which handles any numeric type, including double. The users of the function can, effectively, create their own versions of the function as they need them. For example, to use an integer version of this function, we just put the typename, int, inside angle brackets after the function name when calling the function:

```cpp
int n = -3;
cout << AbsoluteValue<int>(n) << endl;
```

And if we want to use the function for a float, we just do this:

```cpp
float x = -4.5;
cout << AbsoluteValue<float>(x) << endl;
```

Note how we declared the function template itself. The real difference between the function template and a regular run-of-the-mill function is in the header:

```cpp
template <typename T> T AbsoluteValue(T x)
```

First we put the word template. Then we follow it with any number of optional spaces, and then an open angle bracket (that is, a less-than sign). Following the angle bracket, we put the word typename, a close angle bracket (that is, a greater-than sign), and then an identifier name. Most people like to use the name T (since it's the first letter in *type*), so that's what we did, being ones to follow the crowd. Then we put in the rest of the function header, which, taken by itself, looks like this:

```cpp
T AbsoluteValue(T x)
```

Remember, T represents a type. Therefore, this portion of the function header shows a function called AbsoluteValue that takes T as a parameter and returns T. So if we create a function based on this template by using an integer, the function will take an integer as a parameter and return an integer. Remember, T is basically a placeholder for a typename. So when the compiler encounters a line like this:

```cpp
cout << AbsoluteValue<float>(x) << endl;
```

it creates a function based on the template, substituting float anywhere it sees T.

However, if you have two lines that use the same type, as in this

```cpp
cout << AbsoluteValue<float>(x) << endl;
cout << AbsoluteValue<float>(10.0) << endl;
```

the compiler only creates a single function for both lines. (And these two lines don't need to be one after the other.)

### Overloading and function templates

If you really want to go out on a limb and create flexibility in your application, you can use overloading with a function template. Remember, *overloading a function* means that you create two different versions of a single function. Really, what you're doing is creating two separate functions that have different parameters (that is, either a different number of parameters or different types of parameters), but they share the same name.

Look at these two functions found in the `FunctionOverloadingAndTemplates` example:

```cpp
int AbsoluteValue(int x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}

float AbsoluteValue(float x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}
```

These functions are an example of overloading. They take different types as parameters. (One takes an int, and the other takes a float.) Of course, you could combine these functions into a template:

```cpp
template <typename T> T AbsoluteValue(T x)
{
    if (x >= 0)
        return x;
    else
        return -x;
}
```

But is this really any different? After all, you can use the following two lines of code either after the overloaded functions or after the function template:

```cpp
cout << AbsoluteValue<int>(n) << endl;
cout << AbsoluteValue<float>(x) << endl;
```

(We’re assuming that n is an integer and x is a float.) However, the template is a better choice. First, if you use the overloaded form and then try this, you’ll get a problem:

```cpp
cout << AbsoluteValue(10.5) << endl;
```

We all know that 10.5 is a float; therefore, the compiler should just call the float version of the overloaded function. However, the GNU GCC compiler that ships with Code::Blocks gives us this error message:

```text
error: call of overloaded ‘AbsoluteValue(double)’ is ambiguous
```

Ambiguous? But look! The message is saying AbsoluteValue (double)! Hmmm . . . apparently, the GNU GCC compiler thinks that our 10.5 is a double, not a float. And you can actually pass a double into either a function that takes an int or a function that takes a float. The compiler will just convert it to an int or a float, whichever it needs. And because the compiler thinks that 10.5 is a double, it figures it can pass it to either version of the overloaded function. So that leaves you a choice: You can either cast it to a float or create a third overloaded version of the function, one that takes a double.

Yuck. At least Code::Blocks gives you some clue as to the problem because the extended error information is

```text
note: candidates are: int AbsoluteValue(int)
note:                 float AbsoluteValue(float)
```

Creating a template is easier. And that brings us to the second reason the template version is better: If you want a new type of the function, you don’t need to write another version of the function.

But what if you want to overload a function template? That sounds kind of scary, but you can do it. The OverloadedFunctionTemplate example shown in Listing 5-9 contains an overloaded function template.

### Listing 5-9: Overloading a Function Template Provides Even Greater Flexibility

```cpp
#include <iostream>

using namespace std;

template <typename T> T AbsoluteValue(T x)
{
    cout << "(using first)" << endl;
    if (x >= 0)
        return x;
    else
        return -x;
}

template <typename T> T AbsoluteValue(T *x)
{
    cout << "(using second)" << endl;
    if (*x >= 0)
        return *x;
    else
        return -(*x);
}

int main()
{
    int n = -3;
    cout << AbsoluteValue<int>(n) << endl;

    float *xptr = new float(-4.5);
    cout << AbsoluteValue<float>(xptr) << endl;
    cout << AbsoluteValue<float>(10.5) << endl;

    return 0;
}
```

When we pass a pointer (as in the second call to AbsoluteValue() in main()), the compiler figures out that it needs to use the second version of the template. And just to be sure which version gets used and at what time during application execution, we threw in a cout line at the beginning of each function template. When you run this code, here’s what you see:

```text
(using first)
3
(using second)
4.5
(using first)
10.5
```

From the middle two lines you can see that the computer did indeed call the second version of the template.

You can make life a little easier by using a little trick. Most compilers let you leave out the type in angle brackets in the function template call itself. The compiler is smart enough to figure out what type of function to build from the template, based on the types that you pass into the function call! Pretty wild. Here's an example main() that you can substitute for the main() in Listing 5-9:

```cpp
int main()
{
    int n = -3;
    cout << AbsoluteValue(n) << endl;

    float *ptr = new float(-4.5);
    cout << AbsoluteValue(ptr) << endl;
    cout << AbsoluteValue(10.5) << endl;

    return 0;
}
```

In this code, we replaced AbsoluteValue<int>(n) with just AbsoluteValue(n). When you run the modified Listing 5-9, you see the same output as when you run Listing 5-9.

### Templatizing a member function

When you write a template for a class, you can put function templates inside the class template. To people who were familiar with some of the early versions of C++ where template support was minimal, this seems a little shocking. But when the electrical current wears off, we all see that putting a template function inside a template class is possible. You simply declare a function template inside a class, as in the following:

```cpp
class MyMath
{
public:
    string name;

    MyMath(string aname) : name(aname) {}

    template <typename T> void WriteAbsoluteValue(T x)
    {
        cout << "Hello " << name << endl;
        if (x >= 0)
```
