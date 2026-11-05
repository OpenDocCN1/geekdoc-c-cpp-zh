

```
p - q = -14
q - p = 14
```

示例结束]

如果指针算术运算溢出指针类型的域，结果将以实现定义的方式截断，但不会产生异常。

## 23.6.8 指针比较

在非安全上下文中，==、!=、<、>、<= 和 >= 运算符（§12.11）可应用于所有指针类型的值。指针比较运算符包括：

```
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

由于存在从任意指针类型到 void* 类型的隐式转换，因此可以使用这些运算符比较任意指针类型的操作数。这些比较运算符将两个操作数给出的地址当作无符号整数进行比较。

## 23.6.9 sizeof 运算符

对于某些预定义类型（§12.7.13），sizeof 运算符产生一个常量 int 值。对于所有其他类型，sizeof 运算符的结果由实现定义，并被归类为值，而不是常量。

成员打包到结构体中的顺序未指定。

为了对齐，结构体的开头、结构体内部以及结构体末尾可能存在未命名的填充。用作填充的位的内容是不确定的。

当应用于具有结构体类型的操作数时，结果是该类型变量中的总字节数，包括任何填充。

## 23.7 fixed 语句

在非安全上下文中，embedded-statement（§13.1）产生式允许一种附加构造，即 fixed 语句，它用于“固定”可移动变量，使其地址在该语句执行期间保持不变。

```
embedded-statement:
  ...
  fixed-statement
fixed-statement:
  fixed ( pointer-type fixed-pointer-declarators ) embedded-statement
fixed-pointer-declarators:
  fixed-pointer-declarator
  fixed-pointer-declarators , fixed-pointer-declarator
fixed-pointer-declarator:
  identifier = fixed-pointer-initializer
fixed-pointer-initializer:
  & variable-reference
  expression
```

每个 fixed-pointer-declarator 声明一个具有给定 pointer-type 的局部变量，并用相应的 fixed-pointer-initializer 计算出的地址初始化该局部变量。在 fixed 语句中声明的局部变量，可在该变量声明右侧出现的任何 fixed-pointer-initializer 中访问，也可在该 fixed 语句的 embedded-statement 中访问。由 fixed 语句声明的局部变量被视为只读。如果嵌入语句尝试修改此局部变量（通过赋值或 ++ 和 -- 运算符），或将其作为 ref 或 out 参数传递，则发生编译时错误。

在 fixed-pointer-initializer 中使用捕获的局部变量（§12.16.6.2）、值参数或参数数组是错误的。fixed-pointer-initializer 可以是下列之一：

- 标记“&”后跟一个 variable-reference（§10.5），该引用指向非托管类型 T 的可移动变量（§23.4），前提是类型 T* 可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算给定变量的地址，并保证该变量在 fixed 语句执行期间保持在固定地址。
- 一个数组类型的表达式，其元素为非托管类型 T，前提是类型 T* 可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算数组中第一个元素的地址，并保证整个数组在 fixed 语句执行期间保持在固定地址。如果数组表达式为 null，或数组元素数为零，则 fixed 语句的行为由实现定义。
- 一个 string 类型的表达式，前提是类型 char* 可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算字符串中第一个字符的地址，并保证整个字符串在 fixed 语句执行期间保持在固定地址。如果字符串表达式为 null，则 fixed 语句的行为由实现定义。
- 一个 simple-name 或 member-access，它引用可移动变量的固定大小缓冲区成员，前提是该固定大小缓冲区成员的类型可隐式转换为 fixed 语句中给定的指针类型。在这种情况下，初始化器计算指向固定大小缓冲区（§23.8.3）第一个元素的指针，并保证该固定大小缓冲区在 fixed 语句执行期间保持在固定地址。

对于由 fixed-pointer-initializer 计算的每个地址，fixed 语句确保该地址引用的变量在 fixed 语句执行期间不会被垃圾回收器重定位或处置。[示例：如果由 fixed-pointer-initializer 计算的地址引用对象的字段或数组实例的元素，则 fixed 语句保证包含该字段或元素的对象的实例在该语句的生存期内不会被重定位或处置。示例结束]

程序员有责任确保由 fixed 语句创建的指针在该语句执行完毕后不再存在。[示例：当由 fixed 语句创建的指针传递给外部 API 时，程序员有责任确保这些 API 不保留对这些指针的任何记忆。示例结束]

固定对象可能导致堆碎片化（因为它们无法移动）。因此，只有在绝对必要时才应固定对象，并且只应持续尽可能短的时间。

[示例：以下示例

```csharp
class Test
{
    static int x;
    int y;
    unsafe static void F(int* p) {
        *p = 1;
    }
}
```

```
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

演示了 fixed 语句的若干用法。第一条语句固定并获取静态字段的地址，第二条语句固定并获取实例字段的地址，第三条语句固定并获取数组元素的地址。在每种情况下，使用常规 & 运算符都会出错，因为这些变量都被归类为可移动变量。

上例中的第三条和第四条 fixed 语句产生相同的结果。一般来说，对于数组实例 a，在 fixed 语句中指定 &a[0] 与直接指定 a 相同。下面是 fixed 语句的另一个示例，这次使用 string：

```
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

示例结束]

在非安全上下文中，一维数组的数组元素按索引递增顺序存储，从索引 0 开始，到索引 Length − 1 结束。对于多维数组，数组元素的存储方式是：最右侧维度的索引先递增，然后向左下一个维度递增，依此类推。

在获取指向数组实例 a 的指针 p 的 fixed 语句中，从 p 到 p + a.Length − 1 的指针值表示数组中各元素的地址。同样，从 p[0] 到 p[a.Length − 1] 的变量表示实际的数组元素。鉴于数组的存储方式，我们可以将任意维度的数组视为线性数组。[示例：

```
using System;
class Test
{
    static void Main() {
        int[,] a = new int[2,3,4];
        unsafe {
            fixed (int* p = a) {
                for (int i = 0; i < a.Length; ++i) // treat as linear
                    p[i] = i;
            }
        }
    }
}
```

