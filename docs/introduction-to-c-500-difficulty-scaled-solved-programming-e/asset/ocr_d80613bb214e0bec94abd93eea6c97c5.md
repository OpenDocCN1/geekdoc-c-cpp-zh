declares the variable arr as an array of 100 floats. If we ever need to make the type of the array
double, we just change float to double. The declarations of the variables arr remain as is; we
don't have to change them.

Because we create a synonym for an existing type, you might think this is redundant. No,
is not not true. For example if you are going to run on systems where the data types are system
dependent it is very helpful to use a synonym. For example, the statement:

```
typedef short int size_i;
```

makes the type of all size_i variables short int. In these cases variables must be int in another plat-
form we just change short int to int and they become int. The use of synonyms helps us to
adjust our types very easily in different requirements.

Another common use is to create synonyms of complex types, so that we don't have to repeat them.
For example:

```
typedef int (*pcpy) (const char *s1, const char *s2, int len);
```

pcpy is a synonym for a pointer to a function that returns an integer and two arguments of type
const char* and an integer. To create the synonym, we write the prototype and in place of
the function we put the expression (*pointer_name). Now we can use the synonym to declare
variables of that type. For example:

pcpy p_cpy1, p_cpy2, p_cpy3;

As you see, the types of variables are read and written much easier than with the conventional way.
Alternatively, instead of creating a synonym to a pointer, although this is the most popular approach, we
create a synonym to the respective function and then declares pointer. For example:

```
typedef int pfunc(const char *s1, const char *s2, int len);
pfunc *p_cpy1, p_cpy2, p_cpy3;
```

Generally, the creation of synonyms is put in a header file, so that we can include it in any source file
C++11 provides another way to create synonyms by using the using keyword. For example, the

```
using pint = int*
```

makes the name pint synonym of the int* type. Another example:

```
using fp = void(*)(int);
```

the name fp becomes synonym to a pointer type to a function that accepts an int and returns nothing.
t same declaration with typedef would be:

```
typedef void (*)(int);
```

The using syntax looks more intuitive compared to typedef as it resembles an ordinary assign-
ment. Also, using allows us to create clear aliases for templates (e.g., we'll see them in Chapter 16), which is
someth we cannot do with typedef.