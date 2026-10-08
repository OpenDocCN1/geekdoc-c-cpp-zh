
language specification will it allow you to proceed. Many of the errors that the compiler finds are simply “silly errors” caused by mistyping or incomplete edits of the source code. Others result from flaws in our understanding of the way parts of our program interact. To a beginner, the compiler often seems petty, but as you learn to use the language facilities — and especially the type system — to directly express your ideas, you’ll come to appreciate the compiler’s ability to detect problems that would otherwise have caused you hours of tedious searching for bugs.

As an example, we will look at some calls of this simple function:

```cpp
int area(int length, int width);    // calculate area of a rectangle
```

### 5.3.1 Syntax errors

What if we were to call **area()** like this:

```cpp
int s1 = area(7);       // error: ) missing
int s2 = area(7)        // error ; missing
Int s3 = area(7);       // error: Int is not a type
int s4 = area(7);       // error: non-terminated character ( ‘ missing)
```

Each of those lines has a syntax error; that is, they are not well formed according to the C++ grammar, so the compiler will reject them. Unfortunately, syntax errors are not always easy to report in a way that you, the programmer, find easy to understand. That’s because the compiler may have to read a bit further than the error to be sure that there really is an error. The effect of this is that even though syntax errors tend to be completely trivial (you’ll often find it hard to believe you have made such a mistake once you find it), the reporting is often cryptic and occasionally refers to a line further on in the program. So, for syntax errors, if you don’t see anything wrong with the line the compiler points to, also look at previous lines in the program.

Note that the compiler has no idea what you are trying to do, so it cannot report errors in terms of your intent, only in terms of what you did. For example, given the error in the declaration of **s3** above, a compiler is unlikely to say

> “You misspelled **int**; don’t capitalize the **i**.”

Rather, it’ll say something like

- “syntax error: missing ‘;’ before identifier ‘**s3**””
- “‘**s3**’ missing storage-class or type identifiers”
- “‘**Int**’ missing storage-class or type identifiers”

Such messages tend to be cryptic, until you get used to them, and to use a vocabulary that can be hard to penetrate. Different compilers can give very different-looking error messages for the same code. Fortunately, you soon get used to reading such stuff. After all, a quick look at those cryptic lines can be read as

> “There was a syntax error before **s3**, and it had something to do with the type of **Int** or **s3**.”

Given that, it's not rocket science to find the problem.

**TRY THIS**

Try to compile those examples and see how the compiler responds.

### 5.3.2 Type errors

Once you have removed syntax errors, the compiler will start reporting type errors; that is, it will report mismatches between the types you declared (or forgot to declare) for your variables, functions, etc. and the types of values or expressions you assign to them, pass as function arguments, etc. For example:

```cpp
int x0 = arena(7);            // error: undeclared function
int x1 = area(7);             // error: wrong number of arguments
int x2 = area("seven",2);     // error: 1st argument has a wrong type
```

Let's consider these errors.

1. For **arena(7)**, we misspelled **area** as **arena**, so the compiler thinks we want to call a function called **arena**. (What else could it “think”? That’s what we said.) Assuming there is no function called **arena()**, you’ll get an error message complaining about an undeclared function. If there is a function called **arena**, and if that function accepts 7 as an argument, you have a worse problem: the program will compile but do something you didn’t expect it to (that’s a logical error; see §5.7).
2. For **area(7)**, the compiler detects the wrong number of arguments. In C++, every function call must provide the expected number of arguments, of the right types, and in the right order. When the type system is used appropriately, this can be a powerful tool for avoiding run-time errors (see §14.1).
3. For **area**(“**seven**”,2), you might hope that the compiler would look at “**seven**” and figure out that you meant the integer **7**. It won’t. If a function needs an integer, you can’t give it a string. C++ does support some implicit type conversions (see §3.9) but not *string* to *int*. The compiler does not try to guess what you meant. What would you have expected for **area**(“Hovel lane”,2), **area**(“7,2”), and **area**(“sieben”,”zwei”)?

These are just a few examples. There are many more errors that the compiler will find for you.

**TRY THIS**

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_171_0.png)

Try to compile those examples and see how the compiler responds. Try thinking of a few more errors yourself, and try those.

### 5.3.3 Non-errors

As you work with the compiler, you'll wish that it was smart enough to figure out what you meant; that is, you'd like some of the errors it reports not to be errors. That's natural. More surprisingly, as you gain experience, you'll begin to wish that the compiler would reject more code, rather than less. Consider:

```cpp
int x4 = area(10, -7);         // OK: but what is a rectangle with a width of minus 7?
int x5 = area(10.7, 9.3);      // OK: but calls area(10, 9)
char x6 = area(100, 9999);    // OK: but truncates the result
```

For **x4** we get no error message from the compiler. From the compiler's point of view, area(10, -7) is fine: area() asks for two integers and you gave them to it; nobody said that those arguments had to be positive.

For **x5**, a good compiler will warn about the truncation of the doubles 10.7 and 9.3 into the ints 10 and 9 (see §9.2). However, the (ancient) language rules state that you can implicitly convert a double to an int, so the compiler is not allowed to reject the call area(10.7, 9.3).

The initialization of **x6** suffers from a variant of the same problem as the call area(10.7, 9.3). The int returned by area(100, 9999), probably 999900, will be assigned to a char. The most likely result is for **x6** to get the "truncated" value -36. Again, a good compiler will give you a warning even though the (ancient) language rules prevent it from rejecting the code.

As you gain experience, you'll learn how to get the most out of the compiler's ability to detect errors and to dodge its known weaknesses. However, don't get overconfident: "my program compiled" doesn't mean that it will run. Even if it does run, it typically gives wrong results at first until you find the flaws in your logic.

## 5.4 Link-time errors

A program consists of several separately compiled parts, called *translation units*. Every function in a program must be declared with exactly the same type in every translation unit in which it is used. We use header files to ensure that; see §8.3. Every function must also be defined exactly once in a program. If either of these rules is violated, the linker will give an error. We discuss how to avoid link-time errors in §8.3. For now, here is an example of a program that might give a typical linker error:

```cpp
int area(int length, int width);   // calculate area of a rectangle

int main()
{
    int x = area(2,3);
}
```

Unless we somehow have defined area() in another source file and linked the code generated from that source file to this code, the linker will complain that it didn't find a definition of area().

The definition of area() must have exactly the same types (both the return type and the argument types) as we used in our file, that is:

```cpp
int area(int x, int y) {/* ... */}   // "our" area()
```

Functions with the same name but different types will not match and will be ignored:

```cpp
double area(double x, double y) {/* ... */}   // not "our" area()
int area(int x, int y, char unit) {/* ... */}   // not "our" area()
```

Note that a misspelled function name doesn't usually give a linker error. Instead, the compiler gives an error immediately when it sees a call to an undeclared function. That's good: compile-time errors are found earlier than link-time errors and are typically easier to fix.

The linkage rules for functions, as stated above, also hold for all other entities of a program, such as variables and types: there has to be exactly one definition of an entity with a given name, but there can be many declarations, and all have to agree exactly on its type. For more details, see §8.2–3.

## 5.5 Run-time errors

If your program has no compile-time errors and no link-time errors, it'll run. This is where the fun really starts. When you write the program you are able to detect
