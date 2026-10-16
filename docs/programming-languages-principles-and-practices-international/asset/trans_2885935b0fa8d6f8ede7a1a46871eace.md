

任何命名的封闭作用域都可以通过类似记录结构访问的点记法来访问，因此上述 C++ 行为也可以在 Ada 中实现，如下所示：

```
B1: declare
    a: integer;
    y: boolean;
begin
    a := 2;
    y := false;
    B2: declare
        a, b: integer; -- local a now hides a in B1
    begin
        if y then a := B1.a; -- select the a in B1
        else b := B1.a;
        end if;
    end B2;
    ...
end B1;
```

这在 Ada 中称为选择可见性。

C++ 还使用作用域解析运算符从“外部”进入类的作用域以提供缺失的定义，因为 C++ 在类声明中只需要声明，而不需要完整的定义：

```
/* C++ example of class declaration similar to previous Java example */
class IntWithGcd{

    public:
    /* local declaration of intValue function - code for intValue() is not provided */
    int intValue();

    int gcd ( int v ); /* local declaration of gcd */

    private:
    int value; /* local declaration of value member */
};

/* use scope resolution to give actual definition of intValue */
int IntWithGcd::intValue(){
    return value;
}
```

在此思路下的另一个例子是声明中额外的关键字修饰符如何改变声明的作用域。在 C 中，全局变量声明实际上可以通过 extern 关键字跨文件访问：

File 1:

```
extern int x; /* uses x from somewhere else */
---
```

File 2:

```
int x; /* a global x that can be accessed by other files */
---
```

现在如果 File 1 和 File 2 分别编译然后链接在一起，File 1 中的外部 x 将由链接器与 File 2 中提供的 x 标识。另一方面，如果在编写 File 2 时，程序员希望将 x 的作用域限制在 File 2 本身，并且从而防止外部引用，程序员可以使用 static 关键字：

File 2:

```
/* a global x that can only be seen within this file */
static int x;
---
```

现在尝试将 File 1 与 File 2 链接将导致错误：对 x 的未定义引用。这是一种原始版本的范围修改访问控制，类和模块提供了这种控制，在第 5 章和第 11 章中详细讨论。

作用域规则还必须以递归或自引用声明在有意义时能够实现的方式构建。由于函数必须允许递归，这意味着函数名称的声明在进入函数体块之前就开始生效：

```
int factorial (int n){
    /* scope of factorial begins here */
    /* factorial can be called here */
    ---
}
```

另一方面，递归变量声明通常没有意义：

```
int x = x + 1; /* ??? */
```

此声明很可能是一个错误，事实上 Java 和 Ada 将其标记为错误，即使 x 的作用域从 = 号开始。在 Ada 中，这是因为变量声明中的自引用被明确禁止。在 Java 中，这是由于自引用被标记为未初始化的使用。C 和 C++，然而，如果 x 是局部变量⁵，则不会将此标记为错误，而只是对 x 的（可能随机的）未初始化值加一。

⁵ C 和 C++ 中的全局变量不能有此类初始化表达式，因为它们的初始值必须是编译时量；参见第 7.6.2 节。

一种特殊的范围情况，与递归相关，发生在面向对象语言中的类声明中。类声明内部的局部声明通常具有向后延伸以包含整个类的范围（从而部分暂停声明在使用前规则）。例如，在之前的 Java 中的 **IntWithGcd** 示例中，局部数据值在类声明中被引用，甚至在它被定义之前。此规则存在是为了使类内部声明的顺序无关紧要。此类语言的翻译器通常必须执行两次传递来解析程序。在第一次传递中，解析器将所有声明的名称输入符号表。在第二次传递中，解析器查找对名称的每个引用，以验证是否存在声明。

符号表处理声明的方式必须对应于每个声明的作用域。因此，不同的作用域规则需要符号表有不同的行为，甚至符号表内部有不同的结构。在下一节中，我们将检查符号表如何在块结构语言中帮助分析作用域的基本方式。

## 7.3 The Symbol Table

符号表就像字典：它必须支持名称与其关联属性的插入、查找和删除⁶，表示声明中的绑定。符号可以用任意数量的数据结构实现以允许高效访问，例如哈希表和二叉搜索树。然而，在具有块结构的词法作用域语言中维护作用域信息要求声明以类似栈的方式处理。也就是说，在进入块时，处理该块的所有声明并将相应的绑定添加到符号表。然后，在退出块时，由声明提供的绑定被移除，恢复可能存在的任何先前绑定。此过程称为 **scope analysis**。在不将符号表的视图限制为任何特定数据结构的情况下，我们仍然可以图示地将符号表视为一组名称，每个名称都有一个与其关联的声明栈，使得栈顶的声明是其作用域当前处于活动状态的声明。为了说明其工作原理，请考虑图 7.6 的 C 程序。

```
```c
(1)  int x;
(2)  char y;

(3)  void p(){
(4)      double x;
(5)      ...
(6)      { int y[10];
(7)          ...
(8)      }
(9)      ...
(10) }

(11) void q(){
(12)     int y;
```
```

![](img/062750ade02e28185b1fb8e8cf6dc89e_275_0.png)

> ⁶ 删除，当然可能并不意味着从符号表中完全擦除，而只是将其标记为不再活动，因为在翻译器退出作用域后，绑定可能仍需要被重新访问。

(continued)

```
(13)   ---
(14) }

(15) main(){
(16)     char x;
(17)   ---
(18) }
```

Figure 7.6 C program demonstrating symbol table structure

该程序中的名称为 x、y、p、q 和 main，但 x 和 y 各自与三个具有不同作用域的不同声明相关联。在处理 p 的函数体开头处的变量声明之后（图 7.6 的第 5 行），符号表可以表示为图 7.7 所示。（由于 C 中所有函数定义都是全局的，我们在图 7.7 及后续图中的属性中不明确标示这一点。）

![](img/062750ade02e28185b1fb8e8cf6dc89e_276_0.png)

Figure 7.7 Symbol table structure at line 5 of Figure 7.6

在处理 p 中的嵌套块的声明后，使用 y 的局部声明（即图 7.6 的第 7 行），符号表如图所示 7.8 所示。

![](img/062750ade02e28185b1fb8e8cf6dc89e_276_1.png)

Figure 7.8 Symbol table structure at line 7 of Figure 7.6

然后，当 p 的处理完成时（图 7.6 的第 10 行），符号表变为图 7.9 所示（y 声明的栈在第 8 行弹出局部声明的 y，然后在第 10 行从 x 栈弹出局部声明的 x）。

![](img/062750ade02e28185b1fb8e8cf6dc89e_277_0.png)

**Figure 7.9** Symbol table structure at line 10 of Figure 7.6

在进入 q 之后（第 13 行），符号表变为图 7.10 所示。

![](img/062750ade02e28185b1fb8e8cf6dc89e_277_1.png)

**Figure 7.10** Symbol table structure at line 13 of Figure 7.6

当 q 退出（第 14 行）时，符号表如图所示 7.11。

![](img/062750ade02e28185b1fb8e8cf6dc89e_278_0.png)

Figure 7.11 Symbol table structure at line 14 of Figure 7.6

最后，在进入 main 之后（第 17 行），符号表如图所示 7.12。

![](img/062750ade02e28185b1fb8e8cf6dc89e_278_1.png)

Figure 7.12 Symbol table structure at line 17 of Figure 7.6

