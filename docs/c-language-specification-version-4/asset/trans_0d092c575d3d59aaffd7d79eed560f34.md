
```csharp
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
```

该示例演示了 fixed 语句的几种用法。第一个语句固定并获取静态字段的地址，第二个语句固定并获取实例字段的地址，第三个语句固定并获取数组元素的地址。在每种情况下，使用常规的 & 运算符都会出错，因为这些变量都被归类为可移动变量。

第四个 fixed 语句与第三个产生类似的结果。

fixed 语句的此示例使用字符串：

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

在不安全上下文中，单维数组的元素按递增索引顺序存储，从索引 0 开始，到索引 Length – 1 结束。对于多维数组，数组元素存储方式为先增加最右维的索引，然后是下一个左维，依此类推向左。在获取指向数组实例 a 的指针 p 的 fixed 语句中，从 p 到 p + a.Length – 1 的指针值表示数组中元素的地址。同样，变量 p[0] 到 p[a.Length – 1] 表示实际的数组元素。鉴于数组的存储方式，我们可以将任意维度的数组视为线性。

例如：

```csharp
using System;
class Test
{
    static void Main() {
        int[,,] a = new int[2,3,4];
        unsafe {
            fixed (int* p = a) {
                for (int i = 0; i < a.Length; ++i) // treat as linear
                    p[i] = i;
            }
        }

        for (int i = 0; i < 2; ++i) {
            for (int j = 0; j < 3; ++j) {
                for (int k = 0; k < 4; ++k)
                    Console.Write("{0},{1},{2} = {3,2} ", i, j, k, a[i,j,k]);
                Console.WriteLine();
            }
        }
    }
}
```

其输出为：

```text
[0,0,0] = 0 [0,0,1] = 1 [0,0,2] = 2 [0,0,3] = 3
[0,1,0] = 4 [0,1,1] = 5 [0,1,2] = 6 [0,1,3] = 7
[0,2,0] = 8 [0,2,1] = 9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23
```

在示例中

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

使用 fixed 语句固定数组，以便将其地址传递给接受指针的方法。

在示例中：

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
    unsafe static void Main()
    {
        Test test = new Test();
        test.f.size = 10;
        fixed (char* p = test.f.name) {
            PutString("Times New Roman", p, 32);
        }
    }
}
```

使用 fixed 语句固定结构体的固定大小缓冲区，以便其地址可作为指针使用。

通过固定字符串实例产生的 char* 值始终指向以 null 结尾的字符串。在获取指向字符串实例 s 的指针 p 的 fixed 语句中，从 p 到 p + s.Length - 1 的指针值表示字符串中字符的地址，而指针值 p + s.Length 始终指向 null 字符（值为 '\0' 的字符）。

通过固定指针修改托管类型的对象可能导致未定义行为。例如，由于字符串是不可变的，程序员有责任确保不修改由指向固定字符串的指针引用的字符。

字符串的自动 null 终止在调用期望“C 风格”字符串的外部 API 时特别方便。然而请注意，字符串实例允许包含 null 字符。如果存在此类 null 字符，则在将其视为以 null 结尾的 char* 处理时，字符串将显示为被截断。

## 18.7 固定大小缓冲区

固定大小缓冲区用于将“C 风格”的内联数组声明为结构体的成员，主要用于与非托管 API 接口。

### 18.7.1 固定大小缓冲区声明

固定大小缓冲区是表示给定类型变量的固定长度缓冲区存储的成员。固定大小缓冲区声明引入一个或多个给定元素类型的固定大小缓冲区。固定大小缓冲区仅允许在结构体声明中使用，并且只能出现在不安全上下文中（§18.1）。

```text
struct-member-declaration:
    ...
    fixed-size-buffer-declaration

fixed-size-buffer-declaration:
    attributesopt fixed-size-buffer-modifiersopt fixed buffer-element-type
    fixed-size-buffer-declarators ;

fixed-size-buffer-modifiers:
    fixed-size-buffer-modifier
    fixed-size-buffer-modifier fixed-size-buffer-modifiers

fixed-size-buffer-modifier:
    new
    public
    protected
    internal
    private
    unsafe

buffer-element-type:
    type

fixed-size-buffer-declarators:
    fixed-size-buffer-declarator
    fixed-size-buffer-declarator , fixed-size-buffer-declarators

fixed-size-buffer-declarator:
    identifier [ constant-expression ]
```

固定大小缓冲区声明可以包含一组属性（§17）、new 修饰符（§10.2.2）、四个访问修饰符（§10.2.3）的有效组合以及 unsafe 修饰符（§18.1）。属性和修饰符适用于固定大小缓冲区声明所声明的所有成员。同一修饰符在固定大小缓冲区声明中出现多次是错误。

固定大小缓冲区声明不允许包含 static 修饰符。

固定大小缓冲区声明的缓冲区元素类型指定声明所引入的缓冲区（s）的元素类型。缓冲区元素类型必须是预定义类型 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 bool 之一。

缓冲区元素类型后面跟着固定大小缓冲区声明符的列表，每个声明符引入一个新成员。固定大小缓冲区声明符由标识成员的名称的标识符组成，后跟用 [ 和 ] 标记括起来的常量表达式。该常量表达式表示该固定大小缓冲区声明符所引入的成员中的元素数。常量表达式的类型必须可隐式转换为 int 类型，且值必须是大于零的正整数。

固定大小缓冲区的元素保证在内存中按顺序布局。

声明多个固定大小缓冲区的固定大小缓冲区声明等效于使用相同属性和元素类型的单个固定大小缓冲区声明的多次声明。例如

```csharp
unsafe struct A
{
    public fixed int x[5], y[10], z[100];
}
```

等效于

```csharp
unsafe struct A
{
    public fixed int x[5];
    public fixed int y[10];
    public fixed int z[100];
}
```

### 18.7.2 表达式中的固定大小缓冲区

固定大小缓冲区成员的成员查找（§7.3）与字段的成员查找完全相同。

固定大小缓冲区可以通过简单名称（§7.5.2）或成员访问（§7.5.4）在表达式中引用。

当固定大小缓冲区成员作为简单名称引用时，其效果与形式为 this.I 的成员访问相同，其中 I 是固定大小缓冲区成员。

在形式为 E.I 的成员访问中，如果 E 是结构体类型，并且在该结构体类型中对 I 的成员查找识别出一个固定大小缓冲区成员，则 E.I 的求值和分类如下：

- 如果表达式 E.I 不在不安全上下文中出现，则会发生编译时错误。
- 如果 E 被分类为值，则会发生编译时错误。
- 否则，如果 E 是可移动变量（§18.3）并且表达式 E.I 不是固定指针初始化器（§18.6），则会发生编译时错误。
- 否则，E 引用一个固定变量，表达式的结果是指向 E 中固定大小缓冲区成员 I 的第一个元素的指针。结果的类型为 S*，其中 S 是 I 的元素类型，并被分类为值。

固定大小缓冲区的后续元素可以使用从第一个元素开始的指针操作进行访问。

与数组访问不同，固定大小缓冲区元素的访问是不安全操作且不进行范围检查。

以下示例声明并使用具有固定大小缓冲区成员的结构体。
