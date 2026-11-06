+   - First, a set of *candidate functions* is constructed. This set contains all functions that:
+     - are visible at the point of the call;
+     - have the same names as the called function.

As function 11 has a different name, it is removed from the set. The compiler is left with a set of 10 candidate functions.

+   - Second, the set of *viable functions* is constructed. Viable functions are functions for which type conversions exist that can be applied so as to match the types of the function’s parameters to the types of the actual arguments.
+   
+     This implies that at least the number of arguments must match the number of parameters of the viable functions. Function 10’s first argument is a `string`. As a `string` cannot be initialized by an `int` value no appropriate conversion exists and function 10 is removed from the list of candidate functions. `double` parameters can be retained. Standard conversions do exist for `ints` to `doubles`, so all functions having ordinary `double` parameters can be retained. Therefore, the set of viable functions consists of functions 1 through 9.

At this point the compiler tries to determine the types of the template type parameters. This step is outlined in the following subsection.

# ## 20.15 Determining the template type parameters

Having determined the set of candidate functions and from that the set of viable functions the compiler must now determine the actual types of the template type parameters.

It may use any of the three standard template parameter transformation procedures (cf. section 20.4) when trying to match actual types to template type parameters. In this process it concludes that no type can be determined for T in function 1’s T &t1 parameter as the argument 3 is a constant int value. Thus function 1 is removed from the list of viable functions. The compiler is now confronted with the following set of potentially instantiated function templates and ordinary functions:

```
void process(T1 [≡ int] const &t1, T2 [≡ int] const &t2);    // 2
void process(T [≡ int] const &t, double d);                  // 3
void process(T [≡ int] const &t, int i);                     // 4
void process(int, int)(int i1, int i2);                      // 5
void process(int i, int i);                                  // 6
void process(int i, double d);                               // 7
void process(double d, int i);                               // 8
void process(double d1, double d2);                          // 9
```

The compiler associates a *direct match count* value to each of the viable functions. The direct match count counts the number of arguments that can be matched to function parameters without an (auto-matic) type conversion. E.g., for function 2 this count equals 2, for function 7 it is 1 and for function 9 it is 0. The functions are now (decrementally) sorted by their direct match count values:

```
                                                     match
                                                     count
void process(T1 [≡ int] const &t1, T2 [≡ int] const &t2);  2 // 2
void process(T [≡ int] const &t, int i);                  2 // 4
void process(int, int)(int i1, int i2);                   2 // 5
void process(int i, int i2);                              2 // 6
void process(T [≡ int] const &t, double d);               1 // 3
void process(int i, double d);                            1 // 7
void process(double d, int i);                            1 // 8
void process(double d1, double d2);                       0 // 9
```