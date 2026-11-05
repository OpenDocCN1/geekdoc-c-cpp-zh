```
| parenthesized_expression
| member_access
| null_conditional_member_access
| invocation_expression
| element_access
| null_conditional_element_access
| this_access
| base_access
| post_increment_expression
| post_decrement_expression
| object_creation_expression
| delegate_creation_expression
| anonymous_object_creation_expression
| typeof_expression
| sizeof_expression
| checked_expression
| unchecked_expression
| default_value_expression
| nameof_expression
| anonymous_method_expression
| pointer_member_access  // unsafe code support
| pointer_element_access  // unsafe code support
| ;
```

Note: These grammar rules are not ANTLR-ready as they are part of a set of mutually left-recursive rules (primary_expression, primary_no_array_creation_expression, member_access, invocation_expression, element_access, post_increment_expression, post_decrement_expression, pointer_member_access and pointer_element_access) which ANTLR does not handle. Standard techniques can be used to transform the grammar to remove the mutual left-recursion. This has not been done as not all parsing strategies require it (e.g. an LALR parser would not) and doing so would obfuscate the structure and description.

pointer_member_access (§22.6.3) and pointer_element_access (§22.6.4) are only available in unsafe code (§22).

Primary expressions are divided between array_creation_expressions and primary_no_array_creation_expressions. Treating array_creation_expression in this way, rather than listing it along with the other simple expression forms, enables the grammar to disallow potentially confusing code such as

```
object o = new int[3][1];
```

which would otherwise be interpreted as

```
object o = (new int[3])[1];
```

# 11.7.2 Literals

A primary_expression that consists of a literal (§6.4.5) is classified as a value.

# 11.7.3 Interpolated string expressions

An interpolated_string_expression consists of a $ character immediately followed by text within " characters. Within the quoted text there are zero or more interpolations delimited by { and } characters, each of which encloses an expression and optional formatting specifications.