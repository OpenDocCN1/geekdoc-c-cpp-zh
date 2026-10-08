
Please note how we again and again avoid doing complicated work and instead find simpler solutions – often relying on library facilities. That’s the essence of programming: the continuing search for simplicity. Sometimes that’s – somewhat facetiously – expressed as “Good programmers are lazy.” In that sense (and only in that sense), we should be “lazy”; why write a lot of code if we can find a way of writing far less?

## 6.9 Program structure

Sometimes, the proverb says, it’s hard to see the forest for the trees. Similarly, it is easy to lose sight of a program when looking at all its functions, classes, etc. So, let’s have a look at the program with its details omitted:

```c++
#include "std_lib_facilities.h"

class Token { /* ... */};
class Token_stream { /* ... */};

void Token_stream::putback(Token t) { /* ... */}
Token Token_stream::get() { /* ... */}

Token_stream ts;      // provides get() and putback()
double expression();  // declaration so that primary() can call expression()

double primary() { /* ... */}     // deal with numbers and parentheses
double term() { /* ... */}        // deal with * and /
double expression() { /* ... */}  // deal with + and –

int main() { /* ... */}   // main loop and deal with errors
```

The order of the declarations is important. You cannot use a name before it has been declared, so **ts** must be declared before **ts.get()** uses it, and **error()** must be declared before the parser functions because they all use it. There is an interesting loop in the call graph: **expression()** calls **term()** which calls **primary()** which calls **expression()**.

We can represent that graphically (leaving out calls to `error()` – everyone calls `error()`):

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_248_0.png)

This means that we can’t just define those three functions: there is no order that allows us to define every function before it is used. We need at least one declaration that isn’t also a definition. We chose to declare (“forward declare”) `expression()`.

But does this work? It does, for some definition of “work” It compiles, runs, correctly evaluates expressions, and gives decent error messages. But does it work in a way that we like? The unsurprising answer is “Not really.” We tried the first version in §6.6 and removed a serious bug. This second version (§6.7) is not much better. But that’s fine (and expected). It is good enough for its main purpose, which is to be something that we can use to verify our basic ideas and get feedback from. As such, it is a success, but try it: it’ll (still) drive you nuts!

### TRY THIS

Get the calculator as presented above to run, see what it does, and try to figure out why it works as it does.

### Drill

This drill involves a series of modifications of a buggy program to turn it from something useless into something reasonably useful.

- 1. Take the calculator from the file **calculator02buggy.cpp**. Get it to compile. You need to find and fix a few bugs. Those bugs are not in the text in the book. Find the three logic errors deviously inserted in **calculator02buggy.cpp** and remove them so that the calculator produces correct results.
- 2. Change the character used as the exit command from **q** to **x**.
- 3. Change the character used as the print command from **;** to **=**.
- 4. Add a greeting line in **main**():
  > "Welcome to our simple calculator.
  > Please enter expressions using floating-point numbers."
- 5. Improve that greeting by mentioning which operators are available and how to print and exit.

### Review

- 1. What do we mean by “Programming is understanding”?
- 2. The chapter details the creation of a calculator program. Write a short analysis of what the calculator should be able to do.
- 3. How do you break a problem up into smaller manageable parts?
- 4. Why is creating a small, limited version of a program a good idea?
- 5. Why is feature creep a bad idea?
- 6. What are the three main phases of software development?
- 7. What is a “use case”?
- 8. What is the purpose of testing?
- 9. According to the outline in the chapter, describe the difference between a **Term**, an **Expression**, a **Number**, and a **Primary**.
- 10. In the chapter, an input was broken down into its component **Terms**, **Expressions**, **Primary**, and **Numbers**. Do this for **(17+4)/(5-1)**.
- 11. Why does the program not have a function called **number**()?
- 12. What is a token?
- 13. What is a grammar? A grammar rule?
- 14. What is a class? What do we use classes for?
- 15. How can we provide a default value for a member of a class?
- 16. In the expression function, why is the default for the **switch**-statement to “put back” the token?
- 17. What is “look-ahead”?
- 18. What does `putback()` do and why is it useful?
- 19. Why is the remainder (modulus) operation, `%`, difficult to implement in the `term()`?
- 20. What do we use the two data members of the `Token` class for?
- 21. Why do we (sometimes) split a class’s members into `private` and `public` members?
- 22. What happens in the `Token_stream` class when there is a token in the buffer and the `get()` function is called?
- 23. Why were the `';'` and `'q'` characters added to the `switch`-statement in the `get()` function of the `Token_stream` class?
- 24. When should we start testing our program?
- 25. What is a “user-defined type”? Why would we want one?
- 26. What is the interface to a C++ “user-defined type”?
- 27. Why do we want to rely on libraries of code?

### Terms

- analysis
- class
- class member
- data member
- design
- divide by zero
- grammar
- implementation
- interface
- member function
- parser
- private
- prototype
- pseudo code
- public
- syntax analyzer
- token
- use case

### Exercises

- 1. If you haven’t already, do the **Try this** exercises from this chapter.
- 2. Add the ability to use `{}[]` as well as `()` in the program, so that `"{(3+4)*6}"` (`(3+4)`) will be a valid expression.
- 3. Add a factorial operator: use a suffix `!` operator to represent “factorial.” For example, the expression `7!` means `7 * 6 * 5 * 4 * 3 * 2 * 1`. Make `!` bind tighter than `*` and `/`; that is, `7*8!` means `7*(8!)` rather than `(7*8)!`. Begin by modifying the grammar to account for a higher-level operator. To agree with the standard mathematical definition of factorial, let `0!` evaluate to `1`. Hint: The calculator functions deal with `doubles`, but factorial is defined only for `ints`, so just for `x!`, assign the `x` to an `int` and calculate the factorial of that `int`.
- 4. Define a class `Name_value` that holds a string and a value. Rework exercise 19 in Chapter 4 to use a `vector<Name_value>` instead of two `vectors`.
- 5. Add the article `the` to the “English” grammar in §6.4.1, so that it can describe sentences such as “The birds fly but the fish swim.”
- 6. Write a program that checks if a sentence is correct according to the “English” grammar in §6.4.1. Assume that every sentence is terminated by a full stop (.) surrounded by whitespace. For example, `birds fly but the fish swim .` is a sentence, but `birds fly but the fish swim` (terminating dot missing) and `birds fly but the fish swim.` (no space before dot) are not. For each sentence entered, the program should simply respond “OK” or “not OK.” Hint: Don’t bother with tokens; just read into a string using `>>`.
- 7. Write a grammar for bitwise logical expressions. A bitwise logical expression is much like an arithmetic expression except that the operators are `!` (not), `~` (complement), `&` (and), `|` (or), and `^` (exclusive or). Each operator does its operation to each bit of its integer operands (see §25.5). `!` and `~` are prefix unary operators. A `^` binds tighter than `|` (just as `*` binds tighter than `+`) so that `x|y^z` means `x|(y^z)` rather than `(x|y)^z`. The `&` operator binds tighter than `^` so that `x^y&z` means `x^(y&z)`.
- 8. Redo the “Bulls and Cows” game from exercise 12 in Chapter 5 to use four letters rather than four digits.
- 9. Write a program that reads digits and composes them into integers. For example, `123` is read as the characters `1`, `2`, and `3`. The program should output `123 is 1 hundred and 2 tens and 3 ones`. The number should be output as an `int` value. Handle numbers with one, two, three, or four digits. Hint: To get the integer value `5` from the character `'5'` subtract `'0'`, that is, `'5'-'0'==5`.
- 10. A permutation is an ordered subset of a set. For example, say you wanted to pick a combination to a vault. There are 60 possible numbers, and you need three different numbers for the combination. There are `P(60,3)` permutations for the combination, where `P` is defined by the formula:

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_251_0.png)

where `!` is used as a suffix factorial operator. For example, `4!` = `4*3*2*1`. Combinations are similar to permutations, except that the order of the objects doesn’t matter. For example, if you were making a “banana split” sundae and wished to use three different flavors of ice cream out of five that you had, you wouldn’t care if you used a scoop of vanilla at the beginning or the end; you would still have used vanilla. The formula for combinations is

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_251_1.png)
