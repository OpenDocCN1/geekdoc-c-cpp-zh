# 8.8.3 The for Statement

The for statement evaluates a sequence of initialization expressions and then, while a condition is true, repeatedly executes an embedded statement and evaluates a sequence of iteration expressions.

```
for-statement:
  for ( for-initializer_opt ; for-condition_opt ; for-iterator_opt ) embedded-statement

for-initializer:
  local-variable-declaration
  statement-expression-list

for-condition:
  boolean-expression

for-iterator:
  statement-expression-list

statement-expression-list:
  statement-expression
  statement-expression-list , statement-expression
```

The for-initializer, if present, consists of either a local-variable-declaration (§8.5.1) or a list of statement-expressions (§8.6) separated by commas. The scope of a local variable declared by a for-initializer starts at the local-variable-declarator for the variable and extends to the end of the embedded statement. The scope includes the for-condition and the for-iterator.

The for-condition, if present, must be a boolean-expression (§7.20).

The for-iterator, if present, consists of a list of statement-expressions (§8.6) separated by commas.

A for statement is executed as follows:

+   - If a for-initializer is present, the variable initializers or statement expressions are executed in the order they are written. This step is performed only once.
+   - If a for-condition is present, it is evaluated.
+   - If the for-condition is not present or if the evaluation yields true, control is transferred to the embedded statement. When and if control reaches the end point of the embedded statement (possibly from execution of a continue statement), the expressions of the for-iterator, if any, are evaluated in sequence, and then another iteration is performed, starting with evaluation of the for-condition in the step above.
+   - If the for-condition is present and the evaluation yields false, control is transferred to the end point of the for statement.