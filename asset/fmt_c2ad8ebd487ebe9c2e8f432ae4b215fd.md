
请注意，这两个方法的正式类型描述符参数都被声明为 `TypeDescriptor` 类，这使得这些方法可以接收任何类型描述符子类的对象作为实际参数。然后这两个方法都会检查类型形式以决定要采取哪些操作。如果形式是 `NONE`，说明语义错误已经发生在其他位置，因此方法会提前退出，以防止错误消息产生连锁效应。否则，会进行进一步检查。在 `matchTypes` 中，使用 Java 的 `==` 运算符来检测两个类型描述符的对象同一性。这可以在不知道这些对象实际属于哪个类的情况下完成。然而，如果两个描述符不相同，只有当它们都是子范围且其超类型相同时，类型才会兼容。在确定两个描述符的形式为 `SUBRANGE` 后，必须将 `TypeDescriptor` 对象向下转换（downcast）为 `SubrangeDescriptor` 类，才能访问其超类型字段。幸运的是，这种向下转换在解析器中很少再出现；使用 `TypeDescriptor` 作为参数类型和返回类型，将为解析方法之间提供非常干净、高层的通信渠道。

## 8.10.3 在声明中输入类型信息

现在，只要源程序中声明了标识符，就必须输入类型信息。我们在第 8.8 节中注意到了这些位置，那里解析器输入标识符的角色信息。类型信息要么来自类型标识符（在数字或对象声明、参数规范以及记录组件声明中），要么来自类型定义。对于类型标识符，类型描述符已经可用，只需在标识符的符号表项中直接访问即可。对于类型定义，可能会创建一个新类型。因此，`typeDefinition` 方法应该将刚处理完的类型的 `TypeDescriptor` 返回给其调用者。下面的代码展示了该方法的实现，以及它在声明新类型名的 `TypeDeclaration` 方法中的使用：

```
/*
typeDeclaration = "type" identifier "is" typeDefinition ";"
*/
private void typeDeclaration(){
    accept(Token.TYPE, "'type' expected");
    SymbolEntry entry = enterId();
    entry.setRole(SymbolEntry.TYPE);
```

```java
accept(Token.IS, "'is' expected");
entry.setType(typeDefinition());        // Pick up the type
descriptor here
accept(Token.SEMI, "semicolon expected");
}

/*
typeDefinition = enumerationTypeDefinition | arrayTypeDefinition
                | range | <type>name
*/
private TypeDescriptor typeDefinition(){
    TypeDescriptor t = new TypeDescriptor();
    switch (token.code){
        case Token.ARRAY:
            t = arrayTypeDefinition();
            break;
        case Token.L_PAR:
            t = enumerationTypeDefinition();
            break;
        case Token.RANGE:
            t = range();
            break;
        case Token.ID:
            SymbolEntry entry = findId();
            acceptRole(entry, SymbolEntry.TYPE, "type name expected");
            t = entry.type;
            break;
        default: fatalError("error in type definition");
    }
    return t;
}
```

注意在 `typeDefinition` 方法中调用的每个较低层解析方法也会返回一个类型描述符，这本质上就像一根接力棒被沿着解析过程的调用树向上传递。我们看到接力棒会在某一点停住，即当类型定义只是另一个标识符时，其类型描述符被直接访问。从较低层解析方法向上传递类型描述符的策略也用于处理表达式，我们稍后将看到。

下一个例子展示了如何实际创建新类型。枚举类型由一组新的常量标识符组成。以下是 `enumerationTypeDefinition` 方法的代码：

```java
/*
enumerationTypeDefinition = "(" identifierList ")"
*/
private TypeDescriptor enumerationTypeDefinition(){
    accept(Token.L_PAR, "'(' expected");
```

```
SymbolEntry list = identifierList();
list.setRole(SymbolEntry.CONST);
EnumDescriptor t = new EnumDescriptor();
t.setIdentifiers(list);
list.setType(t);
accept(Token.R_PAR, ")' expected");
return t;
}
```

该方法现在返回一个类型描述符。方法中间新增的三行代码：

- 为枚举类型实例化一个类型描述符。
- 将其 `identifiers` 属性设置为刚解析的标识符列表。
- 将这些标识符的类型设置为刚创建的类型描述符。

数组和子范围类型定义的处理类似，留作读者练习。

## 8.10.4 检查表达式中的操作数类型

快速浏览一下 TinyAda 表达式的规则，就会了解应如何检查其类型。自上而下地看，条件必须是布尔表达式，因此很明显，`expression` 方法必须返回一个类型描述符以供检查。以下是 `condition` 方法的新代码：

```
/*
condition = <boolean>expression
*/
private void condition(){
    TypeDescriptor t = expression();
    matchTypes(t, BOOL_TYPE, "Boolean expression expected");
}
```

`expression` 方法又可能看到由布尔运算符分隔的两个或多个关系。因此，`relation` 方法也必须返回类型描述符。如果在 `expression` 方法中检测到布尔运算符，那么两个关系的类型必须分别与解析器的 `BOOL_TYPE` 变量进行匹配。

解析器的编写者必须仔细阅读表达式的每条语法规则，并在相应方法中添加合适的类型检查代码。例如，以下是 `factor` 方法的代码，其中展示了对某些操作数的检查以及相应类型描述符的返回：

/*

factor = primary [ "**" primary ] | "not" primary

*/

private TypeDescriptor factor(){

    TypeDescriptor t1;

    if (token.code == Token.NOT){

        token = scanner.nextToken();

        t1 = primary();

        matchTypes(t1, BOOL_TYPE, "Boolean expression expected");

    }

    else{

        t1 = primary();

        if (token.code == Token.EXPO){

            matchTypes(t1, INT_TYPE, "integer expression expected");

            token = scanner.nextToken();

            TypeDescriptor t2 = primary();

            matchTypes(t2, INT_TYPE, "integer expression expected");

        }

    }

    return t1;

}

此方法有以下三种返回类型描述符的选项：

+   1. `factor` 中没有运算符，因此直接将 `primary` 的第一次调用得到的类型描述符 `t1` 返回给调用者。
+   2. 运算符是前置的 `not`。则在将其与 `BOOL_TYPE` 匹配后返回类型描述符 `t1`。
+   3. 运算符是二元的 `**`。则在将其与从对 `primary` 的第二次调用得到的类型描述符 `t2` 一起匹配到 `INT_TYPE` 后返回类型描述符 `t1`。

正如你所见，每个操作数的类型都必须被检查，并且必须格外小心以确保返回正确的类型描述符。对解析表达式的其余方法的修改留给读者作为练习。

## 8.10.5 处理名称：索引组件引用和过程调用

如果过程期望至少一个参数，则 TinyAda 索引组件引用和过程调用的语法是相同的。如前面的代码段所示，方法名现在必须根据前导标识符的作用区分这两种短语。用于处理尾随短语的代码，该短语由括号表达式列表组成，现在可以拆分为两个不同的解析方法 `actualParameterPart` 和 `indexedComponent`。

方法 `actualParameterPart` 接收过程名的符号条目作为参数。该条目包含过程形式参数的信息，该信息在过程声明时更早输入。当它遍历表达式列表时，此方法应将每个表达式的类型与该位置的形式参数的类型进行匹配。此外，表达式的数量和形式参数的数量必须相同。

方法 `indexedComponent` 接收数组标识符的条目作为参数。该条目的类型描述符包含数组的索引类型和元素类型的信息，该信息在该数组类型定义时更早输入。此方法使用与我们在方法 `actualParameterPart` 中看到的匹配形式参数和实际参数类型相同的策略来匹配表达式与声明的索引类型。然而，`indexedComponent` 还必须返回一个包含数组元素类型以及数组标识符的作用的新符号条目。这将是名称方法在调用树更上层进行角色和类型分析时返回的信息。完成这两个方法以及 TinyAda 解析器中类型分析的其余代码留给读者作为练习。

## 8.10.6 完成静态语义分析

在解析期间还可以施加两种其他类型的语义限制。一个限制涉及参数模式的检查。TinyAda 有三种参数模式：仅输入（由关键字 `in` 表示）、仅输出（由关键字 `out` 表示）和输入/输出（由关键字 `in out` 表示）。这些模式用于控制信息在过程之间进出的流程。例如，只有变量或具有相同模式的参数才能作为实际参数传递，而形式参数已声明为 `out` 或 `in out`。在过程的代码内，`out` 参数不能出现在表达式中，而 `in` 参数不能成为赋值语句的目标。

另一个限制区分了静态表达式和其他表达式。静态表达式是其值可以在编译时计算的表达式。只有静态表达式才能用于数字声明和范围类型定义。我们将在后面的章节讨论这两种类型限制的执行。

## Exercises

+   8.1 将 Lisp 的动态类型灵活性与 Ada、ML、C++ 或 Java 的静态类型可靠性进行比较。尽可能多地思考支持和反对将静态类型作为程序设计辅助的论据。
+   8.2 查阅你正在使用的 C/C++ 编译器（或其他非 Java 编译器）对数据表示的实现细节，并将其与文本中给出的典型实现草图进行比较。它们有何不同？它们有何相同？
+   8.3 (a) 布尔数据类型可能具有也可能不具有顺序关系，并且可能可以也可能不可以转换为整型，这取决于语言。比较以下至少两种语言中布尔类型的处理方式，关于这两个问题：Java、C++、Ada、ML。
+   (b) 让布尔值有序有用吗？可转换为整数有用吗？

## 8.4

**(a)** 给定 C 声明

```c
struct{
    int i;
    double j;
} x, y;
struct{
    int i;
    double j;
} z;
```

赋值 `x = z` 会产生编译错误，但赋值 `x = y` 不会。为什么？

**(b)** 给出两种不同的修复方法 (a) 部分代码的方法，使 `x = z` 能工作。哪种方法更好，为什么？

## 8.5

假设我们有两个 C 数组：

```c
int x[10];
int y[10];
```

为什么赋值 `x = y` 在 C 中无法编译？声明可以修复以使赋值能工作吗？

## 8.6

给定 C/C++ 中的以下变量声明：

```c
enum { one } x;
enum { two } y;
```

赋值 `x = y` 在 C 中是可以的，但在 C++ 中会产生编译器错误。解释原因。

## 8.7

给定 C/C++ 中的以下函数变量声明：

```c
int (*f)(int);
int (*g)(int);
int (*h)(char);
```

赋值 `f = g` 在 C 和 C++ 中是可以的，但赋值 `h = g` 在 C 中会产生编译器警告，在 C++ 中会产生编译器错误。解释原因。

## 8.8

证明集合：

{emptylist} ∪ char ∪ (char × char) ∪ (char × char × char) ∪ …

是集合方程的最小解：

CharList = {emptylist} ∪ char × CharList

（参见第 8.3.5 节和练习 6.53。）

## 8.9 考虑集合方程

ℵ × char = ℵ

+   (a) 证明满足此方程的任何集合 X 必须是无限的。
+   (b) 证明满足此方程的集合的任何元素都必须包含无限多个字符。
+   (c) 此方程有最小解吗？

## 8.10 考虑以下 C 语法中的声明：

```c
struct CharTree{
    char data;
    struct CharTree left, right;
};
```

+   (a) 将 CharTree 重写为联合，类似于第 8.3.5 节的联合 CharList 声明。
+   (b) 为你在 (a) 部分的声明写一个递归集合方程。
+   (c) 描述一个集合，它是你在 (b) 部分方程的最小解。
+   (d) 证明你在 (c) 部分的集合是最小解。
+   (e) 将其重写为有效的 C 声明。

## 8.11 这里有一些 C 中的类型声明：

```c
typedef struct Rec1 * Ptr1;
typedef struct Rec2 * Ptr2;
struct Rec1{
    int data;
    Ptr2 next;
};
struct Rec2{
    double data;
    Ptr2 next;
};
```

这些应该被允许吗？被允许吗？为什么或为什么不？

## 8.12

+   (a) Ada 中子类型和派生类型有什么区别？
+   (b) 以下 Ada 声明相当于什么 C 类型声明？
+       subtype New_Int is integer;
+   (c) 以下 Ada 声明相当于什么 C 类型声明？
+       type New_Int is new integer;

8.13 在 Ada 中，等价测试（Ada 语法中的 x = y）对于所有类型都是合法的，只要 x 和 y 具有相同的类型。在 C 中，等价测试（C 语法中的 x == y）仅允许用于少数类型的变量；然而，x 和 y 的类型不必总是相同。

(a) 描述 C 比较 x == y 合法的 x 和 y 的类型。

(b) 为什么 C 语言不允许对某些类型的变量进行等价测试？

(c) 为什么 C 语言允许对某些不同类型的值进行比较？

8.14 描述 C 中条件表达式的类型正确性和推断规则：

	e1 ? e2 : e3

e2 和 e3 必须具有相同的类型吗？如果它们具有相同的类型，可以是任何类型吗？

8.15 假设我们使用了以下尝试避免使用 static_cast 来打印 true 的内部值的 C++ 代码（参见第 8.7 节末尾的代码）：

```c
union{
    int i;
    bool b;
} x;
...
x.b = true;
cout << x.i << endl;
```

为什么这是错误的？（提示：尝试在 x.b=true 之前执行赋值 x.i=20000。）

8.16 程序员经常忘记数值数据类型如 int 只是数学数系统的近似。例如，在你的系统上尝试以下两个 C 或 C++ 或 Java 中的除法，并解释结果： -2147483648 / -1; -2147483647 / -1。

8.17 本章没有提到变量的初始化问题。描述 C、Ada、ML 或其他类似语言中变量初始化的规则。特别是，程序开始运行时是否会初始化所有类型的变量？如果是，初始值是如何构造的？

8.18 这里有一些 C 语法中的类型和变量声明：

```c
typedef char* Table1;
typedef char* Table2;

Table1 x,y;
Table2 z;
Table2 w;
```

说明在以下情况下哪些变量是类型等价的：(a) 结构等价，(b) 名称等价，(c) 实际的 C 等价算法。务必指出根据手头信息模糊不清的情况。

### 8.19

给定声明

```
int x[10];
int y[5];
```

在 C 中 x 和 y 类型等价吗？

### 8.20

给定以下 C 声明：

```
const PI = 3.14159;
```

如果我们随后在几何公式中使用常数 PI（例如 `A = PI*r*r`），我们会得到错误的结果。为什么？

### 8.21

给定以下 Java 声明：

```
short i = 2;
```

Java 编译器对以下语句生成错误：

```
i = i + i;
```

为什么？
