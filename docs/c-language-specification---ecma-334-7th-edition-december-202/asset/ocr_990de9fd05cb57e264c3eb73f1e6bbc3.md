# 15.2.2.4 Referencing static class types

A namespace_or_type_name (§7.8) is permitted to reference a static class if

+   - The namespace_or_type_name is the T in a namespace_or_type_name of the form T . I, or
+   - The namespace_or_type_name is the T in a typeof_expression (§12.8.17) of the form typeof(T).

A primary_expression (§12.8) is permitted to reference a static class if

+   - The primary_expression is the E in a member_access (§12.8.7) of the form E . I.

In any other context, it is a compile-time error to reference a static class.

> *Note:* For example, it is an error for a static class to be used as a base class, a constituent type (§15.3.7) of a member, a generic type argument, or a type parameter constraint. Likewise, a static class cannot be used in an array type, a new expression, a cast expression, an is expression, an as expression, a sizeof expression, or a default value expression. end note

# 15.2.3 Type parameters

A type parameter is a simple identifier that denotes a placeholder for a type argument supplied to create a constructed type. By contrast, a type argument (§8.4.2) is the type that is substituted for the type parameter when a constructed type is created.

```
type_parameter_list
  : '<' type_parameters '>'
  ;

type_parameters
  : attributes? type_parameter
  | type_parameters ',' attributes? type_parameter
  ;
```

type_parameter is defined in §8.5.

Each type parameter in a class declaration defines a name in the declaration space (§7.3) of that class. Thus, it cannot have the same name as another type parameter of that class or a member declared in that class. A type parameter cannot have the same name as the type itself.

Two partial generic type declarations (in the same program) contribute to the same unbound generic type if they have the same fully qualified name (which includes a generic_dimension_specifier (§12.8.17) for the number of type parameters) (§7.8.3). Two such partial type declarations shall specify the same name for each type parameter, in order.

# 15.2.4 Class base specification

# 15.2.4.1 General

A class declaration may include a class_base specification, which defines the direct base class of the class and the interfaces (§18) directly implemented by the class.

```
class_base
  : ':' class_type
  | ':' interface_type_list
  | ':' class_type ',' interface_type_list
  ;
```

interface_type_list