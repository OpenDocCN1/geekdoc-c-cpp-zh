
It is also important that variables are only known within the block in which you declare them. Once the program passes the closing brace of the block, they are no longer available. Therefore, this declaration does not overlap with the previous one:

```cpp
int upTo = inputUpTo(argc, argv);
```

This declares a “different” upTo, which is only visible in main().

You can also see here that initialization can occur not only with 0 or a constant. Here, a complex function call returns the value with which upTo is initialized.

You can also combine declarations separated by commas. You can declare multiple variables like this:

```cpp
int from, to, result;
```

Here, all variables will be of type int. If you wanted to initialize all (or some) at the same time, you can do so:

```cpp
int from, to = 0, result;
```

Here you declare three variables, but only to is initialized with 0.

## 8.3.1 Structured Binding

Since C++17, it is also possible to declare multiple elements at once and initialize them all with a single equals sign =.

To do this, use auto before square brackets [], which then contain the variables to be declared.

Three variants are possible: binding a C-array, binding a tuple, and binding a structure.

```cpp
// https://godbolt.org/z/Xbgeeg3n
#include <iostream>
#include <tuple> // make_tuple
auto mkTpl() {
    return std::make_tuple(2, 'b', 3.14); // tuple<int,char,double>
}
struct Point {
    int x, y;
};
int main() {
    // Structured binding of a C-array
    int odd[5] = {1,3,7,9,11};
    auto [one, two, three, four, five] = odd;
    // Structured binding of a tuple
    auto [zwei, be, pi] = mkTpl();
    // Structured binding of a struct
    Point p0{10, 15};
    auto [the_x, the_y] = p0;
}
```

**Listing 8.8** With auto, you can also initialize multiple variables at.

Here, the count must match exactly. So, if odd one day contains six elements, binding will fail. The same applies to a tuple that is too large or small, or to an unsuitable structure.

You don't need to copy out the values; you can also let the declaration be references:

```cpp
// https://godbolt.org/z/3zo8GbnW3
int main() {
    int odd[5] = {1,3,7,9,11};
    auto [one, two, three, four, five] = odd;
    auto [zwei, be, pi] = mkTpl(); // no & binding to temp-values

    Point p0{ 10, 15 };
    auto &[ the_x, the_y ] = p0;
}
```

Here, for example, three is a reference to the 7 within odd.

This, of course, only works if there is an object that can be referenced. In the case of mkTpl(), this is not the case, as the function returns a temp-value that is not yet stored anywhere.

## 8.4 The Expression Statement

You can also use any expression as a statement. Although it makes little sense to use 3+4; as a statement, for example, assignments are expressions and are used as statements very often.

Assuming you have previously declared int upTo, the following listing gives examples of expressions used as statements.

```cpp
upTo = 99; // an assignment is an expression
upTo = upTo * 2 + 1; // combining an assignment with a calculation
calculatePrimesUpTo(upTo); // a function call is an expression
std::cout << "Friedrich III"; // the output operator
```

**Listing 8.9** These are all expressions used as statements.

As I mentioned earlier, every expression has a value and a type. If an expression is used as a statement, the type is discarded by the compiler.

> The if, while, do, for, and switch statements are control structures and allow you to program branches and loops. With break and continue, you influence the flow of control structures. return also belongs to this flow in the broadest sense. I would prefer not to mention goto (to find out why, see Section 8.14).

## 8.5 The “if” Statement

With the if statement, you program the conditional execution of statements. The simplest form executes the statement assigned to it only if a specified condition is met:

```cpp
if( Condition ) Statement
```

You already know a bit about the statement part: here you should use a block with {...} so you can group multiple statements and link them to the if. This is called the then branch of the if statement.

The condition, however, is still somewhat ominous. This must be an expression that evaluates to a truth value—that is, true or false. This applies to a specific group of expressions—namely, those that have the type bool.

More correctly, it must be possible to convert the expression to bool. This is a subtle but important difference that I explained in Chapter 4, Section 4.4. This simply means that you can also use a number like 0.

Here are a few conditions that can be true or false:

- greater than 0
- less than 0
- equal to 0
- not equal to 0
- greater than or equal to 0
- less than or equal to 0
- and 0
- or 0
- not 0

With the if statement, you can also write:

```cpp
if( x > 1 ) {
    std::cout << "x is greater than 1";
} else {
    std::cout << "x is not greater than 1";
}
```

There is another useful form of the if statement, which you can see:

```cpp
if( Condition ) Statement1 else Statement2
```

This implements: “Execute Statement1 or Statement2.” Statement2 is called the else branch of the if statement.

img/290cf954ad53865de6b988e6f_349_0.png
**Figure 8.2** Flowchart of the "if" statement with and without "else".

Why only? Because you don't have to execute x > 1 twice. We have already used blocks {...} instead of a single statement. You could also have written the following:

```cpp
if(x > 1)
    std::cout << "x is greater than 1";
else
    std::cout << "x is not greater than 1";
```

is almost the same But because else branches make the code more complex, blocks are really recommended here.

Now you actually know everything about if that you can. What remains is to combine the knowledge: An if is a statement, if the condition, then the branch, and optional else all together is a statement. You both then and else each get a statement associated. You can combine this into complex nesting. It is common to use another if in the else branch to sequentially query different possibilities:

```cpp
if(number < 0) {
    std::cout << "The number is negative";
} else if (number == 0) { // else and follow directly one after another
    std::cout << "The number is zero";
} else if (number > 1000) { // also possible multiple times
    std::cout << "The number is large";
} else { /* x > 0 but x <= 1000 */
    std::cout << "The number is positive";
}
```

It is common to save yourself from wrapping every if statement in a block with one statement. However, if you once make it clear to yourself where you would place all block braces, then you learn something about statements. Completely with all {...} around each single statement, the example would look like this:

```cpp
if(number < 0) {
    std::cout << "The number is negative";
} else {
    if(number == 0) {
        std::cout << "The number is zero";
    } else {
        if(number > 1000) {
}
```
