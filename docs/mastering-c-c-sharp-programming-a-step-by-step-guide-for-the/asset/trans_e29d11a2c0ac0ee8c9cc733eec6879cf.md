
在不安全上下文中，表达式可以产生指针类型；但如果这种情况发生在不安全上下文之外，你将在编译时收到错误。因此，如果在不安全上下文之外的任何以下情况导致指针类型，你将收到错误：

- `simple_name`
- `member_access`
- `invocation_expression`
- `element_access`

`primary_no_array_creation_expression` 和 `unary_expression` 将允许这些结构出现在不安全上下文中：

```
primary_no_array_creation_expression_unsafe
    : pointer_member_access
    | pointer_element_access
    | sizeof_expression
    ;
```

```
unary_expression_unsafe
    : pointer_indirection_expression
    | addressof_expression
    ;
```

我们现在就来讨论这些结构；不安全运算符的结合性和优先级已隐含在语法中。

## 指针间接引用

该表达式由一个星号 (*) 和一个 unary_expression 组成：

```
pointer_indirection_expression
    : '*' unary_expression
    ;
```

一元 * 运算符表示指针间接引用，用于获取指针所指向的变量。如果 P 是类型为 T* 的指针表达式，则对 P 求值的结果将是类型为 T 的变量。如果试图对 void* 类型的表达式或非指针表达式应用一元 * 运算符，则会在编译时收到错误。

当你对空指针应用一元 * 运算符时，效果是实现定义的，并且无法保证不会抛出 System.NullReferenceException。

如果向指针赋了无效值，一元 * 运算符将具有未定义行为。使用 * 运算符解引用指针时，无效值的两个示例是：不再使用的变量地址，以及未针对所指向类型正确对齐的地址。

如果对 *P 形式的表达式求值，并且结果是一个变量，则认为该变量已初始赋值。

## 指针成员访问

该表达式由一个 primary_expression、一个“->”标记、一个 identifier 以及一个可选的 type_argument_list 组成。

```
pointer_member_access
```

```
: primary_expression '- >' identifier ;
```

在 P->I 形式的指针成员访问中，P 必须是除 void* 以外的任何指针类型的表达式，并且它必须表示 P 所指向类型中可访问的成员。

这些指针成员求值为 (*P).I。

示例：

```
using System;
```

```
struct Point
```

```
{
    public int x;
    public int y;

    public override string ToString() {
        return "(" + x + "," + y + ")";
    }
}

class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            p->x = 10;
            p->y = 20;
            Console.WriteLine(p->ToString());
        }
    }
}
```

在此示例中，我们使用 -> 运算符通过指针访问字段并调用结构体方法。由于 P->I 与 (*P).I 完全等价，我们可以将 Main 方法写成这样：

```
class Test
{
```

```
static void Main() {
    Point point;
    unsafe {
        Point* p = &point;
        (*p).x = 10;
        (*p).y = 20;
        Console.WriteLine((*p).ToString());
    }
}
```

## 指针元素访问

该表达式由一个 primary_no_array_creation_expression 以及方括号 [] 内的另一个表达式组成。

```
pointer_element_access
: primary_no_array_creation_expression '[' expression ']'
;
```

在指针元素的 P[E] 形式中，P 必须是除 void* 之外的任何指针类型的表达式，E 必须是可隐式转换为 int、uint、long 或 ulong 的表达式。

此格式的指针元素严格按 *(P + E) 求值。

示例：

```
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) p[i] = (char)i;
```

如果是可变变量，则会在编译时出错。当它表示的是可变变量时，可以在获取地址之前，使用 fixed 语句临时固定该变量。在类或结构的静态构造函数或实例构造函数之外，对于已定义的只读字段，该字段不被视为变量，而是一个值，这意味着无法获取其地址。同样，也无法获取常量的地址。

& 运算符的参数无需已明确赋值。但是，在执行 & 操作之后，在该操作发生的执行路径内，该运算符所应用的变量会被明确赋值。确保变量正确初始化的责任在于程序员。

示例：

```csharp
using System;

class Test
{
	static void Main() {
		int i;
		unsafe {
			int* p = &i;
			*p = 123;
		}
		Console.WriteLine(i);
	}
}
```

在此示例中，i 在初始化 p 的 &i 操作后被明确赋值。*p 内部的赋值将初始化 i，但由程序员确保包含此初始化，并且，如果

取消了该赋值，也不会产生编译时错误。

& 运算符的明确赋值规则可确保你避免对局部变量进行冗余初始化。例如，某些内部 API 会接受一个指向由该 API 填充的结构的指针。此类 API 的调用通常传递一个局部结构体变量的地址；如果该规则不存在，就需要对结构体变量进行冗余初始化。

## 指针递增和递减

在不安全上下文中，可以对除 void* 之外的任何类型的指针变量应用 ++ 运算符和 -- 运算符。因此，对于每个 T* 类型指针，以下运算符是隐式定义的：

- `T* operator ++(T* x);`
- `T* operator --(T* x);`

第一个运算符产生 x + 1 的结果，第二个运算符产生 x − 1 的结果。因此，对于 T* 类型的指针变量，++ 运算符会将 sizeof(T) 加到该变量包含的地址上，而 -- 运算符则相反——从该变量包含的地址中减去 sizeof(T)。

如果指针的递增或递减溢出指针类型域，结果将是实现定义的，但不会抛出任何异常。

## 指针算术

在不安全上下文中，可以将 − 运算符和 + 运算符应用于除 void* 类型以外的所有指针类型值。因此，对于每个 T* 类型指针，以下运算符是隐式定义的：

```
T* operator +(T* x, int y);
T* operator +(T* x, uint y);
T* operator +(T* x, long y);
T* operator +(T* x, ulong y);
```

```
T* operator +(int x, T* y);
T* operator +(uint x, T* y);
T* operator +(long x, T* y);
T* operator +(ulong x, T* y);
```

```
T* operator -(T* x, int y);
T* operator -(T* x, uint y);
T* operator -(T* x, long y);
T* operator -(T* x, ulong y);
```

```
long operator -(T* x, T* y);
```

假设你有一个表达式 P，其类型为 T* 指针类型。你还有一个表达式 N，其类型为 uint、int、long 或 ulong 类型。P + N 和 N + P 这两个表达式都会计算出一个 T* 类型指针值，该值是通过向 P 提供的地址加上 N * sizeof(T) 得到的。同样，P − N 表达式会计算出通过从 P 提供的地址中减去 N * sizeof(T) 得到的 T* 类型指针值。

假设你有一个表达式 P 和一个表达式 Q，两者均为 T* 指针类型，则 P − Q 表达式将给出 P 和 Q 两者提供的地址之差，然后将该差值除以 sizeof(T)。结果类型始终为 long。实际上，P - Q 将按 ((long)(P) − (long)(Q)) / sizeof(T) 计算。

示例：

```
using System;
```

```
class Test
```

```csharp
{
	static void Main() {
		unsafe {
			int* values = stackalloc int[20];
			int* p = &values[1];
			int* q = &values[15];
			Console.WriteLine("p - q = {0}", p - q);
			Console.WriteLine("q - p = {0}", q - p);
		}
	}
}
```

p - q = -14
q - p = 14

如果指针算术运算溢出指针类型域，结果将总是以类似于实现定义的方式被截断，但不会抛出任何异常。

## 指针比较

- bool operator ==(void* x, void* y);
- bool operator !=(void* x, void* y);
- bool operator <(void* x, void* y);
- bool operator >(void* x, void* y);
- bool operator <=(void* x, void* y);
- bool operator >=(void* x, void* y);
