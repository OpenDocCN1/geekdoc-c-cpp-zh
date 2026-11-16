```
{
    T temp;
    temp= a+b+sizeof(T);
    return temp;
}
```

Here, to avoid confusion, you can remember this as just replace int, float or any other data type by the typename which is T, here.

To call a function template, we use the following syntax:

```
func_name <data_type> (arg1,arg2,...);
```

So, our function can be called as :

```
random <int> (5,6);
```

Consider a function max(x,y) that returns the larger of its two arguments. x and y can be of any type that has the ability to be ordered. Because C++ is a strongly typed language, it expects the types of the parameters x and y to be declared at compile time. Without using templates, many overloaded versions of max() are required (one for each data type to be supported), even though the code for each version is essentially identical. Each version compares the arguments and returns the larger.

By using a template, you can define a pattern for a family of related overloaded functions by letting the data type be a parameter:

```
template <class T>

T max(T x, T y)
{
    return (x > y) ? x : y;
};
```

The data type is represented by the template argument <class T>. When you use this template in an application, the compiler generates the appropriate function according to the data type actually used in the call:

```
int i;
```

```
Myclass a, b;
```