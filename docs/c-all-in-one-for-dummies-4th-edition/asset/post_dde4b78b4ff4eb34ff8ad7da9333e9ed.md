
- **Declarative:** Functional programming actually implements the declarative programming paradigm, but the two paradigms are separate. Other paradigms, such as logic programming, implemented by the Prolog language, also support the declarative programming paradigm. The short view of declarative programming is that it does the following: describes what the code should do, rather than how to do it; defines functions that are referentially transparent (without side effects); and provides a clear correspondence to mathematical logic.

## Defining an Impure Language

Many developers have come to see the benefits of functional programming. However, they also don’t want to give up the benefits of their existing language, so they use a language that mixes functional features with one of the other programming paradigms (as described in the “Considering Other Programming Paradigms” sidebar). For example, you can find functional programming features in languages such as C++, C#, and Java. When working with an impure language, you need to exercise care because you can’t work in a purely functional manner, and the features that you might think will work in one way actually work in another. For example, you can’t pass a function to another function in some languages. The following sections help you understand why C++ is an impure functional language.

### Considering the requirements

The basis of functional programming is lambda calculus (https://brilliant.org/wiki/lambda-calculus/), which is actually a math abstraction. Every time you create and use a lambda function, you’re likely using functional programming techniques (in an impure way, at least). C++ supports lambda functions through the lambda expressions that later sections of this chapter explore.

In addition to using lambda functions, languages that implement the functional programming paradigm have some other features in common. Here is a quick overview of these features:

- **First-class and higher-order functions:** First-class and higher-order functions both allow you to provide a function as an input, as you would when using a higher-order function in calculus.
- **Pure functions:** A pure function has no side effects. When working with a pure function, you can
  - Remove the function if no other functions rely on its output
  - Obtain the same results every time you call the function with a given set of inputs
  - Reverse the order of calls to different functions without any change to application functionality
  - Process the function calls in parallel without any consequence
  - Evaluate the function calls in any order, assuming that the entire language doesn't allow side effects
- **Recursion:** Functional language implementations rely on recursion to implement looping. In general, recursion works differently in functional languages because no change in application state occurs.
- **Referential transparency:** The value of a variable (a bit of a misnomer because you can't change the value) never changes in a functional language implementation because functional languages lack an assignment operator.

### Understanding the C++ functional limitations

C++ is actually an extension of C. The original name of C++ was C with classes. So, theoretically, pure C++ is an OOP language. However, with the introduction of the Standard Library (see Book 5, Chapter 6 as well as Book 7 for more on the Standard Library), it becomes possible to add functionality to the language and make it more generic. The use of Standard Library enables you to use the functional programming paradigm in C++. However, even with Standard Library, you can't turn what started out as a procedural language and became an OOP language into a functional programming language. The best you can hope to achieve is a language that supports a number of paradigms — some of them in a general way.

What occurs in C++ for the most part is that you rely on the Standard Library to hide the nonfunctional programming components. For example, you can use constants in your C++ code to create an immutable environment. You use templates to create functions that don't rely on variables and therefore have no state. Using constants with methods can also help eliminate the problems with side effects. You see all these principles demonstrated as the chapter progresses. However, unlike a pure language, such as Haskell, these conventions aren't enforced in C++, and humans will routinely find ways around them when programming needs dictate.

Passing a function to a C++ function can also prove difficult unless you rely on the Standard Library. For example, you can use a transform to interact with a range of values by passing the transform function. As part of the strategy of passing functions to other functions, you can rely on lambda expressions for simple needs. However, passing complex functions is possible as well. When working with complex functions, however, many developers encase them in a typedef to make the code easier to read.

To create a pure function in C++, you must eliminate both state and side effects, which can be quite difficult. The process becomes especially difficult when working with external data, such as a file or a data stream. Obviously, a function that works with external data won't produce the same output every time you call it, but you can still reduce the problems of both state and side effects.

Even the use of recursion in place of the usual for or other looping mechanism can prove difficult in C++. In many cases, recursion relies on the use of mutable variables to track when the recursion should end. Careful use of various recursion strategies can make the use of mutable variables unnecessary, but doing so can be error prone and difficult (sometimes making the code hard to read).

![](img/128ab511de4e7360e167e3b15cdd5dd0_394_0.png)

The takeaway from this section is that you can use C++ in a functional manner, but it requires additional work to do so. The benefits of this approach are that multiprocessing applications are easier to create, the code is more concise, and the code is often easier to understand as well. In some cases, you can't use a functional programming style, especially when interacting with third-party libraries. However, if you work through coding issues using the Standard Library and some built-in C++ features, you can find yourself creating mostly functional code and obtaining the desired benefits from doing so.

## Seeing Data as Immutable

Being able to change the content of a variable is problematic in C++. The memory location used by the variable is important. If the data in a particular memory location changes, the value of the variable pointing to that memory location changes as well. The concept of immutable data requires that specific memory locations remain untainted. To create immutable data in C++, you must use constant variables, as in

```cpp
const double pi = 3.1415926;
```

The reason you need an immutable variable is that in a multiprocessing scenario, the value of the variable must be the same no matter which processor works with it. If x = 5 for one processor, it must equal 5 for all processors, and that value can never change. More important, the ability to change the value of a variable implies order, and functional programming techniques can’t rely on a specific order to accomplish their goals. Finally, immutable variables are reliable. You don’t have to worry about some bit of code, especially that from a hacker, modifying the values in your code because it seems like it might be a good idea. The following sections describe various forms of immutability in C++.

### Working with immutable variables

The Immutable example, shown in Listing 1–1, demonstrates three techniques for creating immutable variables. In all three cases, you can rely on the variable’s value to remain consistent and also rely on the compiler to complain about any changes.

**LISTING 1-1: Working with Constant Data**

```cpp
#include <iostream>

using namespace std;

struct Immutable{
    int val{};
};

int main() {
    const int *test1 = new int(5);
    *test1 = 10;

    const int test2[6];
    test2 = 11;

    const Immutable test3;
    test3.val = 12;

    cout << *test1 << test2 << test3.val << endl;
    return 0;
}
```
