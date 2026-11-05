
> **JON SKEET** Given how easy it is to miss an empty statement when reading code, I wonder whether something larger might be useful for this relatively rare requirement. For example, the following code is legal but probably not what's intended:
> 
> ```csharp
> while (text.IndexOf("xx") != -1);
> {
>     text = text.Replace("xx", "x");
> }
> ```
> 
> The empty statement for the while loop is fairly well camouflaged. If you had to write something like "void;" when you actually wanted an empty statement, the compiler could flag "accidentally empty" statements like the previous example as errors.

> **JESSE LIBERTY** Jon's example shows why empty statements should be rare, and called out (though not necessarily with comments). The problem in his example code can be rectified by following the best practice of empty statements existing either on a line by themselves or, even better, within full braces:
> 
> ```csharp
> while (text.IndexOf("xx") != -1)
> {
>     ;
> }
> 
> {
>     text = text.Replace("xx", "x");
> }
> ```
> 
> No programmer can now miss that the while loop has an empty statement. The purpose of the next set of braces is no more (or less) ambiguous than it was, but the white space helped avoid the confusion.

Execution of an empty statement simply transfers control to the end point of the statement. Thus the end point of an empty statement is reachable if the empty statement is reachable.

An empty statement can be used when writing a while statement with a null body:

```
bool ProcessMessage() {...}
void ProcessMessages() {
    while (ProcessMessage())
        ;
}
```

Also, an empty statement can be used to declare a label just before the closing “}” of a block:

```
    void F() {
        ...
        if (done) goto exit;
        ...
        exit: ;
    }
```

## 8.4 Labeled Statements

A labeled-statement permits a statement to be prefixed by a label. Labeled statements are permitted in blocks, but are not permitted as embedded statements.

*labeled-statement:*
    *identifier* : *statement*

A labeled statement declares a label with the name given by the identifier. The scope of a label is the whole block in which the label is declared, including any nested blocks. It is a compile-time error for two labels with the same name to have overlapping scopes.

A label can be referenced from goto statements (§8.9.3) within the scope of the label. This means that goto statements can transfer control within blocks and out of blocks, but never into blocks.

Labels have their own declaration space and do not interfere with other identifiers. The example

```
    int F(int x) {
        if (x >= 0) goto x;
        x = -x;
    x: return x;
    }
```

is valid and uses the name x as both a parameter and a label.

Execution of a labeled statement corresponds exactly to execution of the statement following the label.

In addition to the reachability provided by normal flow of control, a labeled statement is reachable if the label is referenced by a reachable goto statement. (Exception: If a goto statement is inside a try that includes a finally block, and the labeled statement is outside the try, and the end point of the finally block is unreachable, then the labeled statement is not reachable from that goto statement.)

> ERIC LIPPERT For example, the finally block might always throw an exception, in which case there would be a reachable goto targeting a potentially unreachable label.

> PETER SESTOFT See also the annotations in the discussion of the goto statement in §8.9.3.

## 8.5 Declaration Statements

A declaration-statement declares a local variable or constant. Declaration statements are permitted in blocks, but are not permitted as embedded statements.

```
declaration-statement:
  local-variable-declaration ;
  local-constant-declaration ;
```

### 8.5.1 Local Variable Declarations

A local-variable-declaration declares one or more local variables.

```
local-variable-declaration:
  local-variable-type local-variable-declarators
```

```
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

In the context of a local variable declaration, the identifier var acts as a contextual keyword (§2.4.3). When the local-variable-type is specified as var and no type named var is in scope, the declaration is an implicitly typed local variable declaration, whose type is inferred from the type of the associated initializer expression. Implicitly typed local variable declarations are subject to the following restrictions:

- The local-variable-declaration cannot include multiple local-variable-declarators.
- The local-variable-declarator must include a local-variable-initializer.
- The local-variable-initializer must be an expression.
- The initializer expression must have a compile-time type.
- The initializer expression cannot refer to the declared variable itself.

> **ERIC LIPPERT** In an early design for this feature, it was legal to have multiple declarators.
> 
> ```
> var a = 1, b = 2.5;
> ```
> 
> When C# developers were shown this code, roughly half said that it should have the same semantics as
> 
> ```
> double a = 1, b = 2.5;
> ```
> 
> The other half said that it should have the same semantics as
> 
> ```
> int a = 1; double b = 2.5;
> ```
> 
> Both sides thought that their interpretation was the “obviously correct” one.
> 
> When faced with a syntax that admits two incompatible “obviously correct” interpretations, often the best thing to do is to disallow the syntax entirely rather than to breed confusion.

> **CHRIS SELLS** I think multiple variable declarations in the same statement just to reuse the type name should be illegal, too.

> **ERIC LIPPERT** This constraint stands in contrast to an explicitly typed local variable declaration, which does permit an initializer to reference itself.
> 
> For example, int j = M(out j); is strange, but legal. If this expression were var j = M(out j), then overload resolution could not determine the type returned by M, and hence the type of j, until the type of the argument was known. Of course, the type of the argument is exactly what we are trying to determine.
> 
> Rather than attempting to solve this “chicken and egg” problem, the language specification simply makes this case illegal.

The following are examples of incorrect implicitly typed local variable declarations:

```
var x; // Error: no initializer to infer type from
var y = { 1, 2, 3 }; // Error: array initializer not permitted
var z = null; // Error: null does not have a type
var u = x => x + 1; // Error: anonymous functions do not have a type
var v = v++; // Error: initializer cannot refer to variable itself
```

The value of a local variable is obtained in an expression using a simple-name (§7.6.2), and the value of a local variable is modified using an assignment (§7.17). A local variable must be definitely assigned (§5.3) at each location where its value is obtained.

> **CHRIS SELLS** I really love implicitly typed local variable declarations when the type is anonymous (in which case, you have to use them) or when the type of the variable is made explicit as part of the statement that initializes it, but not because you're too lazy to type!
> 
> For example:
> 
> ```
> var a = new { Name = "Bob", Age = 42 }; // Good
> var b = 1; // Good
> var v = new Person(); // Good
> var d = GetPerson(); // BAD!
> ```
> 
> The compiler is perfectly happy with d as an implicitly typed variable, but pity the poor human reader!
