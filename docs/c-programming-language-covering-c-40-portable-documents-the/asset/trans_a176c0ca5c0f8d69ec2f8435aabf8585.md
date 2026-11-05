
> **乔恩·斯基特** 考虑到阅读代码时很容易漏掉空语句，我想知道对于这种相对少见的需求，是否有更大的语法结构会更有用。例如，下面的代码合法，但很可能不是本意：
> 
> ```csharp
> while (text.IndexOf("xx") != -1);
> {
>     text = text.Replace("xx", "x");
> }
> ```
> 
> while 循环的空语句被相当好地伪装起来了。如果实际想要空语句时必须写成类似 "void;" 这样的形式，编译器就可以把像上一个例子中那样“意外为空”的语句标记为错误。

> **杰西·利伯蒂** 乔恩的例子说明了为什么空语句应当少见，并且应当被明确指出（不一定通过注释）。他示例代码中的问题可以通过遵循以下最佳实践来纠正：空语句要么单独占一行，要么——更好的是——放在完整的大括号内：
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
> 现在任何程序员都不会漏掉这个 while 循环有一个空语句。下一组大括号的用途并不比之前更含糊（也不更明确），但空白有助于避免混淆。

空语句的执行只是将控制转移到该语句的结束点。因此，如果空语句可到达，那么空语句的结束点就可到达。

在编写循环体为 null 的 while 语句时，可以使用空语句：

```
bool ProcessMessage() {...}
void ProcessMessages() {
    while (ProcessMessage())
    ;
}
```

此外，空语句可用于在块的右大括号 "}" 之前声明一个标签：

```
void F() {
...
if (done) goto exit;
...
exit: ;
}
```

## 8.4 带标签语句

带标签语句允许在语句前加一个标签。带标签语句允许出现在块中，但不允许作为嵌入语句。

```
labeled-statement:
identifier : statement
```

带标签语句声明一个标签，其名称由标识符给出。标签的作用域是声明该标签的整个块，包括任何嵌套块。两个同名标签的作用域重叠属于编译时错误。

可以从该标签作用域内的 goto 语句（§8.9.3）引用标签。这意味着 goto 语句可以在块内转移控制，也可以从块内转移到块外，但绝不能转入块内。

标签有自己的声明空间，不会与其他标识符冲突。下面的示例

```
int F(int x) {
if (x >= 0) goto x;
x = -x;
x: return x;
}
```

是有效的，并且把名称 x 同时用作参数和标签。

带标签语句的执行完全对应于执行该标签后面的语句。

除了正常控制流提供的可到达性之外，如果某个标签被可到达的 goto 语句引用，则该带标签语句也是可到达的。（例外：如果 goto 语句位于包含 finally 块的 try 中，而带标签语句位于该 try 之外，并且 finally 块的结束点不可到达，那么该带标签语句无法从该 goto 语句到达。）

> > **埃里克·利珀特** 例如，finally 块可能总是抛出异常，在这种情况下，就会有一个可到达的 goto 指向一个可能不可到达的标签。

> > **彼得·塞斯托夫特** 另请参见 §8.9.3 中 goto 语句讨论中的注释。

## 8.5 声明语句

声明语句声明局部变量或常量。声明语句允许出现在块中，但不允许作为嵌入语句。

```
declaration-statement:
  local-variable-declaration ;
  local-constant-declaration ;
```

### 8.5.1 局部变量声明

局部变量声明声明一个或多个局部变量。

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

局部变量声明的局部变量类型要么直接指定该声明引入的变量的类型，要么用标识符 var 表示应根据初始化器推断类型。类型后面跟着一个局部变量声明符列表，每个声明符引入一个新变量。局部变量声明符由一个命名该变量的标识符组成，后面可选地跟一个 "=" 标记和一个局部变量初始化器，用于给出该变量的初始值。

在局部变量声明的上下文中，标识符 var 充当上下文关键字（§2.4.3。）当局部变量类型指定为 var，并且作用域内没有名为 var 的类型时，该声明就是隐式类型局部变量声明，其类型根据关联的初始化器表达式的类型推断。隐式类型局部变量声明受以下限制：

- 局部变量声明不能包含多个局部变量声明符。
- 局部变量声明符必须包含局部变量初始化器。
- 局部变量初始化器必须是表达式。
- 初始化器表达式必须具有编译时类型。
- 初始化器表达式不能引用所声明的变量本身。

> 埃里克·利珀特 在此功能的早期设计中，允许有多个声明符。
> 
> ```
> var a = 1, b = 2.5;
> ```
> 
> 当向 C# 开发者展示这段代码时，大约一半的人说它应该具有与
> 
> ```
> double a = 1, b = 2.5;
> ```
> 
> 相同的语义。
> 
> 另一半人说它应该具有与
> 
> ```
> int a = 1; double b = 2.5;
> ```
> 
> 相同的语义。
> 
> 双方都认为自己的解释是“显然正确”的。
> 
> 当面对一种允许两种互不兼容的“显然正确”解释的语法时，最好的做法通常是完全禁止这种语法，而不是滋生混乱。

> 克里斯·塞尔斯 我认为，仅仅为了复用类型名而在同一条语句中声明多个变量，也应该是不合法的。

> **埃里克·利珀特** 这一约束与显式类型局部变量声明形成对比，后者确实允许初始化器引用自身。
> 
> 例如，int j = M(out j); 很奇怪，但合法。如果这个表达式写成 var j = M(out j)，那么重载决策在参数类型已知之前，无法确定 M 返回的类型，因而也无法确定 j 的类型。当然，参数的类型正是我们试图确定的东西。
> 
> 语言规范没有尝试解决这个“先有鸡还是先有蛋”的问题，而只是简单地将这种情况规定为不合法。

以下是错误的隐式类型局部变量声明示例：

```
var x; // Error: no initializer to infer type from
var y = {1, 2, 3}; // Error: array initializer not permitted
var z = null; // Error: null does not have a type
var u = x => x + 1; // Error: anonymous functions do not have a type
var v = v++; // Error: initializer cannot refer to variable itself
```

局部变量的值在表达式中通过简单名称（§7.6.2）获取，局部变量的值通过赋值（§7.17）修改。在获取局部变量值的每个位置，该局部变量都必须明确赋值（§5.3）。

> **克里斯·塞尔斯** 我非常喜欢在类型为匿名类型时（这种情况下必须使用它们），或者在变量的类型作为初始化该变量的语句的一部分而被显式说明时，使用隐式类型局部变量声明，但不是因为你懒得打字！
> 
> 例如：

```
var a = new { Name = "Bob", Age = 42 }; // Good
var b = 1; // Good
var v = new Person(); // Good
var d = GetPerson(); // BAD!
```

编译器完全乐于把 d 当作隐式类型变量，但请可怜可怜可怜的人类读者吧！

