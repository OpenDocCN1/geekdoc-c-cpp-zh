
# Chapter 3

# Variables and Statements

> "It takes all kinds to make a world, does it not, Padre?"
> "So it does, my son, so it does."
—Pirate Captain Thomas Bartholomew Red to the Padre, Pirates

There sure can be lots of stuff in a C program.

Yup.

And for various reasons, it'll be easier for all of us if we classify some of the types of things you can find in a program, so we can be clear what we're talking about.

## 3.1 Variables

It's said “variables hold values”. But another way to think about it is that a variable is a human-readable name that refers to some data in memory.

We're going to take a second here and take a peek down the rabbit hole that is pointers. Don't worry about it.

You can think of memory as a big array of bytes’. Data is stored in this “array”¹². If a number is larger than a single byte, it is stored in multiple bytes. Because memory is like an array, each byte of memory can be referred to by its index. This index into memory is also called an *address*, or a *location*, or a *pointer*.

When you have a variable in C, the value of that variable is somewhere, at some address. After, where else would it be? But it's a pain to refer to a value by its numeric address, so we make a name for it, and that's what the variable is.

The reason I'm bringing this up is twofold:

- 1. It's going to make it easier to understand pointer variables—they're variables that hold the address of other variables!
- 2. Also, it's going to make it easier to understand pointers later.

So a variable is a name for some data that's stored in memory at some address.

¹‘byte’ is typically an 8-bit binary number. Think of it as an integer that can hold the values from 0 to 255, inclusive. Technically, C allows bytes to be any number of bits and if you want to unambiguously refer to an 8-bit number, you should use the term octet. But programmers assume you have 8 bits unless you specify otherwise.

²in seriously oversimplifying how modern memory works, here. But the mental model works, so please forgive me.

# Chapter 3. Variables and Statements

### 3.1.1 Variable Names

You can use characters in the range 0-9, A-Z, a-z, and underscore for variable names, with the following rules:

- You can't start a variable with a digit 0-9.
- You can't start a variable name with two underscores.
- You can't start a variable name with an underscore followed by a capital A-Z.

For Unicode, there are some rules in the spec §.2 that talk about which Unicode codepoint ranges are allowed in which parts of identifiers, that's too much to write about here and something you'll never have to think about anyway.

### 3.1.2 Variable Types

Depending on which languages you already have in your toolkit, you might or might not be familiar with the idea of types. But C's kinda picky about them, so we should do a refresher.

Some example, of the most basic:

| Type | Example | C Type |
|---|---|---|
| Integer | 3490 | int |
| Floating point | 3.14159 | float³ |
| Character (single) | 'c' | char |
| String | "Hello, world!" | char⁴ |

C makes an effort to convert most numeric types when you ask it to. But other than, all conversations are manual, not between string and numeric.

All of the types in C are variants on these types.

Before you use a variable, you have to declare a variable and tell C what the variable holds. Once declared, the variable cannot be changed later at runtime. What you set it to is what it is until it falls out of scope and reabsorbed into the universe.

Let's take our previous "Hello, world" and add couple variables to it:

```c
#include <stdio.h>

int main(void) {
    int i;      // Holds signed integers, e.g. -3, 0, 1, 10
    float f;    // Holds signed floating point numbers, e.g. -3.14159

    printf("Hello, World!\n"); // Ah, blessed familiarity

}
```

We've declared a couple of variables. We've used them, and they're both initialized. One holds an integer, and the other holding a floating point (a real number, basically, if you have a background).

Uninitialized variables have indeterminate value³. They have to be initialized or else you must assume they contain some number.

³I'm lying here little. 3.14159 is of type double, but there are not yet and I you associate float with "Floating Point", and C will coerce that type into a float. Don't worry about it until later.

⁴Read this as "pointer to a char" or "char pointer". "Char" for character. I can't find a string, so it accent make people as "char," a minority say "char", and handful say "quare". We'll tell more about pointers later.

⁵Colloquially, we say they "random" values, but they aren't truly—or even pseudo-truly—random numbers.

# Chapter 3. Variables and Statements

This is one of the places C can "get you". Much of the time, in my experience, the indeterminate value is zero... but it can vary from run to run! Never assume the value will be zero, if you see it. Always explicitly initialize variables to some value before you use them⁶.

What's this? You want to store some numbers in those variables? Insanity!

Let's go and do that:

```c
int main(void)
{
    int i;

    i = 2; // Assign the value 2 into the variable i

    printf("Hello, World!\n");
}
```

Killer. We've stored a value. Let's print it.
We're going to do that by passing two arguments to the printf() function. The first argument is a string that describes how and where to print it (called the *format string*), and the second is the value to print, whatever is in the variable i.
printf() hunts through the format string for a variety of special sequences which start with a percent sign (%) tell it what to print. For example, if it finds a %d, it looks to the next parameter that was passed, and prints it out as an integer. If it finds a %f, it prints the value as a float. If it finds a %s, it prints a string.
As, we can print out the value of types like:

And the output will be:
Hello, world! i = 2 and f = 3.14!
In this way, printf() might be similar to various types of format strings or parameterized strings in other languages you are familiar with.

### 3.1.3 Boolean Types

C has Boolean types, true or false?
1!

Historically, C didn't have a Boolean type, and some might argue it thus doesn't.
In C, 0 means "false", and non-zero means "true".
So one is true. And -37 is true. And 0 is false.

You can declare Boolean types as ints:

> ⁶This isn't strictly 100% true. When we get to learning about static storage duration, you'll find some variables are initialized to zero automatically. The best thing to do is always initialize them.

# Chapter 3. Variables and Statements

int x = 1;

```c
if (x) {
    printf("x is true!\n");
}
```

If you include <stdbool.h>, you also get access to some symbolic names that might make things more familiar, namely a bool type and true and false:

```c
#include <stdio.h>
#include <stdbool.h>
```

```c
int main(void) {
    bool x = true;

    if (x) {
        printf("x is true!\n");
    }
}
```

But these are identical to using integer values for true and false. They're just a facade to make things nice.

## 3.2 Operators and Expressions

C operators should be familiar to you from other languages. Let's blast through some of them here.
(There are a bunch more details about this, but we're going to do enough in this section to started).

### 3.2.1 Arithmetic

Hopefully these are familiar:

```c
i = i + 3; // Addition (+) and assignment (=) operators, add 3 to i
i = i - 8; // Subtraction, subtract 8 from i
i = i * 9; // Multiplication
i = i / 2; // Division
i = i % 5; // Modulo (division remainder)
```

There are shorthand variants for all of the above. Each of these lines could more ternary be written as:

```c
i += 3; // Same as "i = i + 3", add 3 to i
i -= 8; // Same as "i = i - 8"
i *= 9; // Same as "i = i * 9"
i /= 2; // Same as "i = i / 2"
i %= 5; // Same as "i = i % 5"
```

There is no exponentiation. You'll have to use one of the pow() function variants from math.h.
Let's get into some of the weir stuff you might not have in your other languages!

### 3.2.2 Ternary Operator

C also includes the ternary operator. This is an expression whose value depends on the result of a conditional embedded in it.

```c
// If x > 10, add 17 to y. Otherwise add 37 to y.
```
