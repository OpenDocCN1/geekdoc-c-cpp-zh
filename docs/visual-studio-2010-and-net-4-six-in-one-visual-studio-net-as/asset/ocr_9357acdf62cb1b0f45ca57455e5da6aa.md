In the first two TransformMacawCalls, the Func<Macaw, Pet> arguments are substituted with
Func<Macaw, Dog> and Func<Pet, Eagle>, respectively. The invocation of TransformDogTo,
a Func<Pet, Eagle> is used instead of the Func<Dog, Pet>. It is entirely valid, strongly typed,
and no conversion magic is done behind the scenes!

Why, for example, Func<Dog, Pet> be substituted with Func<Pet, Eagle>? The fact that
Func<Dog, Pet> is covariant in Pet means that you can return a derived type, namely Eagle,
because an Eagle is a Pet. The same thinking says that Func<Dog, Pet> is contravariant in Dog,
and any operation with Pet also will work on Dog, because Dog is derived from Pet. Therefore,
Func<Pet, Eagle> is a good substitution for Func<Dog, Pet>.

# Variance with Type Options

Obviously, we are not constrained to using only the generic types with variant type
parameters. You can create your own generic interfaces and delegates. use the in modifier
s own a contravariant, and the out for a covariant type parameter. Without a
modifier, type parameter remains invariant.

For example, consider the following declarations:

```
public interface IOperations<in T, U, V> { ... }
public delegate X YDelegate<in T, U, out X>(T t, U u);
```

Here, x is covariant, T is contravariant, and U are invariant type parameters.

The compiler ensures that you keep within the rules for variant type parameters. For
example, in the following interface, all method declarations are invalid because one
more contravariant type parameters are in output positions:

```
public interface IOperations<in T, U, V> {
  T OutputUnsafeOp1(T t);
  U OutputUnsafeOp2(T t);
  List<T> OutputUnsafeOp3();
  Func<V, U> OutputUnsafeOp4();
  void OutputUnsafeOp5(out T t);
  void OutputUnsafeOp6(ref Func<V, U> u, ref T t);
}
```

Similarly, in the following interface definition, all operations are invalid because covariant variant
parameters are in input positions:

```
public interface IOperations<out T, U> {
  void InputUnsafeOp1(T t);
  U InputUnsafeOp2(T t);
  Func<U, T> InputUnsafeOp3(out T t);
  void InputUnsafeOp4(U u, ref T t);
}
```