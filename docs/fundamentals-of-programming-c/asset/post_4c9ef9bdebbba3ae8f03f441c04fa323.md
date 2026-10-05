
## 10.2. STATIC VARIABLES

```cpp
int increment_and_report(int n) {
  cout << "Incrementing " << n << endl;
  return n + 1;
}
```

A pure function simply computes its return value and has no other observable side effects.

A function that uses pure functions and otherwise would be considered itself a pure function; for example:

```cpp
int double_increment(int n) {
  return increment(n) + 1;
}
```

double_increment is a pure function because increment is pure; however, double_increment_with_report:

```cpp
int double_increment_with_report(int n) {
  return increment_and_report(n) + 1;
}
```

is not a pure function because it calls increment_and_report which is impure.

## 10.2 Static Variables

Space in the computer's memory for local variables and function parameters is allocated at run time when the function begins executing. When the function is finished and returns, the memory used for the function's local variables and parameters is freed for other purposes. If a function is never called, the variable's local variables and parameters will never exceed the computer's memory.

Because a function's locals are transient, a function cannot retain any information between calls. C++ provides a way in which a local variable to a function can be retained between calls. Listing 10.3 (counter.cpp) shows how a local variable static allows it to remain in the computer's memory for the duration of the program's execution.

Listing 10.3: counter.cpp

```cpp
#include <iostream>
#include <iomanip>

using namespace std;

/*
 * count
 * Keeps track of a count.
 * Returns the current count.
 */
int count() {
  // cnt's value is retained between calls because it
  // is declared static
  static int cnt = 0;
  return ++cnt; // Increment and return current count
}

int main() {
    // Count to ten
    for (int i = 0; i < 10; i++) {
        cout << count() << ' ';
        cout << endl;
    }
}
```

In Listing 10.3 (counter.cpp), the count function is called 10 times. Each time it returns a tally of the number of times it has been called:

![](img/e326304bd50fbc4f7d5a64c1487eb635_246_0.png)

By contrast, if you remove the word static from Listing 10.3 (counter.cpp), compile it, and rerun it, it prints:

![](img/e326304bd50fbc4f7d5a64c1487eb635_246_1.png)

because new memory is allocated for the cnt variable each time count is called.

The local declaration

static int cnt = 0;

allocates space for cnt and assigns zero to it once—at the beginning of the program's execution. The space set aside for cnt is not released until the program finishes executing.

Recall Listing 9.7 (evenbetterprompt.cpp) that included the following function:

```cpp
int prompt(int n) {
    int value;
    cout << "Please enter integer #" << n << " ";
    cin >> value;
    return value;
}
```

The caller, main, uses prompt function as follows:

```cpp
int value, value2, sum;
cout << "This program adds together two integers." << endl;
value = prompt(1); // Call the function
value2 = prompt(2); // Call the function again
sum = value + value2;
```

The first call to prompt prints the message

![](img/e326304bd50fbc4f7d5a64c1487eb635_246_2.png)

and awaits the user's input. The second call prints the message

```
Please enter integer #2:
```

Another caller might use **prompt** within a loop like this:

```cpp
int sum = 0;
for (int i = 1; i < 10; i++)
sum += prompt(i);
```

Notice that it is the caller's responsibility to keep track of the proper number to pass to **prompt**. The caller may make a mistake and pass the wrong number or not want to manage such details. It would be better to move the responsibility of tracking input count to **prompt**. `static` variables make that possible, Listing 10.4 (promptwithstatic.cpp)

Listing 10.4: promptwithstatic.cpp
```cpp
#include <iostream>
using namespace std;
/*
* prompt requests an integer from the user and
* keeps track of the cumulative number of entries.
* Returns the value entered by the user.
*/
int prompt() {
    static int count = 0;
    int value;
    cout << "please enter integer #" << ++count << "; ";
    cin >> value;
    return value;
}

int main() {
    int value1, value2, sum;
    cout << "This program adds two integers." << endl;
    value1 = prompt(); // Call the function
    value2 = prompt(); // Call the function again
    sum = value1 + value2;
    cout << value1 << " = " << value2 << " = " << sum << endl;
}
```

Listing 10.4 (promptwithstatic.cpp) behaves just like Listing 9.7 (evenbetterprompt.cpp), but in the new variable main does not have to keep track of the number of entries.

Local `static` variables were inherited from the C programming language, but in C++ (see Chapter 14). Functions with `static` variables provide a way to implement executable objects with persistent state. Objects provide a more natural and more flexible way to achieve the same effect.

## 10.3. OVERLOADED FUNCTIONS

In C++, a program can have multiple functions with the same name. When two or more functions in a program have the same name, the function is said to be *overloaded*. The functions must be different somehow, or the compiler would not know how to associate a call with a particular function definition. The compiler identifies a function by name and its parameter list; a function is uniquely identified by its *signature*. A function signature consists of the function's name and its parameter list. In the parameter list, only the types of the formal parameters are important, not their names. If the parameter types do not match, both in name and position, then the functions are different. Consider the following overloaded functions:

- `void f() { /* ... */ }`

This version has no parameters, so its signature differs from all the others which have at least one parameter.

- `void f(int x) { /* ... */ }`

This version differs from Version 3, as its single parameter is an *int*, not a *double*.

- `void f(double x) { /* ... */ }`

This version differs from Version 2, as its single parameter is a *double*, not an *int*.

- `void f(int x, double y) { /* ... ... */ }`

This version differs from Version 5, even though Versions 4 and 5 have the same number of parameters with the same types, the order of the types is different.

- `void f(double x, int y) { /* ... ... */ }`

See the comments for Version 4.

Overloaded functions are a convenience for programmers. If overloaded functions were not allowed (many languages do not support), new names must be created for different functions. It is better for the programmer to choose the same name and let the compiler properly resolve.

## 10.4. Recursion

The *factorial* function is widely used in combinatorial analysis, probability, and statistics. The *factorial* of n is often defined as:

```
n! = {
if n = 0
n · (n-1).
}
```

A C++ function can be defined recursively as well. Listing 10.5 (factorial.cpp) includes a factorial function that exactly models the mathematical definition.

# Listing 10.5: factorial.cpp

```cpp
#include <iostream>

using namespace std;

/*
 * factorial(n)
 * Computes n!
 * Returns the factorial of n.
 */
int factorial(int n) {
    if (n == 0)
        return 1;
    else
        return n * factorial(n - 1);
}

 main() {
    // Try out the factorial function
    cout << "0! = " << factorial(0) << endl;
    cout << "1! = " << factorial(1) << endl;
    cout << "6! = " << factorial(6) << endl;
    cout << "10! = " << factorial(10) << endl;
}
```

Observe that the factorial function in Listing 10.5 (factorial.cpp) uses no loop to compute the result. The factorial function simply calls itself. The call factorial(6) is computed as follows:

```
factorial(6) = 6 * factorial(5)
= 6 * 5 * factorial(4)
= 6 * 5 * 4 * factorial(3)
= 6 * 5 * 4 * 3 * 2 * factorial(2)
= 6 * 5 * 4 * 3 * 2 * 1 * factorial(1)
= 6 * 5 * 4 * 3 * 2 * 1 * 1
= 6 * 5 * 4 * 3 * 2 * 1
= 6 * 5 * 4 * 6
= 6 * 5 * 24
= 720
```

Note that the factorial function can be slightly optimized by changing the if' condition from (n == 0) to (n < 2). This change results in a function execution time that eliminates two function calls at the end:

```
factorial(6) = 6 * factorial(5)
= 6 * 5 * factorial(4)
= 6 * 5 * 4 * factorial(3)
```
