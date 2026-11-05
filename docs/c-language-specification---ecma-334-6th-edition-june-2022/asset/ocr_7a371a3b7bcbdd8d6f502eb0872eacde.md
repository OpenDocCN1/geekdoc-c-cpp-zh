# 11.7.9 Null Conditional Invocation Expression

A null_conditional_invocation_expression is syntactically either a null_conditional_member_access (§11.7.7) or null_conditional_element_access (§11.7.11) where the final dependent_access is an invocation expression (§11.7.8)

A null_conditional_invocation_expression occurs within the context of a statement_expression (§12.7), anonymous_function_body (§11.16.1), or method_body (§14.6.1).

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

When E occurs as a anonymous_function_body or method_body the meaning of E depends on its classification:

+   - If E is classified as nothing then its meaning is the same as the meaning of the block:
+     { if ((object)P != null) PA; }
+     except that P is evaluated only once.
+   - Otherwise the meaning of E is the same as the meaning of the block:
+     { return E; }
+     and in turn the meaning of this block depends on whether E is syntactically equivalent to a null_conditional_member_access (§11.7.7) or null_conditional_element_access (§11.7.11).

# 11.7.10 Element access

# 11.7.10.1 General

An element_access consists of a primary_no_array_creation_expression, followed by a "[" token, followed by an argument_list, followed by a "]" token. The argument_list consists of one or more arguments, separated by commas.

```
element_access
  : primary_no_array_creation_expression '[' argument_list ']'
  ;
```

The argument_list of an element_access is not allowed to contain ref or out arguments.

An element_access is dynamically bound (§11.3.3) if at least one of the following holds:

+   - The primary_no_array_creation_expression has compile-time type dynamic.