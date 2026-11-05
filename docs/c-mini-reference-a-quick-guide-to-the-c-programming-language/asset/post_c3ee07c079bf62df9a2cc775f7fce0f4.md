
The above statement is equivalent to the following two declarations:

```
const TYPE NAME1 = EXP1 ;
const TYPE NAME2 = EXP2 ;
```

The scope of a local constant is the block in which the declaration occurs, similar to local variables. Within the scope of a local constant, it is a compile-time error to declare another local variable or constant with the same name.

## 7. Variables

Variables represent storage locations. Every variable has a type that determines what values can be stored in the variable.

### 7.1. Variable Categories

Variables belong to a few different categories:

- Local variables,
- Static variables,
- Instance variables, and
- Array elements.

In addition, function parameters are also variables.

### Local Variables

A local variable can be declared with a local variable declaration in a block. A local variable declared this way is not automatically initialized and thus has no initial value.

### Static Variables

A field declared with the static modifier is a static variable. The initial value of a static variable is the default value of its type.

### Instance Variables

A non-static field is an instance variable. The initial value of an instance variable of a class (or, record or struct) is the default value of the variable’s type.

### Array Elements

The initial value of each of the elements of an array is the default value of the type of the array elements.

### 7.2. Local Variable Declarations

### 7.2.1. Local variables

A local variable declaration declares one or more local variables, similar to a local constant

```
TYPE NAME ;
TYPE NAME1 , NAME2 ;
```

①
As indicated, we use this somewhat unusual notation to represent C# syntax in this book. TYPE and NAME need to be replaced with a proper type and a valid variable name in a real statement, respectively. The statement ends with a semicolon

②
More than one variable can be declared in one statement with the same type. This particular example only includes two variables, but it illustrates that the variables are separated by commas

Variables can be declared with initializers.

```
TYPE NAME = EXPR ;
TYPE NAME1 = EXPR1 , NAME2 = EXPR2 ;
```

When all variables have initializers, the explicit type name can be omitted in lieu of var. For example,

```
var NAME = EXPR;
var NAME1 = EXPR1, NAME2 = EXPR2;
```

The identifier var is a contextual keyword in the context of local variable declarations. The type of an implicitly typed local variable is inferred from the type of the associated initializer expression.

A discard variable _ may be used as an implicitly declared variable, for example, when you intend to ignore the result of an expression. Discard variables are often used in lambda expressions or in pattern matching. Here’s a trivial example.

```
var _ = 1 + 2;
```

### 7.2.2. Ref local variables

A ref local variable is used to refer to values returned using return

```
ref TYPE NAME = REF_EXPRESSION ;
ref var NAME = REF_EXPRESSION ;
```

You define a ref local by using the ref keyword in two places:

Before the variable declaration.

Immediately before the call to the method that returns the value by reference.

### 7.2.3. Ref readonly local variables

A ref readonly local variable is similar to a ref local variable, but they are not writeable.

```
```csharp
ref readonly TYPE NAME = REF_EXPRESSION ;
ref readonly var NAME = REF_EXPRESSION ;
```
```

Note that you cannot declare "readonly local" variables in C# (which some people might consider a serious limitation considering that the C# language provides so much support for immutability everywhere).

## 8.1. Local Functions

A local function is declared as follows:

Local function header, comprising

Optional and optional local function modifiers,

The return type or

The function name,

A type parameter in case of a generic local function,

A formal parameter list in a pair of parentheses, followed by

An optional type parameter constraint and

Local function body, comprising

A function body block, or

An expression body ending with a semicolon

For example,

```
~~~csharp
static (int, int) DoAdditionTwice(int a, int b) {
    var fstTime = LocalAdd();
    var sndTime = LocalAdd();
    return (fst, snd);

    void LocalAdd() => a + b; ①
}
~~~
```

①

The LocalAdd local function uses the local variables of the enclosing scope, namely, the two parameters of DoAdditionTwice.

Local functions are closures just like lambda functions. Local function modifiers can be either async or unsafe or both.

## 8.2. Static Local Functions

Static local functions are a special form of local functions. They are explicitly prohibited from using, or capturing, local variables, parameters, and this from the enclosing scope. They cannot use instance members of the type. Syntactically, a static local function declaration includes the static modifier. For example,

```
```
static int AbsoluteValue(int a) {
    return LocalAbs(a);
    static int LocalAbs(int x) =>
        x > 0 ? x : -x;
}
```
```

①

The LocalAbs local function does not use any variables of the enclosing scope, and hence it can be declared as static.

## 9. Formal Parameters

Function parameters are also variables. A parameter comes into existence when we invoke an anonymous function or a function member (e.g., method, constructor, accessor, or operator). Parameters may be initialized with values of the arguments given in the invocation. Function arguments are normally passed by value. But, they can use pass-by-reference semantics using the keywords in, ref, or out.

### 9.1. Parameter List

The formal parameter list consists of comma-separated fixed parameters and an optional params array parameter at the end. A fixed parameter consists of

Optional

An optional modifier, in or ref

The parameter type,

The parameter name, followed by

An optional default argument

Each fixed parameter declares a variable of the given type with the given name, which is local to the function body.

A fixed parameter with a default value is known as optional parameter. Arguments are required for non-optional parameters. Optional parameters, if any, can only be placed after any required parameters, before the optional params array. Parameters with in or ref modifiers cannot have default arguments.

The in modifiers, namely, in or ref are only allowed on the first parameter of a static method in a non-generic, non-nested static class. Such a method is called an extension method.

### 9.2. Argument List

Invocation of a function or method is an expression.

```
EXPRESSION ( ARGUMENT_LIST )
```

EXPRESSION should be "callable", e.g., a method or a value of a delegate type. ARGUMENT_LIST can be empty. It follows more or less the same structure as the parameter and each given argument must have a corresponding parameter in the parameter list.

C# supports two kinds of argument syntax, positional arguments and named arguments. A named argument has a form PARAMETER_NAME: VALUE whereas only VALUE is specified for a positional argument. When an argument is in the same position in the argument list as the corresponding parameter in the parameter list, it can use either named or positional argument syntax. Otherwise, only the named argument syntax is allowed. For example, given the following function,

```
static void Metodo(int a = 1, char b = 'b') {
    Console.WriteLine($"a = {a}; b = {b}");
}
```

We can call this function in any of the following ways:

```
Metodo();
```

```
Metodo(2);
Metodo(a: 2);
```

```
Metodo(b: 'c');
```

```
Metodo(4, 'd');
Metodo(a: 4, 'd');
Metodo(4, b: 'd');
Metodo(a: 4, b: 'a');
Metodo(b: 'a', a: 4);
```

①
Both parameters are optional, hence a:1 and b:'b' in this call.

②
Positional vs named argument syntax. These two method invocations are equivalent to each other, with a:2 and b:'b'.

③
The position of this argument is 0 whereas the position of its corresponding parameter is 1. Hence, this particular method call cannot use the positional syntax for the parameter. This call is equivalent to Metodo(1, b: 'c') or Metodo(a: 1, b: 'c').

④
All following five method calls are equivalent, with a:4 and b:'d'.
