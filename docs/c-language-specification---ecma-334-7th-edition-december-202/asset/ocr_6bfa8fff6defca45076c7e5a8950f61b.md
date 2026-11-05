+   - E has a type S, and an identity conversion exists from S to T
+   - E is an anonymous function, T is either a delegate type D or an expression tree type `Expression<D>` and one of the following holds:
+     - An inferred return type X exists for E in the context of the parameter list of D (§12.6.3.12), and an identity conversion exists from X to the return type of D
+     - E is an async lambda with no return value, and S is a non-generic «TaskType»
+     - Either E is non-async and D has a return type V or E is async and D has a return type «TaskType<V>» (§15.15.1), and one of the following holds:
+       - The body of E is an expression that exactly matches Y
+       - The body of E is a block where every return statement returns an expression that exactly matches Y

# 12.6.4.7 Better conversion target

Given two types T₁ and T₂, T₁ is a better conversion target than T₂ if one of the following holds:

+   - An implicit conversion from T₁ to T₂ exists and no implicit conversion from T₂ to T₁ exists
+   - T₁ is «TaskType<S₁» (§15.15.1), T₂ is «TaskType<S₂», and S₁ is a better conversion target than S₂
+   - T₁ is «TaskType<S₁» (§15.15.1), T₂ is «TaskType» S₂>, and T₁ is more specialized than T₂
+   - T₁ is S₁? where S₁ is a signed integral type, and T₂ is S₂? where S₂ is an unsigned integral type. Specifically:
+     - S₁ is sbyte and S₂ is byte, ushort, uint, or ulong
+     - S₁ is short and S₂ is ushort, uint, or ulong
+     - S₁ is int and S₂ is uint, or ulong
+     - S₁ is long and S₂ is ulong

# 12.6.4.8 Overloading in generic classes

Note: While signatures as declared shall be unique (§8.6), it is possible that substitution of type arguments results in identical signatures. In such a situation, overload resolution will pick the most specific (§12.6.4.3) of the original signatures (before substitution of type arguments), if it exists, and otherwise report an error. end note

Example: The following examples show overloads that are valid and invalid according to this rule:

```
public interface I1<T> { ... }
public interface I2<T> { ... }

public abstract class G1<U>
{
    public abstract int F1(U u);        // Overload resolution for G<int>.F1
    public abstract int F1(int i);      // will pick non-generic

    public abstract void F2(I1<U> a);   // Valid overload
    public abstract void F2(I2<U> a);
}

abstract class G2<U,V>
```