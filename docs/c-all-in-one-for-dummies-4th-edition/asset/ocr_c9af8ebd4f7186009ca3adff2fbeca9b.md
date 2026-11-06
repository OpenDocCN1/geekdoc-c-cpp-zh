# Pointers to functions

When an application is running, the functions in the application exist in the memory; so just like anything else in memory, they have an address.

You can access the address of a function by taking the name of it and putting the address-of operator (&) in front of the function name, like this:

```
address = &MyFunction;
```

But to make this work, you need to know what type to declare address. The address variable is a pointer to a function, and the cleanest way to assign a type is to use auto, like this:

```
auto address = &MyFunction;
```

The traditional method is to use a typedef (as shown in the FunctionPointer01 example). Here’s the typedef you need:

```
typedef int(*FunctionPtr)(int);
```

It’s hard to follow, which is why using auto is better, but the name of the new type is FunctionPtr. This defines a type called FunctionPtr that returns an integer (the leftmost int) and takes an integer as a parameter (the rightmost int, which must be in parentheses). The middle part of this statement is the name of the new type, and you must precede it by an asterisk, which means that it’s a pointer to all the rest of the expression. Also, you must put the type name and its preceding asterisk inside parentheses. Now you’re ready to declare some variables! Here goes:

```
FunctionPtr address = &MyFunction;
```

This line declares address as a pointer to a function and initializes it to MyFunction(). For this to work, the code for MyFunction() must have the same prototype declared in the typedef: In this case, it must take an integer as a parameter and return an integer. So, for example, you may have a function like this:

```
int TheSecretNumber(int x) {
  return x + 1;
}
```