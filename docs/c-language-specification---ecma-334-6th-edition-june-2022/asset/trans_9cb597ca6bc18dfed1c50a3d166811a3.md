
形式为 P[E] 的指针元素访问被精确求值为 *(P + E)。有关指针间接运算符 (*) 的描述，请参阅 §22.6.2。有关指针加法运算符 (+) 的描述，请参阅 §22.6.7。

Example: 如下代码中

```
class Test
{
    static void Main()
    {
        unsafe
        {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) p[i] = (char)i;
        }
    }
}
```

指针元素访问用于在 for 循环中初始化字符缓冲区。由于操作 P[E] 与 *(P + E) 精确等价，该示例同样可以写成：

```
class Test
{
    static void Main()
    {
        unsafe
        {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++)
            {
                *(p + i) = (char)i;
            }
        }
    }
}
```

*结束示例*

指针元素访问运算符不检查越界错误，访问越界元素时的行为是未定义的。

> 注：这与 C 和 C++ 相同。结束注记

### 22.6.5 取地址运算符

addressof_expression 由一个与号 (&) 后跟一个 unary_expression 组成。

```
addressof_expression
    : '&' unary_expression
    ;
```

给定类型为 T 且被归类为固定变量 (§22.4) 的表达式 E，构造 &E 计算由 E 给出的变量的地址。结果的类型为 T*，并被归类为值。如果 E 未被归类为变量，如果 E 被归类为只读局部变量，或如果 E 表示可移动变量，则会发生编译时错误。在最后一种情况下，可以使用 fixed 语句 (§22.7) 在获取其地址之前暂时“固定”该变量。

*注：如 §11.7.6 所述，在定义只读字段的结构或类的实例构造函数或静态构造函数之外，该字段被视为值，而不是变量。因此，其地址无法获取。同样，常量的地址也无法获取。*

& 运算符不要求其参数被明确赋值，但在 & 操作之后，运算符所应用的变量在该操作发生的执行路径中被视为已明确赋值。确保在此情况下变量确实得到正确初始化是程序员的责任。

*示例：* 如下代码中

```
using System;

class Test
{
    static void Main()
    {
        int i;
        unsafe
        {
            int* p = &i;
            *p = 123;
        }
        Console.WriteLine(i);
    }
}
```

i 在用于初始化 p 的 &i 操作之后被视为已明确赋值。对 *p 的赋值实际上初始化了 i，但包含此初始化是程序员的责任，如果删除该赋值也不会发生编译时错误。

*结束示例*

*注：& 运算符的明确赋值规则的存在是为了避免局部变量的冗余初始化。例如，许多外部 API 接受指向由 API 填充的结构的指针。对此类 API 的调用通常传递局部结构体变量的地址，而没有该规则，则需要对结构体变量进行冗余初始化。结束注记*

*注：当局部变量、值参数或参数数组被匿名函数 (§11.7.21) 捕获时，该局部变量、参数或参数数组不再被视为固定变量 (§22.7)，而是被视为可移动变量。因此，任何不安全代码获取已被匿名函数捕获的局部变量、值参数或参数数组的地址都是错误。结束注记*

### 22.6.6 指针递增和递减

在不安全上下文中，++ 和 -- 运算符 (§11.7.14 和 §11.8.6) 可以应用于除 void* 之外的所有类型的指针变量。因此，对于每个指针类型 T*，以下运算符被隐式定义：

```
T* operator ++(T* x);
T* operator --(T* x);
```

这些运算符分别产生与 x+1 和 x-1 相同的结果 (§22.6.7)。换句话说，对于类型为 T* 的指针变量，++ 运算符将 sizeof(T) 加到变量中包含的地址上，而 -- 运算符将 sizeof(T) 从变量中包含的地址中减去。

如果指针递增或递减操作溢出指针类型的域，结果是实现定义的，但不会产生异常。

### 22.6.7 指针算术

在不安全上下文中，+ 运算符 (§11.9.5) 和 – 运算符 (§11.9.6) 可以应用于除 void* 之外的所有指针类型的值。因此，对于每个指针类型 T*，以下运算符被隐式定义：

```
T* operator +(T* x, int y);
T* operator +(T* x, uint y);
T* operator +(T* x, long y);
T* operator +(T* x, ulong y);
T* operator +(int x, T* y);
T* operator +(uint x, T* y);
T* operator +(long x, T* y);
T* operator +(ulong x, T* y);
T* operator -(T* x, int y);
T* operator -(T* x, uint y);
T* operator -(T* x, long y);
T* operator -(T* x, ulong y);
long operator -(T* x, T* y);
```

给定指针类型 T* 的表达式 P 和类型为 int、uint、long 或 ulong 的表达式 N，表达式 P + N 和 N + P 计算的类型为 T* 的指针值，该值是通过将 N * sizeof(T) 加到由 P 给出的地址得到。同样，表达式 P – N 计算的类型为 T* 的指针值，该值是通过从由 P 给出的地址减去 N * sizeof(T) 得到。

给定两个指针类型 T* 的表达式 P 和 Q，表达式 P – Q 计算由 P 和 Q 给出的地址之间的差值，然后将该差值除以 sizeof(T)。结果的类型始终为 long。实际上，P – Q 计算为 ((long)(P) - (long)(Q)) / sizeof(T)。

示例：

```
using System;
class Test
{
    static void Main()
    {
        unsafe
        {
            int* values = stackalloc int[20];
            int* p = &values[1];
            int* q = &values[15];
            Console.WriteLine($"p - q = {p - q}");
            Console.WriteLine($"q - p = {q - p}");
        }
    }
}
```

其产生的输出为：

p - q = -14
q - p = 14

结束示例

如果指针算术操作溢出指针类型的域，结果会以实现定义的方式被截断，但不会产生异常。

### 22.6.8 指针比较

在不安全上下文中，==、!=、<、<= 和 >= 运算符 (§11.11) 可以应用于所有指针类型的值。指针比较运算符为：

```
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

由于存在从任何指针类型到 void* 类型的隐式转换，任何指针类型的操作数都可以使用这些运算符进行比较。比较运算符将两个操作数给出的地址作为无符号整数进行比较。

### 22.6.9 sizeof 运算符

对于某些预定义类型 (§11.7.17)，sizeof 运算符产生一个常量 int 值。对于所有其他类型，sizeof 运算符的结果是实现定义的，并被归类为值，而不是常量。

成员被打包到结构体中的顺序是不指定的。

出于对齐目的，结构体开头、结构体内部和结构体末尾可能存在未命名的填充。用于填充的位的内容是不确定的。

当应用于具有结构体类型的操作数时，结果是该类型变量中的总字节数，包括任何填充。

## 22.7 fixed 语句

在不安全上下文中，embedded_statement (§12.1) 产生式允许一个额外的构造，即 fixed 语句，用于“固定”一个可移动变量，使其地址在语句持续期间保持不变。

```
fixed_statement
    : 'fixed' '(' pointer_type fixed_pointer_declarators ')' embedded_statement
    ;

fixed_pointer_declarators
    : fixed_pointer_declarator (',' fixed_pointer_declarator)*
    ;

fixed_pointer_declarator
    : identifier '=' fixed_pointer_initializer
    ;

fixed_pointer_initializer
    : '&' variable_reference
    | expression
    ;
```

每个 fixed_pointer_declarator 声明给定 pointer_type 的局部变量，并使用相应的 fixed_pointer_initializer 计算的地址初始化该局部变量。在 fixed 语句中声明的局部变量可以在其右侧出现的任何 fixed_pointer_initializers 中访问
