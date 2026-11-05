```
named_entity
  : named_entity_target ('.' identifier type_argument_list?)*
  ;

named_entity_target
  : simple_name
  | 'this'
  | 'base'
  | predefined_type
  | qualified_alias_member
  ;
```

Because nameof is not a keyword, a nameof_expression is always syntactically ambiguous with an invocation of the simple name nameof. For compatibility reasons, if a name lookup (§11.7.4) of the name nameof succeeds, the expression is treated as an invocation_expression — regardless of whether the invocation is valid. Otherwise it is a nameof_expression.

Simple name and member access lookups are performed on the named_entity at compile time, following the rules described in §11.7.4 and §11.7.6. However, where the lookup described in §11.7.4 and §11.7.6 results in an error because an instance member was found in a static context, a nameof_expression produces no such error.

It is a compile-time error for a named_entity designating a method group to have a type_argument_list. It is a compile time error for a named_entity_target to have the type dynamic.

A nameof_expression is a constant expression of type string, and has no effect at runtime. Specifically, its named_entity is not evaluated, and is ignored for the purposes of definite assignment analysis (§9.4.4.22). Its value is the last identifier of the named_entity before the optional final type_argument_list, transformed in the following way:

+   - The prefix "@", if used, is removed.
+   - Each unicode_escape_sequence is transformed into its corresponding Unicode character.
+   - Any formatting_characters are removed.

These are the same transformations applied in §6.4.3 when testing equality between identifiers.

Example: The following illustrates the results of various nameof expressions, assuming a generic type List<> declared within the System.Collections.Generic namespace:

```
using System.Collections.Generic;

using TestAlias = System.String;

class Program
{
    static void Main()
    {
        var point = (x: 3, y: 4);

        string n1 = nameof(System);                 // "System"
        string n2 = nameof(System.Collections.Generic); // "Generic"
        string n3 = nameof(point);                  // "point"
        string n4 = nameof(point.x);                // "x"
        string n5 = nameof(Program);                // "Program"
        string n6 = nameof(System.Int32);           // "Int32"
    }
}
```