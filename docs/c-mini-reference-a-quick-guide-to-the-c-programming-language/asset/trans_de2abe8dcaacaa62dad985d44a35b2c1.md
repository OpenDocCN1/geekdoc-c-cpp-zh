
The above statement is equivalent to the following two declarations:

```
const TYPE NAME1 = EXP1 ;
const TYPE NAME2 = EXP2 ;
```

The scope of a local constant is the block in which the declaration occurs, similar to local variables. Within the scope of a local constant, it is a compile-time error to declare another local variable or constant with the same name.

## 7. 变量

变量表示存储位置。每个变量都有一个类型，该类型决定了可以存储在变量中的值。

### 7.1. 变量类别

变量属于以下几个不同的类别：

- 局部变量，
- 静态变量，
- 实例变量，以及
- 数组元素。

此外，函数参数也是变量。

### 局部变量

局部变量可以在块中通过局部变量声明来声明。这样声明的局部变量不会自动初始化，因此没有初始值。

### 静态变量

使用 static 修饰符声明的字段是静态变量。静态变量的初始值是其类型的默认值。

### 实例变量

非静态字段是实例变量。类（或 record 或 struct）实例变量的初始值是变量类型的默认值。

### 数组元素

数组中每个元素的初始值都是数组元素类型的默认值。

### 7.2. 局部变量声明

### 7.2.1. 局部变量

局部变量声明声明一个或多个局部变量，类似于局部常量

```
TYPE NAME ;
TYPE NAME1 , NAME2 ;
```

①
如所述，我们在本书中使用这种 somewhat 不寻常的记法来表示 C# 语法。TYPE 和 NAME 分别需要在实际语句中替换为正确的类型和有效的变量名。语句以分号结束

②
可以在一个语句中声明多个具有相同类型的变量。此特定示例仅包含两个变量，但它说明了变量之间用逗号分隔

变量可以带初始化器声明。

```
TYPE NAME = EXPR ;
TYPE NAME1 = EXPR1 , NAME2 = EXPR2 ;
```

当所有变量都有初始化器时，可以省略显式的类型名而使用 var。例如，

```
var NAME = EXPR;
var NAME1 = EXPR1, NAME2 = EXPR2;
```

标识符 var 在局部变量声明的上下文中是一个上下文关键字。隐式类型局部变量的类型是从关联的初始化器表达式的类型推断出来的。

丢弃变量 _ 可用作隐式声明的变量，例如，当你打算忽略表达式的结果时。丢弃变量常用于 lambda 表达式或模式匹配。以下是一个简单的示例。

```
var _ = 1 + 2;
```

### 7.2.2. Ref 局部变量

ref 局部变量用于引用使用 return 返回的值

```
ref TYPE NAME = REF_EXPRESSION ;
ref var NAME = REF_EXPRESSION ;
```

你通过在两个地方使用 ref 关键字来定义 ref 局部变量：

Before the variable declaration.

Immediately before the call to the method that returns the value by reference.

### 7.2.3. Ref readonly 局部变量

ref readonly 局部变量类似于 ref 局部变量，但它们不可写。

```
```csharp
ref readonly TYPE NAME = REF_EXPRESSION ;
ref readonly var NAME = REF_EXPRESSION ;
```
```

请注意，你不能在 C# 中声明 "readonly local" 变量（有些人可能会认为这是严重的限制，考虑到 C# 语言在各处都提供了大量对不可变性的支持）。

## 8.1. 局部函数

局部函数声明如下：

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

例如，

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

LocalAdd 局部函数使用封闭作用域的局部变量，即 DoAdditionTwice 的两个参数。

局部函数与 lambda 函数一样是闭包。局部函数修饰符可以是 async 或 unsafe 或两者兼有。

## 8.2. 静态局部函数

静态局部函数是局部函数的一种特殊形式。它们明确禁止使用或捕获封闭作用域中的局部变量、参数和 this。它们不能使用类型的实例成员。语法上，静态局部函数声明包含 static 修饰符。例如，

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

LocalAbs 局部函数不使用封闭作用域中的任何变量，因此可以声明为 static。

## 9. 形式参数

函数参数也是变量。当我们调用匿名函数或函数成员（例如，方法、构造函数、访问器或运算符）时，参数就会创建。参数可以用调用中给出的参数值进行初始化。函数参数通常按值传递。但它们可以使用 in、ref 或 out 关键字使用按引用传递语义。

### 9.1. 参数列表

形式参数列表由逗号分隔的固定参数和末尾的可选 params 数组参数组成。固定参数由以下部分组成

Optional

An optional modifier, in or ref

The parameter type,

The parameter name, followed by

An optional default argument

每个固定参数声明一个给定类型且给定名称的变量，该变量是函数体局部的。

具有默认值的固定参数称为可选参数。非可选参数需要参数。可选参数（如果有）只能放在任何必需参数之后，在可选 params 数组之前。带有 in 或 ref 修饰符的参数不能有默认值。

in 修饰符，即 in 或 ref 仅允许在非泛型、非嵌套静态类中的静态方法的第一个参数上使用。这种方法称为扩展方法。

### 9.2. 参数列表

函数或方法的调用是一个表达式。

```
EXPRESSION ( ARGUMENT_LIST )
```

EXPRESSION 应该是“可调用的”，例如方法或委托类型的值。ARGUMENT_LIST 可以为空。它或多或少遵循与参数相同的结构，并且每个给定的参数必须在参数列表中有一个对应的参数。

C# 支持两种参数语法，位置参数和命名参数。命名参数的形式为 PARAMETER_NAME: VALUE，而位置参数仅指定 VALUE。当参数在参数列表中的位置与参数列表中对应参数的位置相同时，可以使用命名或位置参数语法。否则，只能使用命名参数语法。例如，给定以下函数，

```
static void Metodo(int a = 1, char b = 'b') {
    Console.WriteLine($"a = {a}; b = {b}");
}
```

我们可以按以下任何方式调用此函数：

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
两个参数都是可选的，因此在此调用中 a:1 且 b:'b'。

②
位置与命名参数语法。这两个方法调用彼此等价，a:2 且 b:'b'。

③
此参数的位置为 0，而其对应参数的位置为 1。因此，此特定方法调用不能对该参数使用位置语法。此调用等价于 Metodo(1, b: 'c') 或 Metodo(a: 1, b: 'c')。

④
以下五个方法调用都等价，a:4 且 b:'d'。
