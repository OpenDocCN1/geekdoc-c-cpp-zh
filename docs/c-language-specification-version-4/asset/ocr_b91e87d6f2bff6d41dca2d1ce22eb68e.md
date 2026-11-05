The value of a local variable is obtained in an expression using a simple-name (§7.6.2), and the value of a local variable is modified using an assignment (§7.17). A local variable must be definitely assigned (§5.3) at each location where its value is obtained.

The scope of a local variable declared in a local-variable-declaration is the block in which the declaration occurs. It is an error to refer to a local variable in a textual position that precedes the local-variable-declarator of the local variable. Within the scope of a local variable, it is a compile-time error to declare another local variable or constant with the same name.

A local variable declaration that declares multiple variables is equivalent to multiple declarations of single variables with the same type. Furthermore, a variable initializer in a local variable declaration corresponds exactly to an assignment statement that is inserted immediately after the declaration.

The example

```
void F() {
    int x = 1, y, z = x * 2;
}
```

corresponds exactly to

```
void F() {
    int x; x = 1;
    int y;
    int z; z = x * 2;
}
```

In an implicitly typed local variable declaration, the type of the local variable being declared is taken to be the same as the type of the expression used to initialize the variable. For example:

```
var i = 5;
var s = "Hello";
var d = 1.0;
var numbers = new int[] {1, 2, 3};
var orders = new Dictionary<int,Order>();
```

The implicitly typed local variable declarations above are precisely equivalent to the following explicitly typed declarations:

```
int i = 5;
string s = "Hello";
double d = 1.0;
int[] numbers = new int[] {1, 2, 3};
Dictionary<int,Order> orders = new Dictionary<int,Order>();
```

# 8.5.2 Local constant declarations

A local-constant-declaration declares one or more local constants.

```
local-constant-declaration:
    const type constant-declarators

constant-declarators:
    constant-declarator
    constant-declarators , constant-declarator

constant-declarator:
    identifier = constant-expression
```

The type of a local-constant-declaration specifies the type of the constants introduced by the declaration. The type is followed by a list of constant-declarators, each of which introduces a new constant. A constant-declarator consists of an identifier that names the constant, followed by an "=" token, followed by a constant-expression (§7.19) that gives the value of the constant.