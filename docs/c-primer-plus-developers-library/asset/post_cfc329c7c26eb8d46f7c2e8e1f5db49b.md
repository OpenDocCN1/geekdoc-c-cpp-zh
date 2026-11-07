
```cpp
...;
```

and

```cpp
for (n = lim; n > 0; n--)
    ...;
```

different from one another?

Logically, whether the prefix or postfix forms are used makes no difference in these two situations. The values of the expressions aren’t used, so the only effects are side effects. Here the expressions using the operators are full expressions, so the side effects of incrementing x and decrementing n are guaranteed to be performed by the time the program moves on to the next step; the prefix form and postfix form lead to the same final result.

However, although the choice between prefix and postfix forms has no effect on the program’s behavior, it is possible for the choice to have a small effect on execution speed. For built-in types and modern compilers, this seems to be a nonissue. But C++ lets you define these operators for classes. In that case, the user defines a prefix function that works by incrementing a value and then returning it. But the postfix version works by first stashing a copy of the value, incrementing the value, and then returning the stashed copy. Thus, for classes, the prefix version is a bit more efficient than the postfix version.

In short, for built-in types, it most likely makes no difference which form you use. For user-defined types having user-defined increment and decrement operators, the prefix form is more efficient.

## The Increment/Decrement Operators and Pointers

You can use increment operators with pointers as well as with basic variables. Recall that adding an increment operator to a pointer increases its value by the number of bytes in the type it points to. The same rule holds for incrementing and decrementing pointers:

```cpp
double arr[5] = {21.1, 32.8, 23.4, 45.2, 37.4};
double *pt = arr;  // pt points to arr[0], i.e. to 21.1
++pt;              // pt points to arr[1], i.e. to 32.8
```

You can also use these operators to change the quantity a pointer points to by using them in conjunction with the * operator. Applying both * and ++ to a pointer raises the questions of what gets dereferenced and what gets incremented. Those actions are determined by the placement and precedence of the operators. The prefix increment, prefix decrement, and dereferencing operators all have the same precedence and associate from right to left. The postfix increment and decrement operators both have the same precedence, which is higher than the prefix precedence. These two operators associate from left to right.

The right-to-left association rule for prefix operators implies that *++pt means first apply ++ to pt (because the ++ is to the right of the *) and then apply * to the new value of pt:

```cpp
double x = *++pt;  // increment pointer, take the value; i.e., arr[2], or 23.4
```

On the other hand, `++*pt` means obtain the value that `pt` points to and then increment that value:

```cpp
++*pt;      // increment the pointed to value; i.e., change 23.4 to 24.4
```

Here, `pt` remains pointing to `arr[2]`.

Next, consider this combination:

```cpp
(*pt)++;     // increment pointed-to value
```

The parentheses indicate that first the pointer is dereferenced, yielding `24.4`. Then the `++` operator increments that value to `25.4`; `pt` remains pointing at `arr[2]`.

Finally, consider this combination:

```cpp
x = *pt++;     // dereference original location, then increment pointer
```

The higher precedence of the postfix `++` operator means the `++` operator operates on `pt`, not on `*pt`, so the pointer is incremented. But the fact that the postfix operator is used means that the address that gets dereferenced is the original address, `&arr[2]`, not the new address. Thus, the value of `*pt++` is `arr[2]`, or `25.4`, but the value of `pt` after the statement completes is the address of `arr[3]`.

> **Note**
> 
> Incrementing and decrementing pointers follow pointer arithmetic rules. Thus, if `pt` points to the first member of an array, `++pt` changes `pt` so that it points to the second member.

## Combination Assignment Operators

Listing 5.5 uses the following expression to update a loop counter:

```cpp
i = i + by;
```

C++ has a combined addition and assignment operator that accomplishes the same result more concisely:

```cpp
i += by;
```

The `+=` operator adds the values of its two operands and assigns the result to the operand on the left. This implies that the left operand must be something to which you can assign a value, such as a variable, an array element, a structure member, or data you identify by dereferencing a pointer:

```cpp
int k = 5;
k += 3;                 // ok, k set to 8
int *pa = new int[10];   // pa points to pa[0]
pa[4] = 12;
pa[4] += 6;              // ok, pa[4] set to 18
*(pa + 4) += 7;          // ok, pa[4] set to 25
pa += 2;                 // ok, pa points to the former pa[2]
34 += 10;                 // quite wrong
```

Each arithmetic operator has a corresponding assignment operator, as summarized in Table 5.1. Each operator works analogously to `+=`. Thus, for example, the following statement replaces the current value of k with a value 10 times greater:

```cpp
k *= 10;
```

**Table 5.1. Combined Assignment Operators**

| Operator | Effect (L=left operand, R=right operand) |
|---|---|
| `+=` | Assigns L + R to L |
| `-=` | Assigns L - R to L |
| `*=` | Assigns L * R to L |
| `/=` | Assigns L / R to L |
| `%=` | Assigns L % R to L |

## Compound Statements, or Blocks

The format, or syntax, for writing a C++ `for` statement might seem restrictive to you because the body of the loop must be a single statement. That’s awkward if you want the loop body to contain several statements. Fortunately, C++ provides a syntax loophole through which you may stuff as many statements as you like into a loop body. The trick is to use paired braces to construct a compound statement, or block. The block consists of paired braces and the statements they enclose and, for the purposes of syntax, counts as a single statement. For example, the program in Listing 5.8 uses braces to combine three separate statements into a single block. This enables the body of the loop to prompt the user, read input, and do a calculation. The program calculates the running sum of the numbers you enter, and this provides a natural occasion for using the `+=` operator.

Listing 5.8  **block.cpp**

```cpp
// block.cpp -- use a block statement
#include <iostream>
int main()
{
    using namespace std;
    cout << "The Amazing Accounto will sum and average ";
    cout << "five numbers for you.\n";
    cout << "Please enter five values:\n";
    double number;
    double sum = 0.0;
    for (int i = 1; i <= 5; i++)
    {
        // block starts here
        cout << "Value " << i << " is: ";
        cin >> number;
        sum += number;
    }                                  // block ends here
    cout << "Five exquisite choices indeed! ";
    cout << "They sum to " << sum << endl;
    cout << "and average to " << sum / 5 << ".\n";
    cout << "The Amazing Accounto bids you adieu!\n";
    return 0;
}
```

Here is a sample run of the program in Listing 5.8:

```
The Amazing Accounto will sum and average five numbers for you.
Please enter five values:
Value 1: 1942
Value 2: 1948
Value 3: 1957
Value 4: 1974
Value 5: 1980
Five exquisite choices indeed! They sum to 9801
and average to 1960.2.
The Amazing Accounto bids you adieu!
```

Suppose you leave in the indentation but omit the braces:

```cpp
for (int i = 1; i <= 5; i++)
    cout << "Value " << i << ": ";       // loop ends here
    cin >> number;                       // after the loop
    sum += number;
cout << "Five exquisite choices indeed! ";
```

The compiler ignores indentation, so only the first statement would be in the loop. Thus, the loop would print the five prompts and do nothing more. After the loop completes, the program moves to the following lines, reading and summing just one number.

Compound statements have another interesting property. If you define a new variable inside a block, the variable persists only as long as the program is executing statements within the block. When execution leaves the block, the variable is deallocated. That means the variable is known only within the block:

```cpp
#include <iostream>
int main()
{
    using namespace std;
    int x = 20;
    {
        int y = 100;          // block starts
        cout << x << endl;    // ok
        cout << y << endl;    // ok
    }                         // block ends
    cout << x << endl;        // ok
    cout << y << endl;        // invalid, won't compile
    return 0;
}
```
