
## Introducing for Loops

What's a full expression? It's an expression that's not a subexpression of a larger expression. Examples of full expressions include an expression portion of an expression statement and an expression that serves as a test condition for a while loop.

Sequence points help clarify when postfix incrementation takes place. Consider, for instance, the code:

```
while (guests++ < 10)
cout << guests << endl;
```

(The while loop, discussed later in this chapter, works like a for loop that has just a test expression.) Sometimes C++ newcomers use “use the value, then increment it” means in this context, to increment guests after it's in the cout statement. However, the guests++ < 10 is a full expression because it is a while loop condition, so the end of this expression is a sequence point. Therefore, C++ guarantees the side effect (incrementing guests) takes place before the program moves on to cout. Using the postfix form, however, guarantees that guests will be incremented after the comparison,

Now consider this statement:

```
y = (4 + x++) + (6 + x++);
```

The expression 4 + x++ is not a full expression, so C++ does not guarantee that x will be incremented immediately after the subexpression 4 + x++ is evaluated. Here the full expression is the entire assignment statement, and the semicolon marks the sequence point, so that C++ guarantees that x will have been incremented twice by the time the program moves to the following statement. C++ does not specify whether x is increment after each subexpression is evaluated or only after all expressions have been evaluated, which is why you should avoid statements of this kind.

C++11 documentation has dropped the term “sequence point” because the concept doesn't carry over when discussing multiple threads of execution. Instead, descriptions are framed in terms of sequencing, with some events being described as sequenced before other events. This descriptive approach isn't intended to change the rules; the goal is to provide language that can clearly handle multithreaded programming.

### Prefix Versus Postfix

Clearly, whether you use the prefix or postfix form makes a difference if it is used for some purpose, such as a function argument or assigning to a variable. But what if the value of an increment or decrement expression isn't used? For example, are

```
x++;
```

and
```
++x;
```

different from one another? Or are

```
for (n = lim; n > 0; --n)
```

and

```
for (n = lim; n > 0; n--)
```

different from one another?

Logically, the prefix or postfix forms are used made no difference in these two situations. The values of the expressions are not used, so the only effects are the side effects. Here the expressions using the operators are postfix, so the effects of incrementing x and decrementing n are guaranteed to be performed by the time the program moves to the next step; the prefix form and postfix form has no effect on the program's behavior, it is possible for the choice to have a small effect on execution speed. For built-in types and modern compilers, this seems to be a non issue. C++ lets you define these operators for classes. In that case, the user defines a prefix function that works by incrementing a value, and returning it. The postfix version works by first copying the value, incrementing the value, and then returning the copied value. Thus, for classes, the prefix version is a bit more efficient than the postfix version.

In short, for built-in types, it likely makes no difference which you use. For user-defined types using user-defined increment and decrement operators, the prefix form is more efficient.

### The Increment/Decrement Operators and Pointers

You can use increment operators with pointers as well as basic variables. Recall that adding an increment operator to a pointer increases its value by the number of bytes in the type it points to. The same rule holds for incrementing and decrementing pointers:

```
double arr[5] = {21.1, 32.8, 23.4, 45.2, 37.4};
double *pt = arr; // pt points to arr[0], i.e. to 21.1
++pt; // pt points to arr[1], i.e. to 32.8
```

You can also use these operators to change the quantity a pointer points to using in conjunction with the * operator. Applying * and ++ to a pointer raises the questions of what gets dereferenced and what gets incremented. Those actions are determined by priority and precedence of the operators. The prefix increment, decrement, and dereferencing operators all have the same precedence from left to right. The postfix increment and decrement operators both have the same precedence, which is higher than the prefix precedence. These two operators operate from left to right.

The right-to-left association rule for prefix operators implies that ++pt means first apply ++ to pt (because the ++ is to the right of the *) and then * to the new value of pt:

```
double x = ++pt; // increment pointer, take the value; i.e., arr[2], or 23
```

On the other hand, ++pt means the value that pt points to and then increment that value:

```
++pt; // increment the pointed to value; i.e., change 23.4 to 24.4
```

Here, pt remains pointing to arr[2]. Next, consider this combination:

```
(*pt)++; // increment pointed-to value
```

The parentheses indicate that the first pointer is dereferenced, yielding 24.4. Then the ++ operator increments that to 25.4; pt remains pointing at arr[2]. Finally, consider this combination:

```
x = *pt++; // dereference original location, increment pointer
```

The precedence of the suffix ++ operator means the ++ operator operates on pt, not on *pt, so the pointer is incremented. But the fact that the postfix operator is used means the address that dereferenced is the original address, &arr[2], not the new address. Thus, the value of *pt++ is arr[2], or 25.4, but the value of pt after the statement completes the address of arr[3]

> Note Incrementing and decrementing pointers follow pointer arithmetic rules. Thus, if pt points to the first member of an array, ++pt changes so that it points to the second member.

### Combination Assignment Operators

Listing 5.5 uses the following expression to update a loop counter:

```
i = i + by
```

C++ has a combined addition and assignment operator that accomplishes the same result more concisely:

```
i += by
```

The ++ operator adds the values of its two operands and assigns the result to the operand on the left. This implies that the left operand must be something to you can assign a value, such as a variable, an array element, a structure member, or data you identify by dereferencing a pointer:

```
int k = 5;
k += 3; // ok, k set to 8
int *pa = new int[10]; // pa points to pa[0]
p[4] = 12;
pa[4] += 6; // ok, pa[4] set to 18
*(pa + 4) += 7; // ok, pa[4] set to 25
pa += 2; // ok, pa points to the former pa[2]
34 += 10; // quite wrong
```

Each arithmetic operator has a corresponding assignment operator, as summarized in Table 5.1. Each operator works analogously to +=. Thus, for example, the following statement replaces the current value of k with a value 10 times greater:

k *= 10;

## Chapter 5 Loops and Relational Expressions

### 5.1 Combined Assignment Operators

| Operator | Effect (L=left operand, R=right operand) |
| --- | --- |
| += | Assigns L + R to L |
| -= | Assigns L - R to L |
| *= | Assigns L * R to L |
| /= | Assigns L / R to L |
| %= | Assigns L % R to L |

### Compound Statements, or Blocks

The format, or syntax, for writing a C++ for statement might seem restrictive to you because the body of the loop must be a single statement. That seem awkward if you want the loop body to contain several statements. C++ provides a syntax loophole through which you may stuff as many statements as you like into a loop body. The trick is to use paired braces to construct a compound statement, or block. The block consists of paired braces and the statements they enclose, and for the purposes of syntax, counts as a single statement. For example, the program in Listing 5.8 uses braces to combine three statements into a single block. This enables the body of the loop to prompt the user, read input, and do a calculation. The program calculates the running sum of the numbers you enter, and provides a natural occasion for using the += operator.

### Listing 5.8 block.cpp

```
// use a block statement
#include <iostream>
int main() {
{
	using namespace std;

	cout << "The Amazing Account will sum and average ";
	cout << "five numbers for you.\n";
	cout << "Please enter five values:\n";
	double number;
	double sum = 0.0;
	for (int i = 1; i <= 5; i++) {
	{
			cout << "Value " << i << " : ";
		cin >> number;
		sum += number;
	}		// block starts here
}
}
// block ends here
