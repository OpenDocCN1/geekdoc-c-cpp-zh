a constant, while, e.g., a DateTime object can’t be used as a constant.

Since the compiler needs to know the value immediately, it also means that there are some limitations to what we have to do when setting the value. For instance, these are perfect examples of what you CAN do:

```
const int a = 10;
const float b = a * 2.5f;
const string s1 = "Hello, world!";
const string s2 = s1 + " How are you?";
```

On the other hand, you can’t use the result of a method call or a nonconstant class member since these are not constant expressions. Let us discuss some examples of what you can’t do:

```
// NOT possible:
const int a = Math.Cos(4) * 2;
// Possible:
const string s1 = "Hello, world!";
// NOT possible:
const string s2 = s1.Substring(0, 6) + " Universe";
```

The difference lies in what the compiler can be expected to know when it reaches your code, e.g. numbers, strings, and other constants, in contrast to what it has to execute to get the value for.

# A Constant Alternative: The Read-Only Field

If you’re looking for a slightly less restrictive version of a class constant, you may want to have a look at the read-only