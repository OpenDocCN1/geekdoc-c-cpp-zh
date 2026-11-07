![](bbox=[0.346, 0.088, 0.818, 0.193])

**Figure 9.1** Original variable and reference variable

are in fact the same memory location called by different names. For this reason, we need to *bind* a reference variable to the original variable immediately when we declare it. Binding is done through initializing the reference variable with the name of the original variable. The following shows the creation of an original variable of type *int* named *score* and the binding of a reference variable of type *int&* to it.

```
```cpp
int score = 92;              // Declaring and initializing variable score of type int
int& rScore = score;          // Declaring variable rScore of type int& and binding it
```
```

Figure 9.1 shows the situation in memory. We have only one memory location, but with two names. One of the names defines the original variable; the other name defines a reference to that variable.

The interesting point is that the same value, 92, is seen as an *int* type when accessed through the *score* variable; it is seen as an *int&* type when accessed through the *rScore* variable.

The name we have used for a reference variable is the same as the original name, but we add an r at the beginning and make the first letter of the original name uppercase. This is not a mandate. This is our convention and helps us remember to which original variable our reference variable is bound.

# Compound Type

Although the original variable and the reference variable define the same location in memory with the same value seen by both of them, the types of the original variable and the reference variable are different. For example, in Figure 9.1, the type of variable *score* is *int*, but the type of variable *rScore* is *int&*. In other words, the use of reference variables creates a new compound type: **reference type**. A reference type is a compound type because we can have a reference to an *int* (*int&*), a reference to a *double* (*double&*), a reference to a *bool* (*bool&*), and so on. When we bind a variable to a reference variable, the type of the reference variable should be a reference to the type of the original variable. The following is a compilation error. We cannot initialize a reference variable of *double&* to refer to a variable of type *int*.

```
```cpp
int num = 100;
double& rNum = num;            // Compilation error. Type mismatch
```
```

# Permanent Binding

After a reference variable has been declared and bound to a variable name, a *reference* relationship has been created between them and cannot be broken until the variables are destroyed (go out of scope). In C++ parlance, we say that the relationship between a variable and the corresponding reference variable is a constant relation. Figure 9.2 shows that we cannot change the reference relation after it has been created.