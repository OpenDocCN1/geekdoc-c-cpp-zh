
如输出所示，表达式

```
&nums [0]
```

与

```
nums
```

相同。由于第二种形式更短，大多数程序员在需要指向数组开头的指针时使用它。

## 索引指针

当指针引用一个数组时，指针可以像数组一样被索引。这种语法提供了指针算术的替代方案，在某些情况下可能更方便。下面是一个示例：

```csharp
// Index a pointer as if it were an array.
using System;

class PtrIndexDemo {
    unsafe static void Main() {
        int[] nums = new int[10];

        // Index a pointer.
        Console.WriteLine("Index pointer like array.");
        fixed (int* p = nums) {
            for(int i=0; i < 10; i++)
                p[i] = i; // index pointer like array

            for(int i=0; i < 10; i++)
                Console.WriteLine("p[{0}]: {1} ", i, p[i]);
        }

        // Use pointer arithmetic.
        Console.WriteLine("\nUse pointer arithmetic.");
        fixed (int* p = nums) {
            for(int i=0; i < 10; i++)
                *(p+i) = i; // use pointer arithmetic

            for(int i=0; i < 10; i++)
                Console.WriteLine("*(p+{0}): {1} ", i, *(p+i));
        }
    }
}
```

输出如下所示：

```
Index pointer like array.
p[0]: 0
p[1]: 1
p[2]: 2
p[3]: 3
p[4]: 4
p[5]: 5
p[6]: 6
p[7]: 7
p[8]: 8
p[9]: 9
```

使用指针算术。

```
*(p+0): 0
*(p+1): 1
*(p+2): 2
*(p+3): 3
*(p+4): 4
*(p+5): 5
*(p+6): 6
*(p+7): 7
*(p+8): 8
*(p+9): 9
```

正如程序所示，具有以下一般形式的指针表达式

```
*(ptr + i)
```

可以用数组索引语法重写为：

```
ptr[i]
```

关于索引指针，有两点很重要需要理解：首先，不会进行边界检查。因此，可能访问指针所引用的数组末尾之外的元素。其次，指针没有 **Length** 属性。因此，使用指针无法得知数组有多长。

## 指针与字符串

尽管字符串在 C# 中实现为对象，但可以通过指针访问字符串中的字符。为此，你将使用如下的 **fixed** 语句将指向字符串开头的指针赋给一个 **char*** 指针：

```csharp
fixed(char* p = str) { // ...
```

**fixed** 语句执行后，**p** 将指向构成字符串的字符数组的开头。该数组是 *以空字符结尾的*，这意味着它以零结尾。你可以利用这一事实来测试数组的末尾。以空字符结尾的字符数组是在 C/C++ 中实现字符串的方式。因此，获取指向 **string** 的 **char*** 指针允许你以与 C/C++ 几乎相同的方式操作字符串。

下面是一个演示通过 **char*** 指针访问字符串的程序：

```csharp
// Use fixed to get a pointer to the start of a string.
using System;

class FixedString {
    unsafe static void Main() {
        string str = "this is a test";
        // Point p to start of str.
        fixed(char* p = str) {
            // Display the contents of str via p.
            for(int i=0; p[i] != 0; i++)
                Console.Write(p[i]);
        }

        Console.WriteLine();
    }
}
```

输出如下所示：

```
this is a test
```

## 多重间接

你可以让一个指针指向另一个指向目标值的指针。这种情况称为多重间接，或指针的指针。指针的指针可能令人困惑。图 20-1 有助于阐明多重间接的概念。如你所见，普通指针的值是包含所需值的变量的地址。在指针的指针的情况下，第一个指针包含第二个指针的地址，而第二个指针指向包含所需值的变量。

多重间接可以按所需程度继续进行，但很少需要超过指针的指针。事实上，过度的间接难以跟踪且容易出现概念性错误。

一个指针的指针变量必须如此声明。你通过在类型名后放置一个额外的星号来做到这一点。例如，以下声明告诉编译器 q 是类型为 int 的指针的指针：

```
int** q;
```

你应该理解 q 不是指向整数的指针，而是指向 int 指针的指针。

![](img/7022d9b97326a713562c15aa43977d15_620_0.png)

要访问指针的指针间接指向的目标值，你必须两次应用星号运算符，如以下示例所示：

```csharp
using System;

class MultipleIndirect {
    unsafe static void Main() {
        int x;    // holds an int value
        int* p;   // holds an int pointer
        int** q;  // holds a pointer to an int pointer

        x = 10;
        p = &x;  // put address of x into p
        q = &p;  // put address of p into q

        Console.WriteLine(*q);  // display the value of x
    }
}
```

输出是 x 的值，即 10。在程序中，p 被声明为指向 int 的指针，q 被声明为指向 int 指针的指针。

最后一点：不要将多重间接与高级数据结构（如链表）混淆。这两者是根本不同的概念。

## 指针数组

指针可以像任何其他数据类型一样被数组化。大小为 3 的 int 指针数组的声明为

```
int * [] ptrs = new int * [3];
```

要将名为 var 的 int 变量的地址赋给指针数组的第三个元素，写

```
ptrs[2] = &var;
```

要查找 var 的值，写

```
*ptrs[2]
```

## sizeof

在不安全上下文中工作时，你有时会发现知道 C# 值类型之一的大小（以字节为单位）很有用。要获取此信息，请使用 sizeof 运算符。它的一般形式为：

```
sizeof(type)
```

这里，type 是正在获取其大小的类型。一般来说，sizeof 主要用于特殊情况，特别是在使用托管和非托管代码混合时。

## stackalloc

你可以使用 **stackalloc** 从栈上分配内存。它只能在初始化局部变量时使用，其一般形式为：

```
type *p = stackalloc type[size]
```

这里，*p* 是一个指针，接收足够容纳 *size* 个 *type* 对象的内存的地址。此外，*type* 必须是非引用类型。如果栈上没有足够的空间分配内存，则会抛出 **System.StackOverflowException**。最后，**stackalloc** 只能在不安全上下文中使用。

通常，对象的内存是从 *堆* 分配的，*堆* 是空闲内存区域。从栈上分配内存是例外情况。分配在栈上的变量不会被垃圾回收。它们仅在声明它们的方法执行期间存在。当离开该方法时，内存会被释放。使用 **stackalloc** 的一个优点是，你无需担心内存被垃圾回收器移动。

下面是一个使用 **stackalloc** 的示例：

```csharp
// Demonstrate stackalloc.

using System;

class UseStackalloc {
    unsafe static void Main() {
        int* ptrs = stackalloc int[3];

        ptrs[0] = 1;
        ptrs[1] = 2;
        ptrs[2] = 3;

        for(int i=0; i < 3; i++)
            Console.WriteLine(ptrs[i]);
    }
}
```

输出如下所示：

```
1
2
3
```

## 创建固定大小缓冲区

**fixed** 关键字的第二种用法使你能够创建固定大小的单维数组。在 C# 文档中，这些被称为 *固定大小的缓冲区*。固定大小的缓冲区始终是 **struct** 的成员。固定大小缓冲区的目的是允许创建 **struct**，其中构成缓冲区的数组元素包含在 **struct** 内。通常，当你在 **struct** 中包含数组成员时，只有对数组的引用实际保存在 **struct** 内。通过使用固定大小缓冲区，你使整个数组包含在 **struct** 内。这产生了一个结构，可以在 **struct** 的大小很重要的情况下使用，例如在混合语言编程中、与 C# 程序未创建的数据接口，或在任何时候需要包含数组的非托管 **struct**。固定大小缓冲区只能在不安全上下文中使用。
