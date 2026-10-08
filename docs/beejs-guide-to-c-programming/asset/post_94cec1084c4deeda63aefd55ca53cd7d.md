
## Chapter 25. Variadic Functions

What do you do put all the arguments that must be passed first (remember there has to be at least one) and after that, you put . . . Just like this:

```c
void func(int a, ...)    // Literally 3 dots here
```

Here's some code to demo that:

```c
#include <stdio.h>
```

```c
void func(int a, ...)
{
    printf("a is %d\n", a);    // Prints "a is 2"
}
```

```c
int main(void)
{
    func(2, 3, 4, 5, 6);
}
```

So, great, we can get that first in variable a, but what about the rest of the arguments? How do you get them?

Here's where the fun begins!

## 25.2 Getting the Extra Arguments

You're going to include <stdarg.h> to make any of this work.

First things first, we're going to use a special variable of type va_list (variable argument list) to keep track of which variable we are accessing at a time.

The idea is that we start processing arguments with a call to va_start(), process each argument in turn with va_arg(), and then, when done, wrap it up with va_end().

When you call va_start(), you need to pass in the last named parameter (the one just before the ...) so it knows where to looking for the additional arguments.

And when you call va_arg() to get the next argument, you need to tell it the type of argument to get next.

Here's a demo that adds an arbitrary number of integers. The first argument is the number of integers to add. We'll make use of this to figure out how many times we have to call va_arg().

```c
#include <stdio.h>
#include <stdarg.h>
```

```c
int add(int count, ...)
{
    int total = 0;
    va_list va;
```

```c
va_start(va, count);    // Start with arguments after "count"
for (int i = 0; i < count; i++) {
    int n = va_arg(va, int);    // Get the next int
    total += n;
}
```

```c
va_end(va);    // All done
```

```c
return total;
}

int main(void)
{
    printf("%d\n", add(4, 6, 2, -4, 17)); // 6 + 2 - 4 + 17 = 21
    printf("%d\n", add(2, 22, 44)); // 22 + 44 = 66
}
```

Note that printf() is a placeholder, it uses the number of %ds (or whatever) in the format string to know how many arguments there are there.

If the syntax of va_arg() is looking strange to you (because of that loose type floating around in there), you're not alone. These are implemented with preprocessor macros in order to get all the proper magic in

## 25.3 va_list Functionality

What is va_list variable we're using there? It's an opaque variable that holds information about which argument we're going to get next with va_arg(). You see how we call va_arg() over and over? The va_list variable is a placeholder's keeping track of progress so far.

But we have to initialize va_list to some sensible state. That's where va_start() comes into play.

And that's why we have to initialize the initial parameter, you can easily fetch subsequent arguments by calling va_arg() repeatedly. When you do, you have to pass in your va_list (so it can keeping track of where you are), as well as the type of argument you're about to copy off.

It's up to you a programmer to figure out which type you're going to pass to va_arg(). In the above example, we just did. In case of printf(), it uses the format string to determine which type you pull off.

And when you call va_end() to wrap it up. You must (the spec says) call on this particular va_list variable before either call va_start() or va_copy() again. I know we haven't talked about va_copy() yet.

So the standard progression is:

- va_start() to initialize your va_list variable
- va_arg() to get the values
- va_end() to deinitialize your va_list variable

I mentioned va_copy() because it makes a copy of your va_list variable in the exact same state. If you've started with va_arg() with the source variable, the new one won't be started, either. If you've consumed 5 arguments with va_arg() so far, the va_copy will also reflect that.

va_copy() can be useful if you need to see ahead through the arguments but need to remember your current place.

> ¹That is, novices developers aren't supposed to know what is in it or what it means. The spec doesn't dictate what it is in.
> ²Honestly, it would be possible to remove that limitation from the language, but the idea is that macros va_start(), va_arg(), and va_end() should be able to be written in C. And to make that, we need some way to initialize a pointer to the location of first parameter. It would require a language extension to make this possible, and so far the committee hasn't found a rationale for so.

## 25.4 Library Functions That Use va_lists

One of the other uses for these is pretty cool: writing your own printf(). It would be a pain to handle all those specifiers right? All zillion of them? Luckily, there are printf() variants that accept a va_list as argument. You can use these to wrap and make your own custom! These functions start with the letter v, such as vprintf(), vfprintf(), and vsnprintf(). Let's make my_printf() that works like printf() it takes an extra argument front.

```c
#include <stdio.h>
#include <stdarg.h>

int my_printf(int serial, const char *format, ...)
{
    va_list va;
    // Do custom work
    printf("The number is: %d\n", serial);

    // Then pass the rest to vprintf()
    va_start(va, format);
    int rv = vprintf(format, va);
    va_end(va);
    return rv;
}

int main(void)
{
    int x = 10;
    float y = 3.2;

    my_printf(x, "x is %d, y is %f\n", x, y);
}
```

See what we did? On lines 12-14 we started a new va_list, and then passed it right into vprintf(). And it just wants to do with it because it has all built in. We still have to call va_end() when we're done, so don't forget that!

## Chapter 26. Locale and Internationalization

Localization is the process of making your app ready to work in different locales (countries). As you might know, not everyone uses the same character for decimal points or thousands separators—or for currency. These locales have names, and you can select one to use. For example, a US locale might write a number like:

100,000.00

Whereas in Brazil, the same might be written with the commas and decimal points swapped:

100.000,00

Makes it easier to write your code if it ports to other nationalities with ease! Well, sort of. Turns out C has only one built-in locale, and it's limited. The spec really leaves a lot of ambiguity here; it's hard to be completely portable. But we'll do our best!

## 26.1 Setting the Localization, Quick and Dirty

For these calls, <locale>. There is basically one thing you can do here in terms of declaring a specific locale. This is likely what you want to do so that the program does anything:

```c
setlocale(LC_ALL, ""); // Use this environment's locale for everything
```

You'll want to call that so that the program gets initialized with your current locale. Getting into more details, there is one more thing you can do and stay portable: but's by default every time your program starts, so there's not much need to do it yourself. By passing in an empty string for your argument, you're telling C, "Hey, figure out the current locale on this system so I don't have to tell you."

## 26.2 Getting the Monetary Locale Settings

Because moving green pieces of paper around promises to be the key to happiness¹, let's talk about monetary locale. When writing portable code, you know what to type for cash, right? Whether that's "S", "C", "V", or "L". How can you write code with such instance? Luckily, once you call locale(LC_ALL, ""), you can just look this up with a call to localeconv():

```c
struct lconv *x = localeconv();
```

This function returns a pointer to a statically-allocated lconv that has all that juicy information you're looking for. Here are the fields of struct lconv and their meanings.

First, some conversions. An _p means "positive", and n_ means "negative", and int_ means "international". A lot of these are type char or char*, most (or the strings they point to) are actually treated as integers².

Before we go further, know that CHAR_MAX (from <limits>) is the maximum value that can be in a char. And many of the following characters use that to indicate the value is not available in the locale.

| Field | Description |
| :--- | :--- |
| char *mon_decimal_point | Decimal character for money |

> ¹This planet has—or had—a problem, which this was: most of the people living on it were unhappy for much of the time. Many solutions were suggested for this, but most of these were largely concerned with the movement of green pieces of paper, which was odd because on the whole its small green pieces of paper that were unhappy." —The Hitchhiker’s Guide to the Galaxy, Douglas Adams

> ²Remember that char is just a byte-sized integer.
