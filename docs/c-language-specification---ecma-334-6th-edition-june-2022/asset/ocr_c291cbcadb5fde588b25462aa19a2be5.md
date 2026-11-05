Example: The examples that follow use a generic delegate type Func<A,R> that represents a function that takes an argument of type A and returns a value of type R:

```
delegate R Func<A,R>(A arg);
```

In the assignments

```
Func<int,int> f1 = x => x + 1; // Ok
Func<int,double> f2 = x => x + 1; // Ok
Func<double,int> f3 = x => x + 1; // Error
Func<int, Task<int>> f4 = async x => x + 1; // Ok
```

the parameter and return types of each anonymous function are determined from the type of the variable to which the anonymous function is assigned.

The first assignment successfully converts the anonymous function to the delegate type Func<int,int> because, when x is given type int, x + 1 is a valid expression that is implicitly convertible to type int.

Likewise, the second assignment successfully converts the anonymous function to the delegate type Func<int,double> because the result of x + 1 (of type int) is implicitly convertible to type double.

However, the third assignment is a compile-time error because, when x is given type double, the result of x + 1 (of type double) is not implicitly convertible to type int.

The fourth assignment successfully converts the anonymous async function to the delegate type Func<int, Task<int>> because the result of x + 1 (of type int) is implicitly convertible to the effective return type int of the async lambda, which has a return type Task<int>.

end example

A lambda expression F is compatible with an expression tree type Expression<D> if F is compatible with the delegate type D. This does not apply to anonymous methods, only lambda expressions.

Anonymous functions may influence overload resolution, and participate in type inference. See §11.6 for further details.

# 10.7.2 Evaluation of anonymous function conversions to delegate types

Conversion of an anonymous function to a delegate type produces a delegate instance that references the anonymous function and the (possibly empty) set of captured outer variables that are active at the time of the evaluation. When the delegate is invoked, the body of the anonymous function is executed. The code in the body is executed using the set of captured outer variables referenced by the delegate. A delegate_creation_expression (§11.7.15.6) can be used as an alternate syntax for converting an anonymous method to a delegate type.

The invocation list of a delegate produced from an anonymous function contains a single entry. The exact target object and target method of the delegate are unspecified. In particular, it is unspecified whether the target object of the delegate is null, the this value of the enclosing function member, or some other object.

Conversions of semantically identical anonymous functions with the same (possibly empty) set of captured outer variable instances to the same delegate types are permitted (but not required) to return the same delegate instance. The term semantically identical is used here to mean that execution of the anonymous functions will, in all cases, produce the same effects given the same arguments. This rule permits code such as the following to be optimized.