
- Otherwise, the simple_name is undefined and a compile-time error occurs.

## 11.7.5 Parenthesized expressions

A parenthesized_expression consists of an expression enclosed in parentheses.

```
parenthesized_expression
  : '(' expression ')'
  ;
```

A parenthesized_expression is evaluated by evaluating the expression within the parentheses. If the expression within the parentheses denotes a namespace or type, a compile-time error occurs. Otherwise, the result of the parenthesized_expression is the result of the evaluation of the contained expression.

## 11.7.6 Member access

### 11.7.6.1 General

A member_access consists of a primary_expression, a predefined_type, or a qualified_alias_member, followed by a "." token, followed by an identifier, optionally followed by a type_argument_list.

```
member_access
  : primary_expression '.' identifier type_argument_list?
  | predefined_type '.' identifier type_argument_list?
  | qualified_alias_member '.' identifier type_argument_list?
  ;

predefined_type
  : 'bool'  | 'byte'  | 'char'  | 'decimal' | 'double' | 'float' | 'int' |
  'long'   | 'object' | 'sbyte' | 'short' | 'string' | 'uint'  | 'ulong' | 'ushort'
  ;
```

The qualified_alias_member production is defined in §13.8.

A member_access is either of the form E.I or of the form E.I<A1, ..., Ak>, where E is a primary_expression, predefined_type or qualified_alias_member, I is a single identifier, and <A1, ..., Ak> is an optional type_argument_list. When no type_argument_list is specified, consider k to be zero.

A member_access with a primary_expression of type dynamic is dynamically bound (§11.3.3). In this case, the compiler classifies the member access as a property access of type dynamic. The rules below to determine the meaning of the member_access are then applied at run-time, using the run-time type instead of the compile-time type of the primary_expression. If this run-time classification leads to a method group, then the member access shall be the primary_expression of an invocation_expression.

The member_access is evaluated and classified as follows:

- If E is a namespace and E contains a nested namespace with name I, then the result is that namespace.
- Otherwise, if E is a namespace and E contains an accessible type having name I and K type parameters, then the result is that type constructed with the given type arguments.
- If E is classified as a type, if E is not a type parameter, and if a member lookup (§11.5) of I in E with K type parameters produces a match, then E.I is evaluated and classified as follows: Note: When the result of such a member lookup is a method group and K is zero, the method group can contain methods having type parameters. This allows such methods to be considered for type argument inferencing. end note
- If I identifies a type, then the result is that type constructed with any given type arguments.
- If I identifies one or more methods, then the result is a method group with no associated instance expression.
- If I identifies a static property, then the result is a property access with no associated instance expression.
- If I identifies a static field:
  - If the field is readonly and the reference occurs outside the static constructor of the class or struct in which the field is declared, then the result is a value, namely the value of the static field I in E.
  - Otherwise, the result is a variable, namely the static field I in E.
- If I identifies a static event:
  - If the reference occurs within the class or struct in which the event is declared, and the event was declared without event_accessor_declarations (§14.8.1), then E.I is processed exactly as if I were a static field.
  - Otherwise, the result is an event access with no associated instance expression.
- If I identifies a constant, then the result is a value, namely the value of that constant.
- If I identifies an enumeration member, then the result is a value, namely the value of that enumeration member.
- Otherwise, E.I is invalid member reference, and a compile-time error occurs.
- If E is a property access, indexer access, variable, or value, the type of which is T, and a member lookup (§11.5) of I in T with K type arguments produces a match, then E.I is evaluated and classified as follows:
  - First, if E is a property or indexer access, then the value of the property or indexer access is obtained (§11.2.2) and E is reclassified as a value.
  - If I identifies one or more methods, then the result is a method group with an associated instance expression of E.
  - If I identifies an instance property, then the result is a property access with an associated instance expression of E and an associated type that is the type of the property. If T is a class type, the associated type is picked from the first declaration or override of the property found when starting with T, and searching through its base classes.
  - If T is a class_type and I identifies an instance field of that class_type:
    - If the value of E is null, then a System.NullReferenceException is thrown.
    - Otherwise, if the field is readonly and the reference occurs outside an instance constructor of the class in which the field is declared, then the result is a value, namely the value of the field I in the object referenced by E.
    - Otherwise, the result is a variable, namely the field I in the object referenced by E.
  - If T is a struct_type and I identifies an instance field of that struct_type:
    - If E is a value, or if the field is readonly and the reference occurs outside an instance constructor of the struct in which the field is declared, then the result is a value, namely the value of the field I in the struct instance given by E.
    - Otherwise, the result is a variable, namely the field I in the struct instance given by E.
  - If I identifies an instance event:
    - If the reference occurs within the class or struct in which the event is declared, and the event was declared without event_accessor_declarations (§14.8.1), and the reference does not occur as the left-hand side of a += or -= operator, then E.I is processed exactly as if I was an instance field.
    - Otherwise, the result is an event access with an associated instance expression of E.
- Otherwise, an attempt is made to process E.I as an extension method invocation (§11.7.8.3). If this fails, E.I is an invalid member reference, and a binding-time error occurs.

### 11.7.6.2 Identical simple names and type names

In a member access of the form E.I, if E is a single identifier, and if the meaning of E as a simple_name (§11.7.4) is a constant, field, property, local variable, or parameter with the same type as the meaning of E as a type_name (§7.8.1), then both possible meanings of E are permitted. The member lookup of E.I is never ambiguous, since I shall necessarily be a member of the type E in both cases. In other words, the rule simply permits access to the static members and nested types of E where a compile-time error would otherwise have occurred.

*Example:*

```csharp
struct Color
{
    public static readonly Color White = new Color(...);
    public static readonly Color Black = new Color(...);
    public Color Complement() {...}
}

class A
{
    public Color Color;            // Field Color of type Color

    void F()
    {
        Color = Color.Black;       // Refers to Color.Black static member
        Color = Color.Complement(); // Invokes Complement() on Color fld
    }

    static void G()
    {
        Color c = Color.White;     // Refers to Color.White static member
    }
}
```

Within the A class, those occurrences of the Color identifier that reference the Color type are delimited by **, and those that reference the Color field are not.

*end example*

## 11.7.7 Null Conditional Member Access

A *null_conditional_member_access* is a conditional version of *member_access* (§11.7.6) and it is a binding time error if the result type is *void*. For a null conditional expression where the result type may be *void* see (§11.7.9).

A *null_conditional_member_access* consists of a *primary_expression* followed by the two tokens "?" and ".", followed by an *identifier* with an optional *type_argument_list*, followed by zero or more *dependent_accesses*.

```
null_conditional_member_access
: primary_expression '?' '.' identifier type_argument_list? dependent_access*
;

dependent_access
: '.' identifier type_argument_list?    // member access
| '[' argument_list ']'    // element access
| '(' argument_list? ')'    // invocation
;

null_conditional_projection_initializer
: primary_expression '?' '.' identifier type_argument_list?
;
```

A *null_conditional_member_access* expression E is of the form P ?. A. Let T be the type of the expression P. A. The meaning of E is determined as follows:

- If T is a type parameter that is not known to be a reference type or a non-nullable value type, a compile-time error occurs.
- If T is a non-nullable value type, then the type of E is T?, and the meaning of E is the same as the meaning of:

  `((object)P == null) ? (T?)null : P.A`

  Except that P is evaluated only once.
- Otherwise the type of E is T, and the meaning of E is the same as the meaning of:

  `((object)P == null) ? null : P.A`

  Except that P is evaluated only once.

*Note:* In an expression of the form:

P ?. A₀ ?. A₁

then if P evaluates to *null* neither A₀ or A₁ are evaluated. The same is true if an expression is a sequence of *null_conditional_member_access* or *null_conditional_element_access* §11.7.11 operations.
*end note*

A *null_conditional_projection_initializer* is a restriction of *null_conditional_member_access* and has the same semantics. It only occurs as a projection initializer in an anonymous object creation expression (§11.7.15.7).

## 11.7.8 Invocation expressions

### 11.7.8.1 General

An *invocation_expression* is used to invoke a method.
