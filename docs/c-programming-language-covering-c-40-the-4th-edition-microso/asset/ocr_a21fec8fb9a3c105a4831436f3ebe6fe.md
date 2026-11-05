The following example demonstrates how anonymous function type inference allows type information to “flow” between arguments in a generic method invocation. Given the method

```
static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2) {
    return f2(f1(value));
}
```

type inference for the invocation

```
double seconds = F("1:15:30", s => TimeSpan.Parse(s), t => t.TotalSeconds);
```

proceeds as follows: First, the argument “1:15:30” is related to the value parameter, inferring X to be string. Then, the parameter of the first anonymous function, s, is given the inferred type string, and the expression TimeSpan.Parse(s) is related to the return type of f1, inferring Y to be System.TimeSpan. Finally, the parameter of the second anonymous function, t, is given the inferred type System.TimeSpan, and the expression t.TotalSeconds is related to the return type of f2, inferring Z to be double. Thus the result of the invocation is of type double.

# 7.5.2.13 Type Inference for Conversion of Method Groups

Similar to calls of generic methods, type inference must also be applied when a method group M containing a generic method is converted to a given delegate type D (§6.6). Given a method

T_r M<X_1...X_n>(T_1 x_1 ... T_n x_n)

and the method group M being assigned to the delegate type D, the task of type inference is to find type arguments S_1...S_n so that the expression

M<S_1...S_n>

becomes compatible (§15.1) with D.

Unlike the type inference algorithm for generic method calls, in this case there are only argument types—no argument expressions. In particular, there are no anonymous functions and hence no need for multiple phases of inference.

Instead, all X_i are considered unfixed, and a lower-bound inference is made from each argument type U_i of D to the corresponding parameter type T_i of M. If for any of the X_i no bounds were found, type inference fails. Otherwise, all X_i are fixed to corresponding S_i, which are the result of type inference.