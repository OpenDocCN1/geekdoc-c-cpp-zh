
如果是可变变量，则会在编译时出错。当它表示的是可变变量时，可以在获取地址之前，使用 `fixed` 语句临时固定该变量。在类或结构的静态构造函数或实例构造函数之外，对于已定义的只读字段，该字段不被视为变量，而是一个值，这意味着无法获取其地址。同样，也无法获取常量的地址。

`&` 运算符的参数无需已明确赋值。但是，在执行 `&` 操作之后，在该操作发生的执行路径内，该运算符所应用的变量会被明确赋值。确保变量正确初始化的责任在于程序员。

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

在此示例中，`i` 在初始化 `p` 的 `&i` 操作后被明确赋值。`*p` 内部的赋值将初始化 `i`，但由程序员确保包含此初始化，并且，如果取消了该赋值，也不会产生编译时错误。

`&` 运算符的明确赋值规则可确保你避免对局部变量进行冗余初始化。例如，某些内部 API 会接受一个指向由该 API 填充的结构的指针。此类 API 的调用通常传递一个局部结构体变量的地址；如果该规则不存在，就需要对结构体变量进行冗余初始化。

### 指针递增和递减

在不安全上下文中，可以对除 `void*` 之外的任何类型的指针变量应用 `++` 运算符和 `--` 运算符。因此，对于每个 `T*` 类型指针，以下运算符是隐式定义的：

- `T* operator ++(T* x);`
- `T* operator --(T* x);`

第一个运算符产生 `x + 1` 的结果，第二个运算符产生 `x − 1` 的结果。因此，对于 `T*` 类型的指针变量，`++` 运算符会将 `sizeof(T)` 加到该变量包含的地址上，而 `--` 运算符则相反——从该变量包含的地址中减去 `sizeof(T)`。

如果指针的递增或递减溢出指针类型域，结果将是实现定义的，但不会抛出任何异常。

### 指针算术

在不安全上下文中，可以将 `−` 运算符和 `+` 运算符应用于除 `void*` 类型以外的所有指针类型值。因此，对于每个 `T*` 类型指针，以下运算符是隐式定义的：

```csharp
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

假设你有一个表达式 `P`，其类型为 `T*` 指针类型。你还有一个表达式 `N`，其类型为 `uint`、`int`、`long` 或 `ulong` 类型。`P + N` 和 `N + P` 这两个表达式都会计算出一个 `T*` 类型指针值，该值是通过向 `P` 提供的地址加上 `N * sizeof(T)` 得到的。同样，`P − N` 表达式会计算出通过从 `P` 提供的地址中减去 `N * sizeof(T)` 得到的 `T*` 类型指针值。

假设你有一个表达式 `P` 和一个表达式 `Q`，两者均为 `T*` 指针类型，则 `P − Q` 表达式将给出 `P` 和 `Q` 两者提供的地址之差，然后将该差值除以 `sizeof(T)`。结果类型始终为 `long`。实际上，`P - Q` 将按 `((long)(P) − (long)(Q)) / sizeof(T)` 计算。

示例：

```csharp
using System;

class Test
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

```text
p - q = -14
q - p = 14
```

如果指针算术运算溢出指针类型域，结果将总是以类似于实现定义的方式被截断，但不会抛出任何异常。

### 指针比较

- `bool operator ==(void* x, void* y);`
- `bool operator !=(void* x, void* y);`
- `bool operator <(void* x, void* y);`
- `bool operator >(void* x, void* y);`
- `bool operator <=(void* x, void* y);`
- `bool operator >=(void* x, void* y);`

对于所有其他类型，结果将是实现定义的，并且它是一个值而不是常量。

成员被打包到结构体中的顺序没有指定。

为了对齐，结构体的开始、中间和结束可能有未命名的填充。用作填充的位内容是不确定的。

当你将此应用于结构体类型的操作数时，结果将是该指定类型变量的总字节数，其中包括填充。

### The Fixed Statement

在不安全上下文中，`embedded_statement` 产生式允许 `fixed` 语句，这是一种用于临时固定可移动变量的另一个构造。这将允许变量的地址在语句的整个生命周期内保持不变。

```
fixed_statement
    : 'fixed' '(' pointer_type fixed_pointer_declarators ')'
      embedded_statement
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

每个 `fixed_pointer_declarator` 将执行两件事——声明指定 `pointer_type` 的局部变量，并使用与其对应的 `fixed_pointer_initializer` 提供的地址对其进行初始化。当你在 `fixed` 语句中声明局部变量时，它可以在声明右侧出现的任何 `fixed_pointer_initializer` 中访问，并且可以在 `fixed` 语句的 `embedded_statement` 中访问。当你使用 `fixed` 语句声明局部变量时，它是一个只读变量。如果 `embedded_statement` 尝试使用 `++` 和 `--` 运算符修改变量，或尝试将变量作为 `ref` 或 `out` 参数传递，将在编译时发生错误。

`fixed_pointer_initializer` 可以是以下任意一种：

- `&` 标记与对类型为 `T`（`unmanaged`）的可移动变量的 `variable_reference`，只要 `T*` 类型可以隐式转换为 `fixed` 语句中指定的指针类型。初始化器将计算给定变量的地址，并且变量将在 `fixed` 语句“存活”期间保持固定地址。
- 包含 `unmanaged` 类型 `T` 元素的 `array_type` 表达式，只要 `T*` 类型可以隐式转换为 `fixed` 语句提供的指针类型。初始化器将从数组的第一个元素计算地址，并且整个数组将在 `fixed` 语句的生命周期内保持固定地址。如果数组中没有元素或表达式为 `null`，则初始化器计算的地址等于零。
- `string` 类型表达式，只要 `char*` 可以隐式转换为 `fixed` 语句提供的指针类型。初始化器将计算字符串第一个字符的地址，并且整个字符串将在 `fixed` 语句持续期间保持固定地址。如果字符串表达式为 `null`，则 `fixed` 语句的行为是实现定义的。
- `member_access` 或 `simple_name`，它提供对可移动变量的固定大小缓冲区成员的引用，只要固定大小缓冲区成员类型可以隐式转换为 `fixed` 语句提供的指针类型。初始化器将计算固定大小缓冲区的第一个元素的指针。固定大小缓冲区将在 `fixed` 语句“存活”期间保持固定地址。

对于 `fixed_pointer_initializer` 计算的每个地址，`fixed` 语句将确保地址引用的变量在 `fixed` 语句的生命周期内不会被处置或被垃圾回收器重新定位。例如，如果计算出的地址引用对象字段或数组实例元素，则 `fixed` 语句将确保包含它的对象实例在语句运行期间不会被处置或重新定位。

程序员有责任确保 `fixed` 语句创建的指针不能比语句执行时间活得更长。例如，`fixed` 语句创建的指针被传递给外部 API，程序员必须确保 API 不能保留指针的内存。

固定对象可能导致堆碎片，因为这些对象不能被移动。因此，你只有在绝对必要时才固定对象，并且时间要尽可能短。

An example

```csharp
class Test
{
    static int x;
    int y;

    unsafe static void F(int* p) {
        *p = 1;
    }

    static void Main() {
        Test t = new Test();
        int[] a = new int[10];
        unsafe {
            fixed (int* p = &x) F(p);
            fixed (int* p = &t.y) F(p);
            fixed (int* p = &a[0]) F(p);
            fixed (int* p = a) F(p);
        }
    }
}
```

此示例展示了 `fixed` 语句的多种用法。在第一个语句中，我们正在固定一个静态字段并获取其地址。在第二个中，我们固定一个实例字段并获取地址，在第三个中，我们固定一个数组元素并获取地址。在每一种情况下，如果我们使用常规的 `&` 运算符，它将是一个错误，因为每个变量都是可移动变量。第四个语句将给出与第三个类似的结果。

在此示例中，`fixed` 语句使用了字符串：

```csharp
class Test
{
    static string name = "xx";

    unsafe static void F(char* p) {
        for (int i = 0; p[i] != '\0'; ++i)
            Console.WriteLine(p[i]);
    }

    static void Main() {
        unsafe {
            fixed (char* p = name) F(p);
            fixed (char* p = "xx") F(p);
        }
    }
}
```

在不安全上下文中，一维数组元素按索引递增的顺序存储。这从索引 `0` 开始，到索引 `Length - 1` 结束。对于多维数组，元素以右侧维度的索引增加然后最左侧，接着是下一个右侧，左侧，依此类推的方式存储。在 `fixed` 语句获取对数组实例 `a` 的指针时，从 `p` 到 `p + a.Length − 1` 的指针值表示数组元素的地址。同样，从 `p[0]` 到 `p[a.Length − 1]` 的变量表示数组的实际元素。鉴于数组的存储方式，维度数组（任意维度）可以被视为线性：

An example:

```csharp
using System;

class Test
{
    static void Main() {
        int[, ,] a = new int[2,3,4];
        unsafe {
            fixed (int* p = a) {
                for (int i = 0; i < a.Length; ++i)  // treat as linear
                    p[i] = i;
            }
        }
        for (int i = 0; i < 2; ++i)
            for (int j = 0; j < 3; ++j) {
                for (int k = 0; k < 4; ++k)
                    Console.Write("[{0},{1},{2}] = {3,2} ", i, j, k, a[i,j,k]);
                Console.WriteLine();
            }
    }
}
```

而此的输出将是：

```text
[0,0,0] = 0 [0,0,1] = 1 [0,0,2] = 2 [0,0,3] = 3
[0,1,0] = 4 [0,1,1] = 5 [0,1,2] = 6 [0,1,3] = 7
[0,2,0] = 8 [0,2,1] = 9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23
```

Another example:

```csharp
class Test
{
    unsafe static void Fill(int* p, int count, int value) {
        for (; count != 0; count--) *p++ = value;
    }

    static void Main() {
        int[] a = new int[100];
        unsafe {
            fixed (int* p = a) Fill(p, 100, -1);
        }
    }
}
```

我们使用 `fixed` 语句固定数组，以便我们可以将地址传递给将接受指针的方法：

An example:

```csharp
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    Font f;

    unsafe static void Main() {
        Test test = new Test();
        test.f.size = 10;
        fixed (char* p = test.f.name) {
            PutString("Times New Roman", p, 32);
        }
    }
}
```

此处，我们使用 `fixed` 语句来固定结构类型的固定大小缓冲区，以便可以将地址用作指针。

当你固定一个字符串实例，且结果为 `char*` 值时，它始终指向一个以 `null` 结尾的字符串。在与指向字符串实例 `s` 的指针 `p` 相关的 `fixed` 语句中，从 `p` 到 `p + s.Length` 范围内的指针值表示字符串字符的地址，而指针值 `p + s.Length` 将始终指向值为 `\0` 的字符，即空字符。

使用固定指针修改非托管类型对象时，结果通常是未定义行为。例如，字符串是不可变的，因此，程序员有责任确保指针引用的固定字符串中的字符不会被修改。

一个方便之处在于字符串的自动 `null` 结尾。这对于期望 C 风格字符串的外部 API 非常适用。但请注意，字符串实例不能包含 `null` 字符；如果在将字符串视为以 `null` 结尾的 `char*` 时存在这些字符，那么这些 `null` 字符看起来会被截断。

### 固定大小缓冲区

我们使用固定大小缓冲区来声明作为结构成员的 C 风格内联数组。当你想要与非托管 API 交互时，它们非常有用。

#### 固定大小缓冲区的声明

固定大小缓冲区是用于表示指定类型变量的固定长度缓冲区存储的成员。固定大小缓冲区的声明至少引入一个指定元素类型的固定大小缓冲区。我们只能在结构声明中使用固定大小缓冲区，并且只能在非安全上下文中声明它们。

```
struct_member_declaration_unsafe
    : fixed_size_buffer_declaration
    ;

fixed_size_buffer_declaration
    : attributes? fixed_size_buffer_modifier* 'fixed'
```
