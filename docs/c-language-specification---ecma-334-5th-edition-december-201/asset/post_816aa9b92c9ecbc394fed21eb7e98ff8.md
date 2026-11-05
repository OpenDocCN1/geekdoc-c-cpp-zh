
- V is one of IEnumerable<V1>, ICollection<V1>, IReadOnlyList<V1>, IReadOnlyCollection<V1> or IList<V1> and U is a single-dimensional array type U1[]
- V is a constructed class, struct, interface or delegate type C<V1...Vk> and there is a unique type C<U1...Uk> such that U (or, if U is a type parameter, its effective base class or any member of its effective interface set) is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) C<U1...Uk>.
- (The "uniqueness" restriction means that in the case interface C<T>{} class U: C<X>, C<Y>{}, then no inference is made when inferring from U to C<T> because U1 could be X or Y.)

If any of these cases apply then an inference is made from each U_i to the corresponding V_i as follows:

- If U_i is not known to be a reference type then an exact inference is made
- Otherwise, if U is an array type then a lower-bound inference is made
- Otherwise, if V is C<V1...Vk> then inference depends on the i-th type parameter of C:
  - If it is covariant then a lower-bound inference is made.
  - If it is contravariant then an upper-bound inference is made.
  - If it is invariant then an exact inference is made.
- Otherwise, no inferences are made.

### 12.6.3.11 Upper-bound inferences

An upper-bound inference from a type U to a type V is made as follows:

- If V is one of the unfixed X_i then U is added to the set of upper bounds for X_i.
- Otherwise, sets V1...Vk and U1...Uk are determined if any of the following cases apply:
  - U is an array type U1[...] and V is an array type V1[...] of the same rank
  - U is one of IEnumerable<U>, ICollection<U>, IReadOnlyList<U>, IReadOnlyCollection<U> or IList<U> and V is a single-dimensional array type V1[]
  - U is the type U? and V is the type V1?
  - U is constructed class, struct, interface or delegate type C<U1...Uk> and V is a class, struct, interface or delegate type which is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) a unique type C<V1...Vk>
  - (The "uniqueness" restriction means that if we have interface C<T>{} class V<Z>: C<X<Z>>, C<Y<Z>>{}, then no inference is made when inferring from C<U1> to V<Q>. Inferences are not made from U1 to either X<Q> or Y<Q>.)

If any of these cases apply then an inference is made from each U_i to the corresponding V_i as follows:

- If U_i is not known to be a reference type then an exact inference is made
- Otherwise, if V is an array type then an upper-bound inference is made
- Otherwise, if U is C<U1...Uk> then inference depends on the i-th type parameter of C:
  - If it is covariant then an upper-bound inference is made.
  - If it is contravariant then a lower-bound inference is made.
  - If it is invariant then an exact inference is made.
- Otherwise, no inferences are made.

### 12.6.3.12 Fixing

An unfixed type variable X_i with a set of bounds is fixed as follows:

- The set of candidate types U_j starts out as the set of all types in the set of bounds for X_i.
- We then examine each bound for X_i in turn: For each exact bound U of X_i all types U_j that are not identical to U are removed from the candidate set. For each lower bound U of X_i all types U_j to which there is not an implicit conversion from U are removed from the candidate set. For each upper-bound U of X_i all types U_j from which there is not an implicit conversion to U are removed from the candidate set.
- If among the remaining candidate types U_j there is a unique type V to which there is an implicit conversion from all the other candidate types, then X_i is fixed to V.
- Otherwise, type inference fails.

### 12.6.3.13 Inferred return type

The inferred return type of an anonymous function F is used during type inference and overload resolution. The inferred return type can only be determined for an anonymous function where all parameter types are known, either because they are explicitly given, provided through an anonymous function conversion or inferred during type inference on an enclosing generic method invocation.

The inferred effective return type is determined as follows:

- If the body of F is an expression that has a type, then the inferred effective return type of F is the type of that expression.
- If the body of F is a block and the set of expressions in the block’s return statements has a best common type T (§12.6.3.15), then the inferred effective return type of F is T.
- Otherwise, an effective return type cannot be inferred for F.

The inferred return type is determined as follows:

- If F is async and the body of F is either an expression classified as nothing (§12.2), or a statement block where no return statements have expressions, the inferred return type is System.Threading.Tasks.Task
- If F is async and has an inferred effective return type T, the inferred return type is System.Threading.Tasks.Task<T>.
- If F is non-async and has an inferred effective return type T, the inferred return type is T.
- Otherwise, a return type cannot be inferred for F.

[Example: As an example of type inference involving anonymous functions, consider the Select extension method declared in the System.Linq.Enumerable class:

```csharp
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource,TResult>(
            this IEnumerable<TSource> source,
            Func<TSource,TResult> selector)
        {
            foreach (TSource element in source) yield return
            selector(element);
        }
    }
}
```

Assuming the System.Linq namespace was imported with a using namespace directive, and given a class Customer with a Name property of type string, the Select method can be used to select the names of a list of customers:

```csharp
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

The extension method invocation (§12.7.6.3) of Select is processed by rewriting the invocation to a static method invocation:

```csharp
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

Since type arguments were not explicitly specified, type inference is used to infer the type arguments. First, the customers argument is related to the source parameter, inferring TSource to be Customer. Then, using the anonymous function type inference process described above, c is given type Customer, and the expression c.Name is related to the return type of the selector parameter, inferring TResult to be string. Thus, the invocation is equivalent to

```csharp
Enumerable.Select<Customer,string>(customers, ((Customer c) => c.Name))
```

and the result is of type IEnumerable<string>.

The following example demonstrates how anonymous function type inference allows type information to “flow” between arguments in a generic method invocation. Given the method:

```csharp
static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2) {
    return f2(f1(value));
}
```

Type inference for the invocation:

```csharp
double_seconds = F("1:15:30", s => TimeSpan.Parse(s), t =>
    t.TotalSeconds);
```

proceeds as follows: First, the argument "1:15:30" is related to the value parameter, inferring X to be string. Then, the parameter of the first anonymous function, s, is given the inferred type string, and the expression TimeSpan.Parse(s) is related to the return type of f1, inferring Y to be System.TimeSpan. Finally, the parameter of the second anonymous function, t, is given the inferred type System.TimeSpan, and the expression t.TotalSeconds is related to the return type of f2, inferring Z to be double. Thus, the result of the invocation is of type double. end example]

### 12.6.3.14 Type inference for conversion of method groups

Similar to calls of generic methods, type inference shall also be applied when a method group M containing a generic method is converted to a given delegate type D (§11.8). Given a method

```csharp
T_r M<X1...Xn>(T1 x1 ... Tn xn)
```

and the method group M being assigned to the delegate type D the task of type inference is to find type arguments S1...Sn so that the expression:

```csharp
M<S1...Sn>
```

becomes compatible (§20.2) with D.

Unlike the type inference algorithm for generic method calls, in this case, there are only argument types, no argument expressions. In particular, there are no anonymous functions and hence no need for multiple phases of inference.

Instead, all X_i are considered unfixed, and a lower-bound inference is made from each argument type U_j of D to the corresponding parameter type T_j of M. If for any of the X_i no bounds were found, type inference fails. Otherwise, all X_i are fixed to corresponding S_i, which are the result of type inference.

### 12.6.3.15 Finding the best common type of a set of expressions

In some cases, a common type needs to be inferred for a set of expressions. In particular, the element types of implicitly typed arrays and the return types of anonymous functions with block bodies are found in this way.

The best common type for a set of expressions E1...Em is determined as follows:

- A new unfixed type variable X is introduced.
