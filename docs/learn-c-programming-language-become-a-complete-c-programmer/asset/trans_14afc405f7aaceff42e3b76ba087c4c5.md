
**Token**的定义如下：

```
enum class Kind : char {
name, number, end,
plus='+', minus='-', mul='*', div='/', print=';', assign='=', lp='(', rp=')'
};

struct Token {
Kind kind;
string string_value;
double number_value;
};
```

用字符的整数值来表示每个记号既方便又高效，还有助于使用调试器的人。只要没有用作输入的字符的值恰好与某个枚举值相同即可——就我所知，目前没有任何字符集的打印字符具有个位数的整数值。

**Token_stream**的接口如下：

```
class Token_stream {
public:
Token get();
const Token& current();
// ...
};
```

```
// 读取并返回下一个记号 // 最近读取的记号
```

其实现见§10.2.2。

每个语法分析函数都接受一个**bool**（§6.2.2）参数，名为**get**，用来指示该函数是否需要调用**Token_stream::get()**来获取下一个记号。每个语法分析函数计算“它自己的”表达式并返回结果。函数**expr()**处理加法和减法。它由一个循环组成，该循环查找要加或减的项：

```
double expr(bool get) {
double left = term(get);
// 加法和减法
for (;;) { // “永远”

switch (ts.current().kind) {
case Kind::plus:
left += term(true);
break;
case Kind::minus:
left -= term(true);
break;
default:
return left;
}
}
}
```

这个函数本身并没有做太多事情。它像大型程序中典型的较高级函数一样，调用其他函数来完成实际工作。

**switch**语句（§2.2.4，§9.4.2）将其条件值（在**switch**关键字后的括号中给出）与一组常量进行比较。**break**语句用于退出**switch**语句。如果被测试的值不匹配任何**case**标签，则执行**default**分支。程序员可以不提供**default**。

注意，类似2−3+4的表达式会按语法规则计算为(2−3)+4。奇怪的记号for(; ;)是表示无限循环的一种方式；你可以把它读作“永远”（§9.5）；**while(true)**是另一种写法。**switch**语句会不断执行，直到遇到不是+和−的东西，然后执行**default**分支中的**return**语句。

运算符+=和−=用于处理加法和减法；也可以使用**left=left+term(true)**和**left=left−term(true)**，而不改变程序的含义。但**left+=term(true)**和**left−=term(true)**不仅更简短，还能更直接地表达预期操作。每个赋值运算符都是一个独立的词法记号，因此**a+=1;**会因为+和=之间有空格而成为语法错误。

C++为二元运算符提供了赋值运算符：

```
+ - * / % & | ^ << >>
```

这样，以下赋值运算符都是可能的：

```
+= -= *= /= %= &= |= ^= <<= >>=
```

**%**是取模（余数）运算符；**&**、**|**和**^**分别是按位逻辑与、或和异或；**<<**和**>>**是左移和右移运算符；§10.3总结了这些运算符及其含义。对于应用于内置类型操作数的二元运算符@，表达式**x@=y**等价于**x=x@y**，但**x**只求值一次。

函数**term()**处理乘法和除法，其方式与**expr()**处理加法和减法相同：

```
double term(bool get) // 乘法和除法
{
double left = prim(get);
for (;;) {
switch (ts.current().kind) {
case Kind::mul:

left *= prim(true);
break;
case Kind::div:

if (auto d = prim(true)) {
left /= d;
break;
}
return error("divide by 0");
default:
return left;
}
}
}
```

除以零的结果是未定义的，而且通常是灾难性的。因此我们在除法前检查0，如果检测到零除数就调用error()。函数error()在§10.2.4中描述。

变量d在程序中恰好需要它的地方引入，并立即初始化。在条件中引入的名字的作用域是由该条件控制的语句，而得到的值就是条件的值（§9.4.3）。因此，当且仅当d非零时，除法运算和赋值left/=d才会执行。

处理初等表达式的函数prim()与expr()和term()很相似，但因为我们处在调用层次中较低的位置，所以会做一些实际的工作，并且不需要循环：

```
double prim(bool get) // 处理初等表达式
{
if (get) ts.get(); // 读取下一个记号

switch (ts.current().kind) {
case Kind::number: // 浮点常量
{ double v = ts.current().number_value;
ts.get();
return v;
}
case Kind::name:
{ double& v = table[ts.current().string_value]; if (ts.get().kind == Kind::assign) v = expr(true); return v;
}

// 找到对应的 // 看到“=”：赋值

case Kind::minus: // 一元减号
return -prim(true);
case Kind::lp:
{ auto e = expr(true);
if (ts.current().kind != Kind::rp) return error("')' expected");
ts.get(); // 吞掉“)”
return e;
}
default:
return error("primary expected");
}
}
```

当看到一个数字（即整数或浮点字面量）记号时，其值被放入number_value中。类似地，当看到一个名字（无论其如何定义；见§10.2.2和§10.2.3）记号时，其值被放入string_value中。

注意，prim()总是比它分析初等表达式所需的记号多读一个。原因是在某些情况下它必须这样做（例如，判断一个名字是否被赋值），所以为了保持一致，它在所有情况下都必须这样做。在语法分析函数只需要前进到下一个记号的情况下，它不会使用ts.get()的返回值。这没问题，因为我们可以从ts.current()获取结果。如果忽略get()返回值让我感到不安，我可能会添加一个只更新current()而不返回值的read()函数，或者显式“丢弃”结果：void(ts.get())。

在处理名字之前，计算器必须先向前查看以确定它是被赋值还是仅仅被读取。在两种情况下，都要查询符号表。符号表是一个map（§4.4.3，§31.4.3）：

```
map<string,double> table;
```

也就是说，当table以字符串为索引时，得到的值是字符串对应的double。例如，如果用户输入

```
radius = 6378.388;
```

计算器会进入case Kind::name并执行

```
double& v = table["radius"];
// ... expr()计算要赋的值 ...
v = 6378.388;
```

引用v用于在expr()从输入字符计算出6378.388期间持有与radius关联的double值。

第14章和第15章讨论如何将程序组织为一组模块。然而，这个计算器示例的声明可以有一个例外地排列，使每个声明都恰好出现一次并且在使用之前出现。这个例外是expr()，它调用term()，term()调用prim()，而prim()又调用expr()。这个调用循环必须以某种方式打破。在prim()定义之前声明

```
double expr(bool);
```

即可很好地解决。

## 10.2.2 输入

读取输入通常是程序中最杂乱的部分。为了与人交流，程序必须应付人的反复无常、习惯和看似随机的错误。试图强迫人按照更适合机器的行为方式行事，通常（合理地）会被认为令人反感。底层输入例程的任务是读取字符并从它们组合出更高层的记号。然后这些记号成为高层例程的输入单元。在这里，底层输入由ts.get()完成。编写底层输入例程不一定是日常工作。许多系统为此提供了标准函数。

首先，我们需要看到Token_stream的完整定义：

```
class Token_stream {
```

