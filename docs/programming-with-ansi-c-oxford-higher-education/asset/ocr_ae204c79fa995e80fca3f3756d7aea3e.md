```
Output
12 is bigger
sAddress is bigger
cAddress is bigger
```

# How the Program Works

It can be seen that the output is correct now. It should be noted that the definition of the original template is similar to the earlier definition.

```
template <typename T>
bool Max(T First, T Second)
{
    return(First > Second);
}
```

Now, look at the specialization.

```
template <>
bool Max(char *First, char *Second)
{
    return(strcmp(First, Second) > 0);
}
```

This is a special version for C-type strings as the arguments to the functions are char * rather than Type. The body now contains the strcmp() function, which can handle C-type strings. The template <> preceding the function header signifies that the definition following it is not a normal function but a specialization.

# Template Specialization vs Non-Generic Function

It is also possible to overload template definition with normal non-generic functions. The functions with headers can also be written as

```
void GenericBubbleSort(employee TempEmployee[], int Size)
```

or

```
bool Max(char *First, char *Second)
```

that is, by removing template <> from the definition of template specialization. Here, the original template is being overloaded with a non-generic function. Then, what is the difference between a template specialization and a non-generic (normal) function? The difference is that a generic function argument (the one that is overloaded) matching would be much more stringent than the normal function version.

Assume the SumIt() function is overloaded using a non-generic function for Employee objects. If the program has one more class Person, it is possible to write a conversion operator that converts a Person object to an Employee object in the Person class. We can, therefore, call now GenericBubbleSort() with Person array.

The templated function would not work as it expects only an Employee object. The templated version will not be called, as it requires converting the Person object to the Employee object. This, in turn, requires standard conversion, which is not possible with either automatically generated template functions or explicitly specified template functions.