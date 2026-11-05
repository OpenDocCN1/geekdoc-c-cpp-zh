to perform will cause data to be lost from the program. It considers every operation in terms of “wide” and “narrowing” values.

# Widening and Narrowing

The general principle which C# uses is that if you are "narrowing" a value it will always ask you to explicitly tell it that this is what you want to do. If you are widening there is no problem.

To understand what we mean by these terms we could consider suitcases. If I am packing for a trip I will take a case. If I decide to switch to a smaller case I will have to take everything out of the large case and put it into the smaller one. But it might not have room, so I have to leave behind one of my shirts. This is “narrowing”.

However, if I change to a bigger case there is no problem. The bigger case will take everything that was in the smaller case and have room for more.

In C# terms the “size” of a type is the range of values (the biggest and smallest) and the precision (the number of decimal places). This means that if I write:

```
int i = 1;
float x = i;
```

This works fine because the floating point type can hold all the values supported by the integer type. However:

```
float x = 1;
int i = x;
```

- would cause the compiler to complain (even though at the moment the variable x only holds an integer value). The compiler is concerned that you may be discarding information by such an assignment and treats it as an error.

Note that this applies within floating point values as well, for example:

```
double d = 1.5;
float f = d;
```

- would cause an error as well, since the compiler knows that a double is wider than a float.

# Casting

We can force C# to regard a value as being of a certain type by the use of casting. A cast takes the form of an additional instruction to the compiler to force it to regard a value in a particular way. You cast a value by putting the type you want to see there in brackets before it. For example:

```
double d = 1.5;
float f = (float) d;
```

In the above code the message to the compiler is “I don't care that this assignment could cause the loss of information. I, as the writer of the program, will take the responsibility of making sure that the program works correctly”. You can regard casting as the compiler's way of washing its hands of the problem. If a program fails because data is lost it is not because the compiler did something silly.

As we saw above, each type of variable has a particular range of possible values, and the range of floating point values is much greater than that for integers. This means that if you do things like this:

```
int i = 1;
i = (int) 123456781234567890.999 ;
```

- the cast is doomed to fail. The value which gets placed in i will be invalid. Nothing in C# checks for mistakes like this. It is up to you when you write your program to make sure that you never exceed the range of the data types you are using - the program will not notice but the user certainly will!

> > I do not think of this as a failing in C#. It gives you great flexibility, at the cost of assuming you know what you are doing....