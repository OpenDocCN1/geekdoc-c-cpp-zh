
- A is a type parameter having the value type constraint (§15.2.5).
- A is a class that is not abstract and contains an explicitly declared public constructor with no parameters.
- A is not abstract and has a default constructor (§15.11.5).

A compile-time error occurs if one or more of a type parameter’s constraints are not satisfied by the given type arguments.

Since type parameters are not inherited, constraints are never inherited either. [Example: In the following, D needs to specify the constraint on its type parameter T so that T satisfies the constraint imposed by the base class B<T>. In contrast, class E need not specify a constraint, because List<T> implements IEnumerable for any T.

```
class B<T> where T: IEnumerable {...}
class D<T>: B<T> where T: IEnumerable {...}
class E<T>: B<List<T>> {...}
```

end example

## 9.5 Type parameters

A type parameter is an identifier designating a value type or reference type that the parameter is bound to at run-time.

```
type-parameter:
    identifier
```

Since a type parameter can be instantiated with many different type arguments, type parameters have slightly different operations and restrictions than other types. [Note: These include:

- A type parameter cannot be used directly to declare a base class (§15.2.4.2) or interface (§18.2.4).
- The rules for member lookup on type parameters depend on the constraints, if any, applied to the type parameter. They are detailed in §12.5.
- The available conversions for a type parameter depend on the constraints, if any, applied to the type parameter. They are detailed in §11.2.11 and §11.3.8.
- The literal null cannot be converted to a type given by a type parameter, except if the type parameter is known to be a reference type (§11.2.11). However, a default expression (§12.7.15) can be used instead. In addition, a value with a type given by a type parameter can be compared with null using == and != (§12.11.7) unless the type parameter has the value type constraint.
- A new expression (§12.7.11.2) can only be used with a type parameter if the type parameter is constrained by a constructor-constraint or the value type constraint (§15.2.5).
- A type parameter cannot be used anywhere within an attribute.
- A type parameter cannot be used in a member access (§12.7.5) or type name (§8.8) to identify a static member or a nested type.
- A type parameter cannot be used as an unmanaged-type (§23.3).

end note

As a type, type parameters are purely a compile-time construct. At run-time, each type parameter is bound to a run-time type that was specified by supplying a type argument to the generic type declaration. Thus, the type of a variable declared with a type parameter will, at run-time, be a closed constructed type (§9.4.3). The run-time execution of all statements and expressions involving type parameters uses the type that was supplied as the type argument for that parameter.

## 9.6 Expression tree types

Expression trees permit lambda expressions to be represented as data structures instead of executable code. Expression trees are values of expression tree types of the form `System.Linq.Expressions.Expression<TDelegate>`, where `TDelegate` is any delegate type. For the remainder of this specification we will refer to these types using the shorthand `Expression<TDelegate>`.

If a conversion exists from a lambda expression to a delegate type `D`, a conversion also exists to the expression tree type `Expression<TDelegate>`. Whereas the conversion of a lambda expression to a delegate type generates a delegate that references executable code for the lambda expression, conversion to an expression tree type creates an expression tree representation of the lambda expression.

Expression trees are efficient in-memory data representations of lambda expressions and make the structure of the lambda expression transparent and explicit.

Just like a delegate type `D`, `Expression<TDelegate>` is said to have parameter and return types, which are the same as those of `D`.

> [Example: The following program represents a lambda expression both as executable code and as an expression tree. Because a conversion exists to `Func<int, int>`, a conversion also exists to `Expression<Func<int, int>>`:

```
    Func<int, int> del = x => x + 1;            // Code
    Expression<Func<int, int>> exp = x => x + 1; // Data
```

> Following these assignments, the delegate `del` references a method that returns `x + 1`, and the expression tree `exp` references a data structure that describes the expression `x => x + 1`. end example]

The exact definition of the generic type `Expression<TDelegate>` as well as the precise rules for constructing an expression tree when a lambda expression is converted to an expression tree type, are implementation dependent.

Two things are important to make explicit:

- Not all lambda expressions can be converted to expression trees. For instance, lambda expressions with statement bodies, and lambda expressions containing assignment expressions cannot be represented. In these cases, a conversion still exists, but it will fail at compile-time. These exceptions are detailed in §11.7.3.
- `Expression<TDelegate>` offers an instance method `Compile` which produces a delegate of type `TDelegate`:

```
      Func<int, int> del2 = exp.Compile();
```

    Invoking this delegate causes the code represented by the expression tree to be executed. Thus, given the definitions above, `del1` and `del2` are equivalent, and the following two statements will have the same effect:

```
      int i1 = del1();
      int i2 = del2(1);
```

    After executing this code, `i1` and `i2` will both have the value 2.

## 9.7 The dynamic type

The type `dynamic` has special meaning in C#. Its purpose is to allow dynamic binding, which is described in detail in §12.3.2.

`dynamic` is considered identical to `object` except in the following respects:

- Operations on expressions of type `dynamic` can be dynamically bound (§12.3.3).
- Type inference (§12.6.3) will prefer `dynamic` over `object` if both are candidates.
- `dynamic` cannot be used as
  - the type in an `object`-creation-expression (§12.7.11.2)
  - a predefined-type in a member-access (§12.7.5.1)
  - the operand of the typeof operator
  - an attribute argument
  - a constraint
  - an extension method type
  - any part of a type argument within struct-interfaces (§16.2.4) or interface-type-list (§15.2.4.1).

Because of this equivalence, the following holds:

- There is an implicit identity conversion between object and dynamic, and between constructed types that are the same when replacing dynamic with object
- Implicit and explicit conversions to and from object also apply to and from dynamic.
- Signatures that are the same when replacing dynamic with object are considered the same signature
- The type dynamic is indistinguishable from object at run-time.
- An expression of the type dynamic is referred to as a **dynamic expression**.

## 10. Variables

### 10.1 General

Variables represent storage locations. Every variable has a type that determines what values can be stored in the variable. C# is a type-safe language, and the C# compiler guarantees that values stored in variables are always of the appropriate type. The value of a variable can be changed through assignment or through use of the ++ and -- operators.

A variable shall be definitely assigned (§10.4) before its value can be obtained.

As described in the following subclauses, variables are either initially assigned or initially unassigned. An initially assigned variable has a well-defined initial value and is always considered definitely assigned. An initially unassigned variable has no initial value. For an initially unassigned variable to be considered definitely assigned at a certain location, an assignment to the variable shall occur in every possible execution path leading to that location.

### 10.2 Variable categories

### 10.2.1 General

C# defines seven categories of variables: static variables, instance variables, array elements, value parameters, reference parameters, output parameters, and local variables. The subclauses that follow describe each of these categories.

[Example: In the following code

```
class A
{
    public static int x;
    int y;
    void F(int[] v, int a, ref int b, out int c) {
        int i = 1;
        c = a + b++;
    }
}
```

x is a static variable, y is an instance variable, v[0] is an array element, a is a value parameter, b is a reference parameter, c is an output parameter, and i is a local variable. end example

### 10.2.2 Static variables

A field declared with the static modifier is called a static variable. A static variable comes into existence before execution of the static constructor (§15.12) for its containing type, and ceases to exist when the associated application domain ceases to exist.

The initial value of a static variable is the default value (§10.3) of the variable's type.

For the purposes of definite assignment checking, a static variable is considered initially assigned.

### 10.2.3 Instance variables

### 10.2.3.1 General

A field declared without the static modifier is called an instance variable.
