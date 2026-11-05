+   - Otherwise, no inferences are made.

# 11.6.3.12 Fixing

An unfixed type variable X₁ with a set of bounds is fixed as follows:

+   - The set of candidate types Uₑ starts out as the set of all types in the set of bounds for Xᵢ.
+   - We then examine each bound for Xᵢ in turn: For each exact bound U of Xᵢ, all types Uₑ that are not identical to U are removed from the candidate set. For each lower bound U of Xᵢ, all types Uₑ to which there is not an implicit conversion from U are removed from the candidate set. For each upper bound U of Xᵢ, all types Uₑ from which there is not an implicit conversion to U are removed from the candidate set.
+   - If among the remaining candidate types Uₑ there is a unique type V to which there is an implicit conversion from all the other candidate types, then Xᵢ is fixed to V.
+   - Otherwise, type inference fails.

# 11.6.3.13 Inferred return type

The inferred return type of an anonymous function F is used during type inference and overload resolution. The inferred return type can only be determined for an anonymous function where all parameter types are known, either because they are explicitly given, provided through an anonymous function conversion or inferred during type inference on an enclosing generic method invocation.

The inferred effective return type is determined as follows:

+   - If the body of F is an expression that has a type, then the inferred effective return type of F is the type of that expression.
+   - If the body of F is a block and the set of expressions in the block's return statements has a best common type T (§11.6.3.15), then the inferred effective return type of F is T.
+   - Otherwise, an effective return type cannot be inferred for F.

The inferred return type is determined as follows:

+   - If F is async and the body of F is either an expression classified as nothing (§11.2), or a block where no return statements have expressions, the inferred return type is System.Threading.Tasks.Task.
+   - If F is async and has an inferred effective return type T, the inferred return type is System.Threading.Tasks.Task<T>.
+   - If F is non-async and has an inferred effective return type T, the inferred return type is T.
+   - Otherwise, a return type cannot be inferred for F.

Example: As an example of type inference involving anonymous functions, consider the Select extension method declared in the System.Linq.Enumerable class:

```
```csharp
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource,TResult>(
            this IEnumerable<TSource> source,
            Func<TSource,TResult> selector)
        {
            foreach (TSource element in source)
```
```