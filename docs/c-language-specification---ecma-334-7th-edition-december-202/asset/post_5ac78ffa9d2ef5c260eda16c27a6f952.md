
```
D3 d3 = F;    // Error – not applicable
D4 d4 = F;    // Error – not applicable in normal form
D5 d5 = F;    // Error – applicable but not compatible
}
```

The assignment to d1 implicitly converts the method group F to a value of type D1.

The assignment to d2 shows how it is possible to create a delegate to a method that has less derived (contravariant) parameter types and a more derived (covariant) return type.

The assignment to d3 shows how no conversion exists if the method is not applicable.

The assignment to d4 shows how the method must be applicable in its normal form.

The assignment to d5 shows how parameter and return types of the delegate and method are allowed to differ only for reference types.

end example

As with all other implicit and explicit conversions, the cast operator can be used to explicitly perform a particular conversion.

Example: Thus, the example

```
object obj = new EventHandler(myDialog.OkClick);
could instead be written
object obj = (EventHandler)myDialog.OkClick;
```

end example

A method group conversion can refer to a generic method, either by explicitly specifying type arguments within E, or via type inference (§12.6.3). If type inference is used, the parameter types of the delegate are used as argument types in the inference process. The return type of the delegate is not used for inference. Whether the type arguments are specified or inferred, they are part of the method group conversion process; these are the type arguments used to invoke the target method when the resulting delegate is invoked.

Example:

```
delegate int D(string s, int i);
delegate int E();

class X
{
    public static T F<T>(string s, T t) {...}
    public static T G<T>() {...}

    static void Main()
    {
        D d1 = F<int>;    // Ok, type argument given explicitly
        D d2 = F;         // Ok, int inferred as type argument
        E e1 = G<int>;    // Ok, type argument given explicitly
        E e2 = G;         // Error, cannot infer from return type
    }
}
```

end example

Method groups may influence overload resolution, and participate in type inference. See §12.6 for further details.

The run-time evaluation of a method group conversion proceeds as follows:

- If the method selected at compile-time is an instance method, or it is an extension method which is accessed as an instance method, the target object of the delegate is determined from the instance expression associated with E:
  - The instance expression is evaluated. If this evaluation causes an exception, no further steps are executed.
  - If the instance expression is of a reference_type, the value computed by the instance expression becomes the target object. If the selected method is an instance method and the target object is null, a System.NullReferenceException is thrown and no further steps are executed.
  - If the instance expression is of a value_type, a boxing operation (§10.2.9) is performed to convert the value to an object, and this object becomes the target object.
- Otherwise, the selected method is part of a static method call, and the target object of the delegate is null.
- A delegate instance of delegate type D is obtained with a reference to the method that was determined at compile-time and a reference to the target object computed above, as follows:
  - The conversion is permitted (but not required) to use an existing delegate instance that already contains these references.
  - If an existing instance was not reused, a new one is created (§20.5). If there is not enough memory available to allocate the new instance, a System.OutOfMemoryException is thrown. Otherwise the instance is initialized with the given references.

## 11. Patterns and pattern matching

### 11.1 General

A pattern is a syntactic form that can be used with the is operator (§12.12.12) and in a switch_statement (§13.8.3) to express the shape of data against which incoming data is to be compared. A pattern is tested against the expression of a switch statement, or against a relational_expression that is on the left-hand side of an is operator, each of which is referred to as a pattern input value.

### 11.2 Pattern forms

#### 11.2.1 General

A pattern may have one of the following forms:

```
pattern
  : declaration_pattern
  | constant_pattern
  | var_pattern
  ;
```

A declaration_pattern and a var_pattern can result in the declaration of a local variable.

Each pattern form defines the set of types for input values that the pattern may be applied to. A pattern P is applicable to a type T if T is among the types whose values the pattern may match. It is a compile-time error if a pattern P appears in a program to match a pattern input value (§11.1) of type T if P is not applicable to T.

Each pattern form defines the set of values for which the pattern matches the value at runtime.

#### 11.2.2 Declaration pattern

A declaration_pattern is used to test that a value has a given type and, if the test succeeds, provide the value in a variable of that type.

```
declaration_pattern
  : type simple_designation
  ;
simple_designation
  : single_variable_designation
  ;
single_variable_designation
  : identifier
  ;
```

The runtime type of the value is tested against the type in the pattern using the same rules specified in the is-type operator (§12.12.12.1). If the test succeeds, the pattern matches that value. It is a compile-time error if the type is a nullable value type (§8.3.12). This pattern form never matches a null value.

Note: The is-type expression e is T and the declaration pattern e is T _ are equivalent when T isn't a nullable type. end note

Given a pattern input value (§11.1) e, if the simple_designation is the identifier _, it denotes a discard (§9.2.9.1) and the value of e is not bound to anything. (Although a declared variable with the name _ may be in scope at that point, that named variable is not seen in this context.) If simple_designation is any other identifier, a local variable (§9.2.9) of the given type named by the given identifier is introduced. That local variable is assigned the value of the pattern input value when the pattern matches the value.

Certain combinations of static type of the pattern input value and the given type are considered incompatible and result in a compile-time error. A value of static type E is said to be pattern compatible with the type T if there exists an identity conversion, an implicit or explicit reference conversion, a boxing conversion, or an unboxing conversion from E to T, or if either E or T is an open type (§8.4.3). A declaration pattern naming a type T is applicable to every type E for which E is pattern compatible with T.

Note: The support for open types can be most useful when checking types that may be either struct or class types, and boxing is to be avoided. end Note

Example: The declaration pattern is useful for performing run-time type tests of reference types, and replaces the idiom

```
var v = expr as Type;
if (v != null) { /* code using v */ }
```

with the slightly more concise

```
if (expr is Type v) { /* code using v */ }
```

end example

It is an error if type is a nullable value type.

Example: The declaration pattern can be used to test values of nullable types: a value of type Nullable<T> (or a boxed T) matches a type pattern T2 if the value is non-null and T2 is T, or some base type or interface of T. For example, in the code fragment

```
int? x = 3;
if (x is int v) { /* code using v */ }
```

The condition of the if statement is true at runtime and the variable v holds the value 3 of type int inside the block. end example

#### 11.2.3 Constant pattern

A constant_pattern is used to test the value of a pattern input value (§11.1) against the given constant value.

```
constant_pattern
  : constant_expression
  ;
```

A constant pattern P is applicable to a type T if there is an implicit conversion from the constant expression of P to the type T.

For a constant pattern P, its converted value is

- if the pattern input value's type is an integral type or an enum type, the pattern's constant value converted to that type; otherwise
- if the pattern input value's type is the nullable version of an integral type or an enum type, the pattern's constant value converted to its underlying type; otherwise
- the value of the pattern's constant value.

Given a pattern input value e and a constant pattern P with converted value v,
