# Explicit Casting (manually) - converting a larger type to a smaller size type

Double -> float -> long -> int -> char

# Implicit Casting

Implicit casting is done automatically when passing a smaller size type to a larger size type:

# Example::

```
Int myint = 9;
```

```
Double mydouble = myint;    // Automatic casting: int to double
```

```
Console.writeline(myint);    // Outputs 9
```

```
Console.writeline(mydouble); // Outputs 9
```

# Explicit Casting

Explicit casting must be done manually by placing the type in parentheses in front of the value:

# Example::

```
Double mydouble = 9.78;
```

```
Int myint = (int) mydouble;    // Manual casting: double to int
```