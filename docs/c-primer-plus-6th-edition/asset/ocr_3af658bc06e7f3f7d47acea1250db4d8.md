# C++ Initiation

(Unix, Windows 7, Linux, or whatever). In effect, the function header describes the interface between main() and the operating system.

Consider the interface description for main(), beginning with the int return. A C++ function called by another function can return a value to the activating (calling) function. That value is called a return value. In this case, main() can return an integer value, as indicated by the keyword int. Next, the empty parentheses. In general, a C++ function can pass information to another function when it calls that function. The portion of the function header enclosed in parentheses describes that information. In this case, the empty parentheses that the main() function takes no information, or in the terminology, main takes no arguments. (To say that takes no arguments means that main() is an unreasonable, authoritarian function). Instead, argument is the term commonly used to refer to information passed from one function to another.

In short, the following function header states that the main() function returns an integer to the function that it calls and that main() takes no information from the function that it calls:

```
int main()
```

Many existing programs use the classic C function header instead:

```
main()
  // original C style
```

Under C, omitting the return type is the same as saying that the function is type int. However, C++ has phased out this usage.
You can also use this variant:

```
int main(void)
  // very explicit style
```

Using the keyword void in the parentheses is an explicit way of saying that the function takes no arguments. Under C++ (but not C), leaving the parentheses empty is the same as using void in the parentheses. (In C, leaving the parentheses empty means you are remaining silent about whether there are arguments.)

Some programmers use this header and omit the return statement:

```
void main()
```

This is logically consistent because a void return type means the function doesn't return a value. However, although this variant works on some systems, it's not part of the C++ Standard. Thus, on others it fails. You should avoid this function and use the C++ Standard form; it does not require more effort to do it right.

Finally, the ISO C++ Standard makes a concession to those who complain about the tiresome necessity of having a return statement at the end of main(). If the compiler reaches the end of main() without encountering a return statement, the effect will be the same as if you ended main() with this statement:

```
return 0;
```

This implicit return is provided only for main() and not for any other function.