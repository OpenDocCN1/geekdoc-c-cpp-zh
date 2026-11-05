
If namespaces imported by using namespace directives in the given namespace or compilation unit directly contain non-generic type declarations C_i with eligible extension methods M_e, then the set of those extension methods is the candidate set.

- If no candidate set is found in any enclosing namespace declaration or compilation unit, a compile-time error occurs.
- Otherwise, overload resolution is applied to the candidate set as described in §12.6.4. If no single best method is found, a compile-time error occurs.
- C is the type within which the best method is declared as an extension method.

Using C as a target, the method call is then processed as a static method invocation (§12.6.6).

> Note: Unlike an instance method invocation, no exception is thrown when expr evaluates to a null reference. Instead, this null value is passed to the extension method as it would be via a regular static method invocation. It is up to the extension method implementation to decide how to respond to such a call. end note

The preceding rules mean that instance methods take precedence over extension methods, that extension methods available in inner namespace declarations take precedence over extension methods available in outer namespace declarations, and that extension methods declared directly in a namespace take precedence over extension methods imported into that same namespace with a using namespace directive.

Example:

```
public static class E
{
    public static void F(this object obj, int i) { }
    public static void F(this object obj, string s) { }
}

class A { }

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
    static void Test(A a, B b, C c)
    {
        a.F(1);          // E.F(object, int)
        a.F("hello");    // E.F(object, string)
        b.F(1);          // B.F(int)
        b.F("hello");    // E.F(object, string)
        c.F(1);          // C.F(object)
        c.F("hello");    // C.F(object)
    }
}
```

In the example, B's method takes precedence over the first extension method, and C's method takes precedence over both extension methods.

```csharp
public static class C
{
    public static void F(this int i) => Console.WriteLine($"C.F({i})");
    public static void G(this int i) => Console.WriteLine($"C.G({i})");
    public static void H(this int i) => Console.WriteLine($"C.H({i})");
}
```

```csharp
namespace N1
{
    public static class D
    {
        public static void F(this int i) => Console.WriteLine($"D.F({i})");
        public static void G(this int i) => Console.WriteLine($"D.G({i})");
    }
}
```

```csharp
namespace N2
{
    using N1;

    public static class E
    {
        public static void F(this int i) => Console.WriteLine($"E.F({i})");
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

E.F(1)
D.G(2)
C.H(3)

D.G takes precedence over C.G, and E.F takes precedence over both D.F and C.F.

*end example*

## 12.8.9.4 Delegate invocations

For a delegate invocation, the primary_expression of the invocation_expression shall be a value of a delegate_type. Furthermore, considering the delegate_type to be a function member with the same parameter list as the delegate_type, the delegate_type shall be applicable (§12.6.4.2) with respect to the argument_list of the invocation_expression.

The run-time processing of a delegate invocation of the form D(A), where D is a primary_expression of a delegate_type and A is an optional argument_list, consists of the following steps:

- D is evaluated. If this evaluation causes an exception, no further steps are executed.
- The argument list A is evaluated. If this evaluation causes an exception, no further steps are executed.
- The value of D is checked to be valid. If the value of D is null, a System.NullReferenceException is thrown and no further steps are executed.
- Otherwise, D is a reference to a delegate instance. Function member invocations (§12.6.6) are performed on each of the callable entities in the invocation list of the delegate. For callable entities consisting of an instance and instance method, the instance for the invocation is the instance contained in the callable entity.

See §20.6 for details of multiple invocation lists without parameters.

## 12.8.10 Null Conditional Invocation Expression

A null_conditional_invocation_expression is syntactically either a null_conditional_member_access (§12.8.8) or null_conditional_element_access (§12.8.12) where the final dependent_access is an invocation expression (§12.8.9).

A null_conditional_invocation_expression occurs within the context of a statement_expression (§13.7), anonymous_function_body (§12.19.1), or method_body (§15.6.1).

Unlike the syntactically equivalent null_conditional_member_access or null_conditional_element_access, a null_conditional_invocation_expression may be classified as nothing.

```
null_conditional_invocation_expression
  : null_conditional_member_access '(' argument_list? ')'
  | null_conditional_element_access '(' argument_list? ')'
  ;
```

A null_conditional_invocation_expression expression E is of the form P?A; where A is the remainder of the syntactically equivalent null_conditional_member_access or null_conditional_element_access, A will therefore start with . or [. Let PA signify the concatenation of P and A.

When E occurs as a statement_expression the meaning of E is the same as the meaning of the statement:

```
if ((object)P != null) PA
```

except that P is evaluated only once.

When E occurs as an anonymous_function_body or method_body the meaning of E depends on its classification:

- If E is classified as nothing then its meaning is the same as the meaning of the block:
  { if ((object)P != null) PA; }
  except that P is evaluated only once.
- Otherwise the meaning of E is the same as the meaning of the block:
  { return E; }
  and in turn the meaning of this block depends on whether E is syntactically equivalent to a null_conditional_member_access (§12.8.8) or null_conditional_element_access (§12.8.12).

## 12.8.11 Element access

### 12.8.11.1 General

An element_access consists of a primary_no_array_creation_expression, followed by a "[" token, followed by an argument_list, followed by a "]" token. The argument_list consists of one or more arguments, separated by commas.

```
element_access
  : primary_no_array_creation_expression '[' argument_list ']'
  ;
```

The argument_list of an element_access is not allowed to contain out or ref arguments.

An element_access is dynamically bound (§12.3.3) if at least one of the following holds:

- The primary_no_array_creation_expression has compile-time type dynamic.
- At least one expression of the argument_list has compile-time type dynamic and the primary_no_array_creation_expression does not have an array type.

In this case, the compiler classifies the element_access as a value of type dynamic. The rules below to determine the meaning of the element_access are then applied at run-time, using the run-time type instead of the compile-time type of those of the primary_no_array_creation_expression and argument_list expressions which have the compile-time type dynamic. If the primary_no_array_creation_expression does not have compile-time type dynamic, then the element access undergoes a limited compile-time check as described in §12.6.5.

If the primary_no_array_creation_expression of an element_access is a value of an array_type, the element_access is an array access (§12.8.11.2). Otherwise, the primary_no_array_creation_expression shall be a variable or value of a class, struct, or interface type that has one or more indexer members, in which case the element_access is an indexer access (§12.8.11.3).

### 12.8.11.2 Array access

For an array access, the primary_no_array_creation_expression of the element_access shall be a value of an array_type. Furthermore, the argument_list of an array access is not allowed to contain named arguments. The number of expressions in the argument_list shall be the same as the rank of the array_type, and each expression shall be of type int, uint, long, or ulong, or shall be implicitly convertible to one or more of these types.

The result of evaluating an array access is a variable of the element type of the array, namely the array element selected by the value(s) of the expression(s) in the argument_list.

The run-time processing of an array access of the form P[A], where P is a primary_no_array_creation_expression of an array_type and A is an argument_list, consists of the following steps:

- P is evaluated. If this evaluation causes an exception, no further steps are executed.
- The index expressions of the argument_list are evaluated in order, from left to right. Following evaluation of each index expression, an implicit conversion (§10.2) to one of the following types is performed: int, uint, long, ulong. The first type in this list for which an implicit conversion exists is chosen. For instance, if the index expression is of type short then an implicit conversion to int is performed, since implicit conversions from short to int and from short to long are possible. If evaluation of an index expression or the subsequent implicit conversion causes an exception, then no further index expressions are evaluated and no further steps are executed.
