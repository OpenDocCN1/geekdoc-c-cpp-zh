In addition to the reachability provided by normal flow of control, a labeled statement is reachable if the label is referenced by a reachable goto statement, unless the goto statement is inside the try block or a catch block of a try-statement that includes a finally block whose end point is unreachable, and the labeled statement is outside the try-statement.

# 13.6 Declaration statements

# 13.6.1 General

A declaration-statement declares a local variable or constant. Declaration statements are permitted in blocks, but are not permitted as embedded statements.

```
declaration-statement:
    local-variable-declaration ;
    local-constant-declaration ;
```

# 13.6.2 Local variable declarations

A local-variable-declaration declares one or more local variables.

```
local-variable-declaration:
    local-variable-type local-variable-declarators

local-variable-type:
    type
    var

local-variable-declarators:
    local-variable-declarator
    local-variable-declarators , local-variable-declarator

local-variable-declarator:
    identifier
    identifier = local-variable-initializer

local-variable-initializer:
    expression
    array-initializer
```

The local-variable-type of a local-variable-declaration either directly specifies the type of the variables introduced by the declaration, or indicates with the identifier var that the type should be inferred based on an initializer. The type is followed by a list of local-variable-declarators, each of which introduces a new variable. A local-variable-declarator consists of an identifier that names the variable, optionally followed by an “=” token and a local-variable-initializer that gives the initial value of the variable.

In the context of a local variable declaration, the identifier var acts as a contextual keyword (§7.4.4).When the local-variable-type is specified as var and no type named var is in scope, the declaration is an implicitly typed local variable declaration, whose type is inferred from the type of the associated initializer expression. Implicitly typed local variable declarations are subject to the following restrictions:

+   - The local-variable-declaration cannot include multiple local-variable-declarators.
+   - The local-variable-declarator shall include a local-variable-initializer.
+   - The local-variable-initializer shall be an expression.
+   - The initializer expression shall have a compile-time type.
+   - The initializer expression cannot refer to the declared variable itself

[Example: The following are incorrect implicitly typed local variable declarations: