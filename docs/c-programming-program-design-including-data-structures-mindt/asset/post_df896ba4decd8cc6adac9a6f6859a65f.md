
From the input stream. The statement in Line 22 uses the member function `remove` of `stringList` to remove the string from `stringList`. The statement in Line 24 outputs the modified `stringList`. The statements in Lines 29 through 32 test the function `seqSearch`.

**NOTE** The website accompanying this book contains additional programs illustrating how to use the `class template unorderedArrayListType` to create lists of `double` elements and `clockType` objects.

Just as we can derive the `class template unorderedArrayListType` from the abstract `class template arrayListType` to manipulate unordered lists, we can also derive the `class template orderedArrayListType` to manipulate ordered lists. (See Programming Exercise 23 at the end of this chapter.)

## C++11 Random Number Generator

In Chapter 5, we discussed how to generate random numbers using the functions `rand` and `srand`. However, statistically the function `rand` is not as random as one would like and its outcome can be predicted. C++11 provides many functions to implement a random number generator. In this section, we briefly discuss how to use C++ random number generator utilities in a program.

To use C++11 random number generator functions we use an engine and a distribution. An engine returns unpredictable (random) bits. The chances of obtaining a 0 bit are always the same as the chances of obtaining 1 bit. A distribution returns random numbers whose likelihoods correspond to a specific shape such as a uniform or normal distribution. Consider the following statements:

```
default_random_engine num{};                         //Line 1
uniform_int_distribution<unsigned int> randomNum{1, 6}; //Line 2
```

The first statement declares `num` to be an object of type `default_random_engine`, which is a `class`. The second statement declares `randomNum` to be an object of type `uniform_int_distribution`, which is a `class template`. The values 1 and 6 in parentheses specify that the object `randomNum` randomly generates an unsigned int between 1 and 6.

The following expression generates the next random number between 1 and 6:

```
randomNum(num)    //Line 3
```

The definitions of the classes `default_random_engine` and `uniform_int_distribution`, and other classes used to generate random numbers are contained in the header file `random`.

The statements in Lines 1 to 3 will always generate the same sequence of numbers every time you run a program that contains these statements. As in Chapter 5, to generate a different sequence of numbers every time we run the program, we use an object of type `random_device` to obtain a seed, as follows.

```
random_device rddevice{};
default_random_engine num{ rddevice() };
```

Consider the following program:

```
//C++11: Random number generator.

#include <iostream>
#include <random>

using namespace std;

int main()
{
    random_device rddevice{};
    default_random_engine num{ rddevice() };
    uniform_int_distribution<unsigned int> randomNum{1, 6};

    for (unsigned int count = 1; count <= 10; count++)
        cout << randomNum(num) << " ";
    cout << endl;

    return 0;
}
```

### Sample Runs

**Sample Run 1:**

```
3 2 5 6 5 2 5 5 5 3
```

**Sample Run 2:**

```
2 1 6 1 2 5 4 5 3 6
```

The statements to declare the objects `rddevice`, `num`, and `randomNum` work as explained before. The `for` loop executes 10 times, generating a sequence of 10 random numbers using the objects `randomNum` and `num`.

To generate random real numbers we use the class `uniform_real_distribution` as follows:

```
random_device rddevice{};
default_random_engine num{ rddevice() };
uniform_real_distribution<double> randomRealNum {1, 40};
```

The first two statements are the same as before. In the third statement, the object `randomRealNum` randomly generates a random number between 1 and 40 of type `double`.

Note that the C++11 standard library provides 25 distribution types in five categories. For example, `uniform_int_distribution` and `uniform_real_distribution` fall in the category of uniform distributions.

## Quick Review

1. An operator that has different meanings with different data types is said to be overloaded.
2. In C++, `>>` is used as a stream extraction operator and as a right shift operator. Similarly, `<<` is used as a stream insertion operator and as a left shift operator. Both are examples of operator overloading.
3. Any function that overloads an operator is called an operator function.
4. The syntax of the heading of the operator function is:
   `returnType operatorSymbol(parameters)`
5. In C++, `operator` is a reserved word.
6. Operator functions are value-returning functions.
7. Except for the assignment operator and the member selection operator, to use an operator on class objects, that operator must be overloaded. The assignment operator performs a default member-wise copy.
8. For classes with pointer member variables, the assignment operator must be explicitly overloaded.
9. Operator overloading provides the same concise notation for user-defined data types as is available for built-in data types.
10. When an operator is overloaded, its precedence cannot be changed, its associativity cannot be changed, default parameters cannot be used, the number of parameters that the operator takes cannot be changed, and the way in which an operator works with built-in data types remains the same.
11. It is not possible to create new operators. Only existing operators can be overloaded.
12. Most C++ operators can be overloaded.
13. The operators that cannot be overloaded are `.`, `.*`, `::`, `?:`, and `sizeof`.
14. The pointer `this` refers to the object as a whole.
15. The operator functions that overload the operators `()`, `[]`, `->`, or `=` for a class must be members of that class.
16. A `friend` function is a nonmember of a class.
17. The heading of the prototype of a `friend` function is preceded by the word `friend`.
18. In C++, `friend` is a reserved word.
19. If an operator function is a member of a class, the far left operand of the operator must be a class object (or a reference to a class object) of that operator’s class.
20. The binary operator function as a member of a class has only one parameter; as a nonmember of a class, it has two parameters.
21. The operator functions that overload the stream insertion operator, `<<`, and the stream extraction operator, `>>`, for a class must be `friend` functions of that class.
22. To overload the pre-increment (`++`) operator for a class if the operator function is a member of that class, it must have no parameters. Similarly, to overload the pre-decrement (`--`) operator for a class if the operator function is a member of that class, it must have no parameters.
23. To overload the post-increment (`++`) operator for a class if the operator function is a member of that class, it must have one parameter, of type `int`. The user does not specify any value for the parameter. The dummy parameter in the function heading helps the compiler generate the correct code. The post-decrement operator has similar conventions.
24. A conversion constructor is a single-parameter function.
25. A conversion constructor converts its argument to an object of the constructor’s class. The compiler implicitly calls such constructors.
26. Classes with pointer member variables must overload the assignment operator and include both the copy constructor and the destructor.
27. In C++, a function name can be overloaded.
28. In C++, `template` is a reserved word.
29. Using templates, you can write a single code segment for a set of related functions—called the function template.
30. Using templates, you can write a single code segment for a set of related classes—called the class template.
31. The syntax of a template is

```
template <class Type>
declaration;
```

in which `Type` is a user-defined identifier, which is used to pass types (that is, data types) as parameters, and `declaration` is either a function or a class. The word `class` in the heading refers to any user-defined data type or built-in data type.

32. Class templates are called parameterized types.
33. In a class template, the parameter `Type` specifies how a generic class template is to be customized to form a specific template class.
34. The parameter `Type` is mentioned in every class header and member function definition.
