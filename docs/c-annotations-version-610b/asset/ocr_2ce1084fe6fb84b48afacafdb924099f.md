Function objects are objects for which `operator()` has been defined. Function objects are not just used in combination with generic algorithms, but also as a (preferred) alternative to pointers to functions.

Function objects are frequently used to implement *predicate* functions. Predicate functions return boolean values. Predicate functions and predicate function objects are commonly referred to as 'predicates'. Predicates are frequently used by generic algorithms such as the `count`, if generic algorithm, covered in chapter 19, returning the number of times its function object has returned `true`. In the *standard template library* two kinds of predicates are used: *unary predicates* receive one argument, *binary predicates* receive two arguments.

Assume we have a class `Person` and an array of `Person` objects. Further assume that the array is not sorted. A well known procedure for finding a particular `Person` object in the array is to use the function `lsearch`, which performs a *linear search* in an array. Example:

```
```cpp
Person &target = targetPerson();    // determine the person to find
Person *pArray;
size_t n = fillPerson(&pArray);

cout << "The target person is";

if (!lsearch(&target, pArray, &n, sizeof(Person), compareFunction))
    cout << " not";
cout << "found\n";
```
```

The function `targetPerson` determines the person we're looking for, and `fillPerson` is called to fill the array. Then `lsearch` is used to locate the target person.

The comparison function must be available, as its address is one of the arguments of `lsearch`. It must be a real function having an address. If it is defined inline then the compiler has no choice but to ignore that request as inline functions don't have addresses. `compareFunction` could be implemented like this:

```
```cpp
int compareFunction(void const *p1, void const *p2)
{
    return *reinterpret_cast<Person const *>(p1)   // lsearch wants 0
           !=                                       // for equal objects
           *reinterpret_cast<Person const *>(p2);
}
```
```

This, of course, assumes that the `operator!=` has been overloaded in the class `Person`. But overloading `operator!=` is no big deal, so let's assume that that operator is actually available.

On average `n / 2` times *at least* the following actions take place:

+   1. The two arguments of the compare function are pushed on the stack;
+   2. The value of the final parameter of `lsearch` is determined, producing `compareFunction`'s address;
+   3. The compare function is called;
+   4. Then, inside the compare function the address of the right-hand argument of the `Person::operator!=` argument is pushed on the stack;
+   5. `Person::operator!=` is evaluated;
+   6. The argument of the `Person::operator!=` function is popped off the stack;
+   7. The two arguments of the compare function are popped off the stack.