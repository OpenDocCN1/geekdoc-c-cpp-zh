

```c
unsigned char testPattern0 = 0x20;    // testPattern0 = 0010 0000
unsigned char setPattern0 = 0x08;     // setPattern0 = 0000 1000

// assume portShadow holds 1010 0110
if (portShadow & testPattern0)      // if bit 5 is set, the AND will give a nonzero result
{
  // set bit5 reset bit 5 and update portShadow
  // portShadow = (1010 0110 & ~(0010 0000)) | (0000 1000)
  // portShadow = (1010 0110 & 1101 1111) | (0000 1000)
  // portShadow = 1000 1110
  portShadow = (portShadow & ~testPattern0 ) | setPattern0;
  setPort(portShadow);
}
```

## 图 7.2 使用位运算符测试和修改 I/O 端口信号

无需实际读取端口状态的时间开销即可测试端口状态——从内存读取可能快得多。

如果影子寄存器存储在内部寄存器中，操作可能会更快。

在某些微处理器实现中，端口状态可能无法读取，只能写入。

当复位位 5 时，与其声明一个单独变量来保存可用于复位该位的模式，不如直接对用于测试该位的模式取反。

```
// portShadow = (1010 0110 & ~(0010 0000)) | (0000 1000)
// portShadow = (1010 0110 & 1101 1111) | (0000 1000)
```

代码片段的第一行显示起始模式。第二行显示按位与运算右操作数的按位取反。与运算的结果将复位位 5，得到中间结果

```
1000 0110
```

作为最后一步，我们只需将逻辑 1 或入位位置 3，得到

```
1000 1110
```

## 编码风格

使用位运算符时，良好的做法是使用括号以确保实现所需的操作。

现在让我们看看如何使用左移运算符来辅助完成此任务。请记住，移位运算符是二元运算符。它们的两个操作数包括要移位的操作数和移位量。该运算符实现逻辑移位，除非采取相反措施，否则应用于操作数的移位只是暂时的。

## 示例 7.2

让我们从两个 8 位数字开始，将一个左移四位，另一个右移两位，如图 7.3 的代码片段所示。

```
unsigned char a = 0x3;        // a = 0000 0011
unsigned char b = 0xC5;       // b = 1100 0101
printf( "a shifted 4 places left is %x", a << 4); // prints ...0011 0000
printf( "b shifted 2 places right is %x", b >> 2); // prints ...0110 0101
printf( "a is %x", a );       // prints ...0000 0011
printf( "b is %x", b );       // prints ...1100 0101
0000 0011   1100 0101
0011 0000   0011 0001
a << 4;     b >> 2;
```

## 图 7.3 使用位运算符在数据字中设置和复位位

请注意，两个操作数的值将保持不变。

## 示例 7.3

现在让我们使用左移运算符重复前面的示例，如图 7.4 所示。

```
unsigned char bitPattern0 = 0x1;    // bitPattern0 = 0000 0001
// assume portShadow holds 1010 0110
if (portShadow & (bitPattern0 << 5))   // if bit 5 is set, the AND will give a nonzero result
{
    // set bit5 reset bit 5 and update portShadow
    // portShadow = (1010 0110 & ~(0010 0000)) | (0000 1000)
    // portShadow = (1010 0110 & 1101 1111) | (0000 1000)
    // portShadow = 1000 1110
    portShadow = (portShadow & ~(bitPattern0 << 5)) | (bitPattern0 << 3);
    setPort(portShadow);
}
```

## 图 7.4 使用位运算符在数据字中设置和复位位

## 示例 7.4

*getPort(), setPort()*

现在，让我们看一个稍微复杂的问题。

将使用访问函数 *getPort()* 从微处理器端口读取数据，然后测试模式 0001 1010。与 *setPort()* 类似，此类函数在大多数支持端口 I/O 的微处理器上很典型。该函数读取端口并返回端口信号的状态。

在此示例中，我们执行以下操作：

- 从端口读取数据。
- 将所有位复位为零，除了感兴趣的位。

我们通过定义一个掩码来实现复位操作，该掩码在感兴趣的位置为 1，其他位置为 0，然后将掩码与数据进行与运算。

模式中值为 1 的位将在结果中显示为 1。所有其他位将显示为 0。掩码操作很重要，以确保后续的模式匹配仅限于相关位。

接下来，我们在被测试字与所需模式之间形成按位异或（^）。如果存在该模式，结果应全为 0。

这些步骤在图 7.5 的代码片段中说明。

```
unsigned char getPort(void); // port access function prototype
unsigned char testPattern0 = 0x1A; // testPattern0 = 0001 1010
unsigned char mask = 0x1E; // mask = 0001 1110
unsigned char portData = 0x0; // working variable
// assume port holds 1101 1011
portData = getPort(); // read the port
if (((portData & mask) ^ testPattern0) == 0) // will give a zero result if pattern present
{
    printf("pattern present\n");
}
```

### 图 7.5 使用位运算符在数据字中测试模式

## 7.2.3 算术运算

我们可以利用位移操作来提高特定算术运算的系统性能。认识到二进制乘以二只是左移，除以二只是右移，人们可以在必要时执行此类操作，而不是使用数学包中的相应运算。

一些基本操作可以如图 7.6 所示实现。

```
EXAMPLE 7.5

Multiply by x where x is 2, 4, 8, ...
result = number << x;

Divide by y where y is 2, 4, 8, ...
result = number >> y;
```

### 图 7.6 使用位运算符执行算术运算

一些稍微复杂的示例可以如图 7.7 的代码模块中所示实现。

## 示例 7.6

```
Multiply by x where x is a simple number such as 5, 6, 9, 10, 12,...
result = (number << 2) + number; // multiply by 5 ...0101
result = (number << 2) + (number << 1); // multiply by 6 ...0110
result = (number << 3) + number; // multiply by 9 ...1001
result = (number << 3) + (number << 1); // multiply by 10 ...1010
result = (number << 3) + (number << 2); // multiply by 12 ...1100
```

## 图 7.7 使用位运算符执行算术运算

更复杂的操作收益甚微。

## 7.3 指针变量和内存地址

## 7.3.1 入门

我们一直在研究持有不同类型数据和不同值的变量。

```
int myAge = 39;
float mySpeed = 54.52;
char myAnswer = 't';
```

我们知道这些变量存储在内存的某个位置，并且不同类型需要不同数量的内存。此时，我们应该提出几个问题。如何知道变量存储在哪里？如何知道变量如何存储？大数据对象的存储方式是否与较小的对象相同？如何将大数据对象传递给函数？这些问题对于嵌入式应用比桌面应用更相关，因为在嵌入式应用中，人们通常试图优化系统中内存的数量、组织和使用。桌面应用程序通常没有此类顾虑。让我们看看如何开始回答这些问题。

每个定义的变量在内存中都有一个存储位置，并且该位置有一个值，无论变量是否初始化或赋值。该位置有一个地址。随着程序中每个变量的存储，系统内存将开始类似于图 7.8 中的样子。

![](img/679b8d2d47f1bf86e17aca48f596f5cc_348_0.png)

### 图 7.8 内存中数据存储的典型视图

使用数据（即变量）时，可以读取其值、修改其值，或询问其存储位置。我们已经了解到变量持有不同类型的值，整数、浮点数、字符等等。在 C 语言中，变量值的类型也可以是内存地址。地址只是带有值的另一个变量。到目前为止，这没什么特别。但是，现在可能会产生一些混淆。

正如我们最初使用内置类型时所学到的，它们只是内存中的一组位。直到将类型与该集合关联，它才作为整数、字符或浮点数获得意义。如果我们查看 16 位数量 0xFE89，没有什么可以将其区分为变量的值或变量的地址。编译器也并不更聪明。因此，为了减少混淆，每个持有地址的变量都会被赋予一个独特的名称和类型——指针。因此，指针是一个值为内存地址的变量——既不多也不少。

## 指针

考虑上述内存片段中标准 C 声明、定义和初始化。

```
unsigned int myData0 = 0x3;
```

编译器响应此类声明：

### myData0

- 分配 16 位内存来保存变量 myData0，假设我们使用 16 位整数。这既是声明也是定义。
- 将值 3 (0x3) 放入这 16 位中。
- 将内存中数据存储的地址（例如 0x3000）与变量 myData0 关联。

随后，当我们写 myData0 时，实际上是指位置 0x3000 处的数据。如果我们想知道数据存储在哪里，即内存中的哪个地址，只需询问即可。我们使用地址运算符 &，编译器会返回相应信息。如果我们写

### 地址运算符

```
&myData0; // read address of myData0
```

编译器返回 0x3000 作为数据存储的位置。现在，如果我们写

```
int *myData0Ptr = &myData0;
```

会发生以下情况。编译器

### myData0Ptr

- 分配 16 位内存来保存（指针类型）变量 myData0Ptr。
- 查找 myData0 的地址（即 0x3000），并将该值放入该地址的 16 位中。

我们使用符号 * 来告诉编译器该变量是指针。我们使用像 myData0Ptr 这样的独特名称来告诉我们（或与代码一起工作的人）该变量是指针。这是良好的编码风格。

处理指针和指针声明时，知道如何读取它们有时有助于使其角色更加清晰。

