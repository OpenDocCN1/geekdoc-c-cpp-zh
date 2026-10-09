The probability of winning any prize is pretty small. You can easily (at least approximately) compute the odds of winning a prize, and it's less than 5%. The author had to play this game many times to get the one win (so that he could include its output in the book). It was the most difficult part of writing this book. 😊

# 15.2.2. Grammar

An *enum* type is a value type. It defines a custom integral numeric type. The enum types are used essentially to define a set of (related) named integer constants.

To define an enum type, we use the *enum* keyword and specify the names of enum members:

```
enum Prize {
   Mega,
   // ...
}
```

By default, the associated constant values of the enum members are of type *int*. You can explicitly specify any other integral numeric type as the underlying type of an enum type. For example,

```
enum Prize : byte {
   Mega,
   // ...
}
```

The enum values start with zero by default and increase by one in the order defined. One can also explicitly set a specific constant value for each enum member, if desired.