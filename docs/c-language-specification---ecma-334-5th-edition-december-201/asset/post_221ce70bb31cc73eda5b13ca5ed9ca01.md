
```
enum-modifier:
  new
  public
  protected
  internal
  private
```

It is a compile-time error for the same modifier to appear multiple times in an enum declaration.

The modifiers of an enum declaration have the same meaning as those of a class declaration (§15.2.2). However, the abstract, and sealed, and static modifiers are not permitted in an enum declaration. Enums cannot be abstract and do not permit derivation.

## 19.4 Enum members

The body of an enum type declaration defines zero or more enum members, which are the named constants of the enum type. No two enum members can have the same name.

```
enum-member-declarations:
  enum-member-declaration
  enum-member-declarations , enum-member-declaration

enum-member-declaration:
  attributes_opt identifier
  attributes_opt identifier = constant-expression
```

Each enum member has an associated constant value. The type of this value is the underlying type for the containing enum. The constant value for each enum member shall be in the range of the underlying type for the enum. [Example: The example

```
enum Color: uint
{
    Red = -1,
    Green = -2,
    Blue = -3
}
```

results in a compile-time error because the constant values -1, -2, and -3 are not in the range of the underlying integral type uint. end example]

Multiple enum members may share the same associated value. [Example: The example

```
enum Color
{
    Red,
    Green,
    Blue,
    Max = Blue
}
```

shows an enum in which two enum members—Blue and Max—have the same associated value. end example]

The associated value of an enum member is assigned either implicitly or explicitly. If the declaration of the enum member has a constant-expression initializer, the value of that constant expression, implicitly converted to the underlying type of the enum, is the associated value of the enum member. If the declaration of the enum member has no initializer, its associated value is set implicitly, as follows:

- If the enum member is the first enum member declared in the enum type, its associated value is zero.
- Otherwise, the associated value of the enum member is obtained by increasing the associated value of the textually preceding enum member by one. This increased value shall be within the range of values that can be represented by the underlying type, otherwise a compile-time error occurs.

[Example: The example

```
using System;
enum Color
{
    Red,
    Green = 10,
    Blue
}
class Test
{
    static void Main() {
        Console.WriteLine(StringFromColor((Color.Red)));
        Console.WriteLine(StringFromColor((Color.Green)));
        Console.WriteLine(StringFromColor((Color.Blue)));
    }
    static string StringFromColor(Color c) {
        switch (c) {
            case Color.Red:
                return String.Format("Red = {0}", (int) c);
            case Color.Green:
                return String.Format("Green = {0}", (int) c);
            case Color.Blue:
                return String.Format("Blue = {0}", (int) c);
            default:
                return "Invalid color";
        }
    }
}
```

prints out the enum member names and their associated values. The output is:

```
Red = 0
Green = 10
Blue = 11
```

for the following reasons:

- the enum member Red is automatically assigned the value zero (since it has no initializer and is the first enum member);
- the enum member Green is explicitly given the value 10;
- and the enum member Blue is automatically assigned the value one greater than the member that textually precedes it.

end example]

The associated value of an enum member may not, directly or indirectly, use the value of its own associated enum member. Other than this circularity restriction, enum member initializers may freely refer to other enum member initializers, regardless of their textual position. Within an enum member initializer, values of other enum members are always treated as having the type of their underlying type, so that casts are not necessary when referring to other enum members.

[Example: The example

```
enum Circular
{
    A = B,
    B
}
```

results in a compile-time error because the declarations of A and B are circular. A depends on B explicitly, and B depends on A implicitly. end example]

Enum members are named and scoped in a manner exactly analogous to fields within classes. The scope of an enum member is the body of its containing enum type. Within that scope, enum members can be referred to by their simple name. From all other code, the name of an enum member shall be qualified with the name of its enum type. Enum members do not have any declared accessibility—an enum member is accessible if its containing enum type is accessible.

## 19.5 The System.Enum type

The type System.Enum is the abstract base class of all enum types (this is distinct and different from the underlying type of the enum type), and the members inherited from System.Enum are available in any enum type. A boxing conversion (§11.2.8) exists from any enum type to System.Enum, and an unboxing conversion (§11.3.6) exists from System.Enum to any enum type.

Note that System.Enum is not itself an enum-type. Rather, it is a class-type from which all enum-types are derived. The type System.Enum inherits from the type System.ValueType (§9.3.2), which, in turn, inherits from type object. At run-time, a value of type System.Enum can be null or a reference to a boxed value of any enum type.

## 19.6 Enum values and operations

Each enum type defines a distinct type; an explicit enumeration conversion (§11.3.3) is required to convert between an enum type and an integral type, or between two enum types. The set of values of the enum type is the same as the set of values of the underlying type and is not restricted to the values of the named constants. Any value of the underlying type of an enum can be cast to the enum type, and is a distinct valid value of that enum type.

Enum members have the type of their containing enum type (except within other enum member initializers: see §19.4). The value of an enum member declared in enum type E with associated value v is (E)v.

The following operators can be used on values of enum types:

- ==, !=, <, >, <=, >= (§12.11.6)
- binary + (§12.9.5)
- binary - (§12.9.6)
- ^, &, | (§12.12.3)
- ~ (§12.8.5)
- ++, -- (§12.7.10 and §12.8.6)
- sizeof (§23.6.9)

Every enum type automatically derives from the class System.Enum (which, in turn, derives from System.ValueType and object). Thus, inherited methods and properties of this class can be used on values of an enum type.

## 20. Delegates

### 20.1 General

A delegate declaration defines a class that is derived from the class System.Delegate. A delegate instance encapsulates an invocation list, which is a list of one or more methods, each of which is referred to as a callable entity. For instance methods, a callable entity consists of an instance and a method on that instance. For static methods, a callable entity consists of just a method. Invoking a delegate instance with an appropriate set of arguments causes each of the delegate's callable entities to be invoked with the given set of arguments.

> [Note: An interesting and useful property of a delegate instance is that it does not know or care about the classes of the methods it encapsulates; all that matters is that those methods be compatible (§20.4) with the delegate's type. This makes delegates perfectly suited for "anonymous" invocation. end note]

### 20.2 Delegate declarations

A delegate-declaration is a type-declaration (§14.7) that declares a new delegate type.

```
delegate-declaration:
    attributes_opt delegate-modifiers_opt delegate return-type
    identifier variant-type-parameter-list_opt
    ( formal-parameter-list_opt ) type-parameter-constraints-clauses_opt ;
```

```
delegate-modifiers:
    delegate-modifier
    delegate-modifiers delegate-modifier
```

delegate-modifier:
- new
- public
- protected
- internal
- private

It is a compile-time error for the same modifier to appear multiple times in a delegate declaration.

A delegate declaration shall not supply a type-parameter-constraints-clauses unless it also supplies a variant-type-parameter-list.

A delegate declaration that supplies a variant-type-parameter-list is a generic delegate declaration.

The new modifier is only permitted on delegates declared within another type, in which case it specifies that such a delegate hides an inherited member by the same name, as described in §15.3.5.

The public, protected, internal, and private modifiers control the accessibility of the delegate type. Depending on the context in which the delegate declaration occurs, some of these modifiers might not be permitted (§8.5.2).

The delegate's type name is identifier.

The optional formal-parameter-list specifies the parameters of the delegate, and return-type indicates the return type of the delegate.

The optional variant-type-parameter-list (§18.2.3) specifies the type parameters to the delegate itself.

The return type of a delegate type shall be either void, or output-safe (§18.2.3.2).
