# Answers to Self-Test Exercises 725

Definition:

```
template<class T>
T maximum(T first, T second)
{
    if (first < second)
        return second;
    else
        return first;
}
```

2. Function declaration:

```
template<class T>
T absolute(T value);
//Precondition: The expressions x < 0 and -x are defined
//whenever x is of type T.
```

Definition:

```
template<class T>
T absolute(T value);
{
    if (value < 0)
        return -value;
    else
        return value;
}
```

+   3. Templates provide a facility to allow the definition of functions and classes that have parameters for type names.

+   4. e. Any type, whether a primitive type (provided by C++) or a type defined by the user (class or struct type, enum type, or a type array, or int, float, double...), must be a type for which the code in the template makes sense. For example, the swapValues template function (Display 16.1), the type T must have a correctly working assignment operator.

+   5. The function declaration and function definition are given in the following code. They are basically identical to the versions in Display 5.6 except that instances of int are changed to T in the parameter list.

Function declaration:

```
template<class T>
int search(const T[], int numberUsed, T target);
//Precondition: numberUsed <= the declared size of a.
//Also, a[0] through a[numberUsed-1] have values.
//Returns the first index such that a[index] == target,
//provided there is such an index, otherwise returns -1.
```