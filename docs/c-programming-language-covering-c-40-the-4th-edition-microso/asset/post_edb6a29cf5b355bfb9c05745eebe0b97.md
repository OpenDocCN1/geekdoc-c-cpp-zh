
U is constructed class, struct, interface, or delegate type C<U1, ..., Un> and V is a class, struct, interface, or delegate type that is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) a unique type C<V1, ..., Vn>.

(The "uniqueness" restriction means that if we have interface C<T>{} class V<Z>: C<X<Z>>, C<V<Z>>{}, then no inference is made when inferring from C<U> to V<Q>. Inferences are not made from U1 to either X<Q> or V<Q>.)

If any of these cases apply, then an inference is made from each Ui to the corresponding Vi as follows:

- If Ui is not known to be a reference type, then an exact inference is made.
- Otherwise, if V is an array type, then an upper-bound inference is made.
- Otherwise, if U is C<U1, ..., Un>, then inference depends on the i-th type parameter of C:
  - If it is covariant, then an upper-bound inference is made.
  - If it is contravariant, then a lower-bound inference is made.
  - If it is invariant, then an exact inference is made.
- Otherwise, no inferences are made.

> **VLADIMIR RESHETNIKOV** So, no inferences are ever made for method type parameters that do not appear in the parameter types of the generic method. For example, no inferences are made for parameters that appear only in constraints:
> 
> ```csharp
> using System.Collections.Generic;
> 
> class C
> {
>     static void Foo<T,U>(T x) where T : IEnumerable<U> { }
> 
>     static void Main()
>     {
>         Foo(new List<int>());
>         // Error CS0411: The type arguments for method
>         // 'C.Foo<T,U>(T)' cannot be inferred from the
>         // usage.
>     }
> }
> ```

## 7.5.2.11 Fixing

An unfixed type variable Xi with a set of bounds is fixed as follows:

- The set of candidate types Uj starts out as the set of all types in the set of bounds for Xi.

> **ERIC LIPPERT**  This condition illustrates a subtle design point of C#. When faced with the need to choose a “best type” given a set of types, we always choose one of the types in the set. That is, if asked to choose the best type in `{Cat, Dog, Goldfish}`, we fail to find a best type; we never say, “The common base type Animal is the best we can do given those three choices” because Animal is not one of the choices in the first place.

- We then examine each bound for xᵢ in turn: For each bound U of xᵢ, all types Uⱼ that are not identical to U are removed from the candidate set. For each lower bound U of xᵢ, all types Uⱼ to which there is not an implicit conversion from U are removed from the candidate set. For each upper bound U of xᵢ, all types Uⱼ from which there is not an implicit conversion to U are removed from the candidate set.
- If among the remaining candidate types Uⱼ there is a unique type V from which there is an implicit conversion to all other candidate types, then xᵢ is fixed to V.
- Otherwise, type inference fails.

> **ERIC LIPPERT**  In C# 2.0, the generic method type inference algorithm failed if two distinct bounds were computed for the same type parameter. In C# 3.0, we have situations such as the Join method, which must infer the type of the “key” upon which the two collections are joined. If the key in one collection is, say, `int`, and the corresponding key in the other collection is `int?`, then we have two distinct types. Because every int may be converted to int?, however, we could allow the ambiguity and resolve it by picking the more general of the two types. C# 4.0 supports generic variance, which complicates the situation further; now we might have upper, lower, and exact bounds on a type parameter.

## 7.5.2.12 Inferred Return Type

The *inferred return type* of an anonymous function F is used during type inference and overload resolution. The inferred return type can only be determined for an anonymous function where all parameter types are known, either because they are explicitly given, provided through an anonymous function conversion, or inferred during type inference on an enclosing generic method invocation. The inferred return type is determined as follows:

- If the body of F is an *expression*, then the inferred return type of F is the type of that expression.
- If the body of F is a *block* and the set of expressions in the block’s return statements has a best common type T (§7.5.2.14), then the inferred return type of F is T.

![](img/04b421b044b1254de966ab5335775a89_284_0.png)

> > **VLADIMIR RESHETNIKOV** Even return statements in unreachable code are included in the set and participate in calculation of the inferred return type. This has a surprising consequence, in that removing unreachable code can change the program behavior.

- Otherwise, a return type cannot be inferred for F.

As an example of type inference involving anonymous functions, consider the `Select` extension method declared in the `System.Linq.Enumerable` class:

```
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource, TResult>(
            this IEnumerable<TSource> source,
            Func<TSource, TResult> selector)
        {
            foreach (TSource element in source)
                yield return selector(element);
        }
    }
}
```

Assuming the `System.Linq` namespace was imported with a using clause, and given a class Customer with a Name property of type string, the Select method can be used to select the names of a list of customers:

```
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

The extension method invocation (§7.6.5.2) of Select is processed by rewriting the invocation to a static method invocation:

```
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

Since type arguments were not explicitly specified, type inference is used to infer the type arguments. First, the customers argument is related to the source parameter, inferring T to be Customer. Then, using the anonymous function type inference process described above, c is given type Customer, and the expression c.Name is related to the return type of the selector parameter, inferring S to be string. Thus the invocation is equivalent to

```
Enumerable.Select<Customer,string>(customers, (Customer c) => c.Name)
```

and the result is of type `IEnumerable<string>`.

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

## 7.5.2.13 Type Inference for Conversion of Method Groups

Similar to calls of generic methods, type inference must also be applied when a method group M containing a generic method is converted to a given delegate type D (§6.6). Given a method

T_r M<X_1...X_n>(T_1 x_1 ... T_n x_n)

and the method group M being assigned to the delegate type D, the task of type inference is to find type arguments S_1...S_n so that the expression

M<S_1...S_n>

becomes compatible (§15.1) with D.

Unlike the type inference algorithm for generic method calls, in this case there are only argument types—no argument expressions. In particular, there are no anonymous functions and hence no need for multiple phases of inference.

Instead, all X_i are considered unfixed, and a lower-bound inference is made from each argument type U_i of D to the corresponding parameter type T_i of M. If for any of the X_i no bounds were found, type inference fails. Otherwise, all X_i are fixed to corresponding S_i, which are the result of type inference.
