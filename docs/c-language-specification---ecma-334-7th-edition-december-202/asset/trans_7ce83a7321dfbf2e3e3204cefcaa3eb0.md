
unsafe static void Fill(int* p, int count, int value)
{
    for (; count != 0; count--)
    {
        *p++ = value;
    }
}

static void Main()
{
    int[] a = new int[100];
    unsafe
    {
        fixed (int* p = a) Fill(p, 100, -1);
    }
}

fixed 语句用于固定一个数组，以便其地址可以传递给接受指针的方法。

示例结束

通过固定字符串实例产生的 char* 值始终指向以 null 结尾的字符串。在获取指向字符串实例 s 的指针 p 的 fixed 语句中，从 p 到 p + s.Length - 1 范围内的指针值表示字符串中字符的地址，而指针值 p + s.Length 始终指向一个 null 字符（值为 '\0' 的字符）。

## 示例：

```
class Test
{
    static string name = "xx";

    unsafe static void F(char* p)
    {
        for (int i = 0; p[i] != '\0'; ++i)
        {
            System.Console.WriteLine(p[i]);
        }
    }

    static void Main()
    {
        unsafe
        {
            fixed (char* p = name) F(p);
            fixed (char* p = "xx") F(p);
        }
    }
}
```

示例结束

示例：以下代码展示了 fixed_pointer_initializer，其表达式的类型不是 array_type 或 string：

```
public class C
{
    private int _value;
    public C(int value) => _value = value;
    public ref int GetPinnableReference() => ref _value;
}

public class Test
{
    unsafe private static void Main()
    {
        C c = new C(10);
        fixed (int* p = c)
        {
            // ...
        }
    }
}
```

类型 C 具有可访问的 GetPinnableReference 方法，其签名正确。在 fixed 语句中，当在 c 上调用该方法时返回的 ref int 用于初始化 int* 指针 p。示例结束

通过固定指针修改托管类型的对象可能导致未定义行为。

注意：例如，由于字符串是不可变的，因此程序员有责任确保指向固定字符串的指针所引用的字符不会被修改。注释结束

注意：字符串的自动空终止在调用期望“C 风格”字符串的外部 API 时特别方便。注意，然而，字符串实例允许包含 null 字符。如果存在此类 null 字符，则在将其视为以 null 结尾的 char* 处理时，字符串将显示为被截断。注释结束

## 23.8 固定大小缓冲区

### 23.8.1 通用

固定大小缓冲区用于将“C 风格”的内联数组声明为结构体的成员，主要用于与非托管 API 接口。

### 23.8.2 固定大小缓冲区声明

固定大小缓冲区是表示给定类型变量的定长缓冲区存储的成员。固定大小缓冲区声明引入一个或多个给定元素类型的固定大小缓冲区。

注意：像数组一样，固定大小缓冲区可以被认为包含元素。因此，数组定义的术语元素类型也用于固定大小缓冲区。注释结束

固定大小缓冲区仅允许在结构体声明中使用，并且只能在 unsafe 上下文中出现（§23.2）。

```
fixed_size_buffer_declaration
: attributes? fixed_size_buffer_modifier* 'fixed' buffer_element_type
  fixed_size_buffer_declarators ';'

fixed_size_buffer_modifier
```

```
: 'new'
| 'public'
| 'internal'
| 'private'
| 'unsafe'
;
```

```
buffer_element_type
: type
;
```

```
fixed_size_buffer_declarators
: fixed_size_buffer_declarator (',' fixed_size_buffer_declarator)*
;
```

```
fixed_size_buffer_declarator
: identifier '[' constant_expression ']'
;
```

固定大小缓冲区声明可以包含一组属性（§22）、new 修饰符（§15.3.5）、与结构体成员允许的声明访问性相对应的访问修饰符（§16.4.3）以及 unsafe 修饰符（§23.2）。属性和修饰符适用于固定大小缓冲区声明声明的所有成员。固定大小缓冲区声明中同一修饰符出现多次是错误。

固定大小缓冲区声明不允许包含 static 修饰符。

固定大小缓冲区声明的缓冲区元素类型指定声明引入的缓冲区（s）的元素类型。缓冲区元素类型应为预定义类型 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 bool 之一。

缓冲区元素类型后面跟着一个固定大小缓冲区声明符列表，每个声明符引入一个新的成员。固定大小缓冲区声明符由标识成员的名称的标识符组成，后跟用 [ 和 ] 标记括起来的常量表达式。常量表达式表示该固定大小缓冲区声明符引入的成员中的元素数。常量表达式的类型应可隐式转换为 int 类型，且值应为非零正整数。

固定大小缓冲区的元素应在内存中顺序布局。

声明多个固定大小缓冲区的固定大小缓冲区声明等价于使用相同属性和元素类型的单个固定大小缓冲区声明的多个声明。

*示例：*

```
unsafe struct A
{
    public fixed int x[5], y[10], z[100];
}
```

等价于

```
unsafe struct A
{
    public fixed int x[5];
    public fixed int y[10];
    public fixed int z[100];
}
```

*示例结束*

### 23.8.3 表达式中的固定大小缓冲区

固定大小缓冲区成员的成员查找（§12.5）与字段的成员查找完全相同。

固定大小缓冲区可以通过 simple_name（§12.8.4）、member_access（§12.8.7）或 element_access（§12.8.11）引用在表达式中使用。

当固定大小缓冲区成员作为简单名称引用时，其效果与形式为 this.I 的成员访问相同，其中 I 是固定大小缓冲区成员。

在形式为 E.I 的成员访问中，其中 E 可能是隐式的 this，如果 E 是结构体类型并且在该结构体类型中对 I 的成员查找识别出一个固定大小成员，则 E.I 的求值和分类如下：

- 如果表达式 E.I 未在 unsafe 上下文中出现，则会发生编译时错误。
- 如果 E 被分类为值，则会发生编译时错误。
- 否则，如果 E 是可移动变量（§23.4），则：
  - 如果表达式 E.I 是 fixed_pointer_initializer（§23.7），则表达式的结果是指向 E 中固定大小缓冲区成员 I 的第一个元素的指针。
  - 否则如果表达式 E.I 是 element_access（§12.8.11）中形式为 E.I[J] 的 primary_no_array_creation_expression（§12.8.11.1），则 E.I 的结果是指向 E 中固定大小缓冲区成员 I 的第一个元素的指针 P，并且封闭的 element_access 然后被求值作为指针元素访问（§23.6.4）P[J]。
  - 否则会发生编译时错误。
- 否则，E 引用一个固定变量，表达式的结果是指向 E 中固定大小缓冲区成员 I 的第一个元素的指针。结果的类型为 S*，其中 S 是 I 的元素类型，并被分类为值。

固定大小缓冲区的后续元素可以使用从第一个元素的指针操作进行访问。与数组访问不同，固定大小缓冲区元素的访问是 unsafe 操作且不进行范围检查。

示例：以下声明并使用了一个具有固定大小缓冲区成员的结构体。

```
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize)
    {
        int len = s.Length;
        if (len > bufSize)
        {
            len = bufSize;
        }
        for (int i = 0; i < len; i++)
        {
            buffer[i] = s[i];
        }
        for (int i = len; i < bufSize; i++)
        {
            buffer[i] = (char)0;
        }
    }
    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```

*示例结束*

### 23.8.4 确定性赋值检查

固定大小缓冲区不受确定性赋值检查（§9.4）的约束，并且固定大小缓冲区成员在结构体类型变量的确定性赋值检查中被忽略。

当固定大小缓冲区成员的最外层包含的结构体变量是静态变量、类实例的实例变量或数组元素时，固定大小缓冲区的元素会自动初始化为其默认值（§9.3）。在所有其他情况下，固定大小缓冲区的初始内容是未定义的。

## 23.9 栈分配

请参阅 §12.8.21 了解 stackalloc 操作符的一般信息。在此，讨论该操作符产生指针的能力。

在 unsafe 上下文中，如果 stackalloc_expression（§12.8.21）作为 local_variable_declaration（§13.6.2）的初始化表达式出现，其中 local_variable_type 为指针类型（§23.3）或推断（var），则 stackalloc_expression 的结果是指向已分配块开头的类型为 T * 的指针，其中 T 是 stackalloc_expression 的 unmanaged_type。

在所有其他方面，unsafe 上下文中 local_variable_declarations（§13.6.2）和 stackalloc_expressions（§12.8.21）的语义遵循为安全上下文定义的语义。

*示例：*

```
unsafe
{
    // Memory uninitialized
    int* p1 = stackalloc int[3];
    // Memory initialized
    int* p2 = stackalloc int[3] { -10, -15, -30 };
    // Type int is inferred
    int* p3 = stackalloc[] { 11, 12, 13 };
    // Can't infer context, so pointer result assumed
    var p4 = stackalloc[] { 11, 12, 13 };
    // Error: no conversion exists
    long* p5 = stackalloc[] { 11, 12, 13 };
    // Converts 11 and 13, and returns long*
}
```
