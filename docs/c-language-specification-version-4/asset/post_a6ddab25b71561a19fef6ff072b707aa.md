
```
class B
{
    public void F(int i) { }
}
class C
{
    public void F(object obj) { }
}
class X
{
    static void Test(A a, B b, C c) {
        a.F(1);      // E.F(object, int)
        a.F("hello"); // E.F(object, string)
        b.F(1);      // B.F(int)
        b.F("hello"); // E.F(object, string)
        c.F(1);      // C.F(object)
        c.F("hello"); // C.F(object)
    }
}
```

In the example, B’s method takes precedence over the first extension method, and C’s method takes precedence over both extension methods.

```
public static class C
{
    public static void F(this int i) { Console.WriteLine("C.F({0})", i); }
    public static void G(this int i) { Console.WriteLine("C.G({0})", i); }
    public static void H(this int i) { Console.WriteLine("C.H({0})", i); }
}
namespace N1
{
    public static class D
    {
        public static void F(this int i) { Console.WriteLine("D.F({0})", i); }
        public static void G(this int i) { Console.WriteLine("D.G({0})", i); }
    }
}
namespace N2
{
    using N1;
    public static class E
    {
        public static void F(this int i) { Console.WriteLine("E.F({0})", i); }
    }
    class Test
    {
        static void Main(string[] args)
        {
            1.F();
            2.G();
            3.H();
        }
    }
}
```

The output of this example is:

```
E.F(1)
D.G(2)
C.H(3)
```

D.G takes precedence over C.G, and E.F takes precedence over both D.F and C.F.

## 7.6.5.3 Delegate invocations

For a delegate invocation, the primary-expression of the invocation-expression must be a value of a delegate-type. Furthermore, considering the delegate-type to be a function member with the same parameter list as the delegate-type, the delegate-type must be applicable (§7.5.3.1) with respect to the argument-list of the invocation-expression.

The run-time processing of a delegate invocation of the form D(A), where D is a primary-expression of a delegate-type and A is an optional argument-list, consists of the following steps:

- D is evaluated. If this evaluation causes an exception, no further steps are executed.
- The value of D is checked to be valid. If the value of D is null, a System.NullReferenceException is thrown and no further steps are executed.
- Otherwise, D is a reference to a delegate instance. Function member invocations (§7.5.4) are performed on each of the callable entities in the invocation list of the delegate. For callable entities consisting of an instance and instance method, the instance for the invocation is the instance contained in the callable entity.

## 7.6.6 Element access

An element-access consists of a primary-no-array-creation-expression, followed by a “[” token, followed by an argument-list, followed by a “]” token. The argument-list consists of one or more arguments, separated by commas.

```
element-access:
    primary-no-array-creation-expression [ argument-list ]
```

The argument-list of an element-access is not allowed to contain ref or out arguments.

An element-access is dynamically bound (§7.2.2) if at least one of the following holds:

- The primary-no-array-creation-expression has compile-time type dynamic.
- At least one expression of the argument-list has compile-time type dynamic and the primary-no-array-creation-expression does not have an array type.

The run-time processing of an array access of the form P[A], where P is a primary-no-array-creation-expression of an array-type and A is an argument-list, consists of the following steps:

- P is evaluated. If this evaluation causes an exception, no further steps are executed.
- The index expressions of the argument-list are evaluated in order, from left to right. Following evaluation of each index expression, an implicit conversion (§6.1) to one of the following types is performed: int, uint, long, ulong. The first type in this list for which an implicit conversion exists is chosen. For instance, if the index expression is of type short then an implicit conversion to int is performed, since implicit conversions from short to int and from short to long are possible. If evaluation of an index expression or the subsequent implicit conversion causes an exception, then no further index expressions are evaluated and no further steps are executed.
- The value of P is checked to be valid. If the value of P is null, a System.NullReferenceException is thrown and no further steps are executed.
- The value of each expression in the argument-list is checked against the actual bounds of each dimension of the array instance referenced by P. If one or more values are out of range, a System.IndexOutOfRangeException is thrown and no further steps are executed.
- The location of the array element given by the index expression(s) is computed, and this location becomes the result of the array access.

### 7.6.6.2 Indexer access

For an indexer access, the primary-no-array-creation-expression of the element-access must be a variable or value of a class, struct, or interface type, and this type must implement one or more indexers that are applicable with respect to the argument-list of the element-access.

The binding-time processing of an indexer access of the form P[A], where P is a primary-no-array-creation-expression of a class, struct, or interface type T, and A is an argument-list, consists of the following steps:

- The set of indexers provided by T is constructed. The set consists of all indexers declared in T or a base type of T that are not override declarations and are accessible in the current context (§3.5).
- The set is reduced to those indexers that are applicable and not hidden by other indexers. The following rules are applied to each indexer S.I in the set, where S is the type in which the indexer I is declared:
  - If I is not applicable with respect to A (§7.5.3.1), then I is removed from the set.
  - If I is applicable with respect to A (§7.5.3.1), then all indexers declared in a base type of S are removed from the set.
  - If I is applicable with respect to A (§7.5.3.1) and S is a class type other than object, all indexers declared in an interface are removed from the set.
- If the resulting set of candidate indexers is empty, then no applicable indexers exist, and a binding-time error occurs.
- The best indexer of the set of candidate indexers is identified using the overload resolution rules of §7.5.3. If a single best indexer cannot be identified, the indexer access is ambiguous, and a binding-time error occurs.
- The index expressions of the argument-list are evaluated in order, from left to right. The result of processing the indexer access is an expression classified as an indexer access. The indexer access expression references the indexer determined in the step above, and has an associated instance expression of P and an associated argument list of A.

Depending on the context in which it is used, an indexer access causes invocation of either the get-accessor or the set-accessor of the indexer. If the indexer access is the target of an assignment, the set-accessor is invoked to assign a new value (§7.17.1). In all other cases, the get-accessor is invoked to obtain the current value (§7.1.1).

## 7.6.7 This access

A this-access consists of the reserved word this.

```
this-access:
    this
```

A this-access is permitted only in the block of an instance constructor, an instance method, or an instance accessor. It has one of the following meanings:

- When this is used in a primary-expression within an instance constructor of a class, it is classified as a value. The type of the value is the instance type (§10.3.1) of the class within which the usage occurs, and the value is a reference to the object being constructed.
- When this is used in a primary-expression within an instance method or instance accessor of a class, it is classified as a value. The type of the value is the instance type (§10.3.1) of the class within which the usage occurs, and the value is a reference to the object for which the method or accessor was invoked.
- When this is used in a primary-expression within an instance constructor of a struct, it is classified as a variable. The type of the variable is the instance type (§10.3.1) of the struct within which the usage occurs, and the variable represents the struct being constructed. The this variable of an instance constructor of a struct behaves exactly the same as an out parameter of the struct type—in particular, this means that the variable must be definitely assigned in every execution path of the instance constructor.
- When this is used in a primary-expression within an instance method or instance accessor of a struct, it is classified as a variable. The type of the variable is the instance type (§10.3.1) of the struct within which the usage occurs, and the variable represents the struct for which the usage occurs.
  - If the method or accessor is not an iterator (§10.14), the this variable represents the struct for which the method or accessor was invoked, and behaves exactly the same as a ref parameter of the struct type.
  - If the method or accessor is an iterator, the this variable represents a copy of the struct for which the method or accessor was invoked, and behaves exactly the same as a value parameter of the struct type.

Use of this in a primary-expression in a context other than the ones listed above is a compile-time error. In particular, it is not possible to refer to this in a static method, a static property accessor, or in a variable-initializer of a field declaration.

## 7.6.8 Base access

A base-access consists of the reserved word base followed by either a "." token and an identifier or an argument-list enclosed in square brackets:

```
base-access:
    base . identifier
    base [ argument-list ]
```

A base-access is used to access base class members that are hidden by similarly named members in the current class or struct. A base-access is permitted only in the block of an instance constructor, an instance method, or an instance accessor. When base.I occurs in a class or struct, I must denote a member of the base class of that class or struct. Likewise, when base[E] occurs in a class, an applicable indexer must exist in the base class.

At binding-time, base-access expressions of the form base.I and base[E] are evaluated exactly as if they were written ((B)this).I and ((B)this)[E], where B is the base class of the class or struct in which the
