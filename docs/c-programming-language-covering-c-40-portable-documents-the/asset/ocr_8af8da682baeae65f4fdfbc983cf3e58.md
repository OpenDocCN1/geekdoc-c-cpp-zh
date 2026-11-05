```
enum Circular
{
    A = B,
    B
}
```

results in a compile-time error because the declarations of A and B are circular. A depends on B explicitly, and B depends on A implicitly.

Enum members are named and scoped in a manner exactly analogous to fields within classes. The scope of an enum member is the body of its containing enum type. Within that scope, enum members can be referred to by their simple names. From all other code, the name of an enum member must be qualified with the name of its enum type. Enum members do not have any declared accessibility—an enum member is accessible if its containing enum type is accessible.

# 14.4 The System.Enum Type

The type System.Enum is the abstract base class of all enum types (this is distinct and different from the underlying type of the enum type), and the members inherited from System.Enum are available in any enum type. A boxing conversion (§4.3.1) exists from any enum type to System.Enum, and an unboxing conversion (§4.3.2) exists from System.Enum to any enum type.

Note that System.Enum is not itself an enum-type. Rather, it is a class-type from which all enum-types are derived. The type System.Enum inherits from the type System.ValueType (§4.1.1), which in turn inherits from type object. At runtime, a value of type System.Enum can be null or a reference to a boxed value of any enum type.

# 14.5 Enum Values and Operations

Each enum type defines a distinct type; an explicit enumeration conversion (§6.2.2) is required to convert between an enum type and an integral type, or between two enum types. The set of values that an enum type can take on is not limited by its enum members. In particular, any value of the underlying type of an enum can be cast to the enum type, and is a distinct valid value of that enum type.

Enum members have the type of their containing enum type (except within other enum member initializers; see §14.3). The value of an enum member declared in enum type E with associated value v is (E)v.