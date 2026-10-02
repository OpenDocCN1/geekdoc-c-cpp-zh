
这些指令的作用是：将 `ESP` 寄存器保存到栈上，将 `ESP` 寄存器的值设置为 `ESP` 的值，并在栈上为局部变量分配空间。

`ESP` 的值在函数执行期间保持不变，用于访问局部变量和参数。为了这个目的，可以使用 `ESP`，但由于它在这一方法下会发生变化，所以这种做法不太方便。

函数结尾（function epilogue）释放栈上分配的空间，将 `EBP` 寄存器中的值恢复到初始状态，并将控制权返回给调用者：

```
mov     esp, ebp
pop     ebp
ret     0
```

函数序言和结尾通常在反汇编器中被识别，用于界定函数。

如果你发现了任何拼写错误、错误或建议，请随时给我留言：我的电子邮箱。谢谢！

## 1.6.1 递归

序言和结尾（Prolrologues and epilogues，原文此处拼写错误）会影响性能。

## 1.7 空函数

序言和结尾（Prolrologues and epilogues，原文此处拼写错误）会影响性能。

## 1.8 返回值

现在我们知道序言和结尾，一个空函数（1.3）。

## 1.9 栈

序言和结尾（Prolrologues and epilogues，原文此处拼写错误）会影响性能。

### 1.9.1 栈是用来做什么的？

**保存返回地址**

#### x86

使用 `CALL` 指令调用另一个函数时，`CALL` 之后的点地址会被保存到栈中，然后无条件跳转到操作数的地址。`CALL` 指令等价于 `PUSH address_after_call / JMP` 指令对。`RET` 从栈中获取一个值并跳转到该值——这等价于 `POP tmp / JMP` 指令对。

...但无论如何，它生成了正确的代码：

| ?@YAXZ PROC | ; f |
|---|---|
| ; Line 2 | push ebp |
| mov ebp, esp | |
| ; Line 3 | call ?@YAXZ ; f |
| ; Line 4 | pop ebp |
| ?@YAXZ END | ret ; f |

此外，如果我们开启了编译器优化（/ox 选项），优化后的代码将不会溢出栈，而是会正确工作 57：

| ?@YAXZ PROC | ; f |
|---|---|
| ; Line 2 | $LL$3 |
| ; Line 3 | jmp SHORT $LL$f |
| ?@YAXZ END | |

GCC 4.4.1 在两种情况下都生成了类似的代码，并对该问题发出了警告。

#### ARM

ARM 程序也使用栈来保存返回地址，但方式不同。正如在“Hello, world!”（第24 页 1.5 节）中提到的，RA 被保存到 LR（链接寄存器）。然而，如果需要调用另一个函数并再次使用 LR，则必须保存它的值。通常，它是在函数序言中保存的。

通常我们使用诸如 `PUSH R4-R7, LR` 指令配合序言中的 `POP R4-R7` 指令，寄存器值会被保存在栈中，包括 LR。

尽管如此，如果一个函数从未调用任何其他函数，在 RISC 术语中它被称为叶函数（leaf function）58。结果，如果此类函数很小且使用的寄存器很少，叶函数就不会保存 LR，它可能完全不使用栈。在不使用栈的情况下调用叶函数是可能的，这比在 x86 机器上更快，因为不需要额外的 RAM 作为栈 59。这对于栈内存无法分配或可以避免的情况也有用。

> 57此处参阅 infocenter.com/help/index.jsp?topic=/com.arm.doc.faqs/ka1375.html
> 58早些时候，在 PDP-11 上，CALL 指令（调用其他函数）是昂贵的；可能会消耗执行时间的 50%，因此认为拥有少的函数是一种反模式（Eric S. Raymond, 《Unix 编程艺术》, (2003) 第4章第二部分）。

如果你发现了拼写错误或有任何建议，请随时给我写信：我的电子邮件。谢谢！

一些叶函数的示例：第 133 页的 11.14.3、第133 页的 11.14、第395 页的 1.282、第417 页的 1.298、第417 页的 1.285、第264 页的 1.192、第261 页的 1.190、第285 页的 1.209。

## 传递函数参数

x86 中传递参数最流行的方法被称为“cdecl”：

```
push arg3
push arg2
push arg1
call f
add esp, 12 ; 4*3=12
```

调用者函数通过栈指针获取参数。

因此，在执行 f() 函数的第一条指令之前，在栈中定位参数值的方式如下：

| ESP | 返回地址 |
|---|---|
| ESP+4 | 参数#1，在 IDA 中标记为 arg 0 |
| ESP+8 | 参数#2，在 IDA 中标记为 arg 4 |
| ESP+0C | 参数#3，在 IDA 中标记为 arg 8 |

关于其他调用约定的信息，请参阅（第932 页 6.1 节）。

顺便说，调用者函数没有任何关于传递了多少参数的信息。具有可变参数的 C 函数（如 `printf()`）可以使用格式字符串占位符（以 % 符号开头）来确定它们的数量。

如果我们写如下代码：

```
printf("%d %d %d", 1234);
```

`printf()` 将打印并返回栈中紧邻其后的数字⁶⁰。

这就是为什么我们如何声明 `main()` 函数并不重要：可以是 `main()`、`main(int argc, char *argv[])` 或 `main(int argc, char *argv[], char *envp[])`。

事实上，CRT 代码调用 main() 的方式如下：

```
push envp
push argv
push argc
call main
...
```

即使你将 main() 声明为没有参数的 `main()`，它们仍然存在于栈中，但不会使用。如果你将 main() 声明为 `main(int argc, char *argv[])`，你可以使用前两个参数，而第三个参数对你的函数来说将保持“不可见”。甚至，可以声明为 `main(int argc)`，它可以正常工作。

> ⁶⁰严格意义上不是随机的，而是不可预测的：第50 页 1.9 节

如果你发现了拼写错误、错误或任何建议，请随时给我写信：我的邮箱。谢谢！

## 传递参数的替代方法

值得注意的是，没有任何规定程序员必须通过栈传递参数。这不是强制性要求。可以实现完全不使用栈的任何其他方法。

在汇编语言初学者中相当流行的方法是通过全局变量传递参数，例如：列表 1.39：汇编代码

```
...
mov X, 123
mov Y, 456
call do_something
```

但通过全局变量传递参数有一个缺点：`do_something` 不能递归调用，因为它是不安全的。这种方法在多线程环境下也是不安全的。此外，通过寄存器传递参数通常是更好的选择，例如：

```
mov eax, 123
mov ebx, 456
call do_something
```

这种方法在不使用栈的情况下调用函数是可能的，这比在 x86 机器上更快，因为不需要额外的 RAM 作为栈59。这对于栈内存无法分配或可以避免的情况也有用。

```c
#else
snprintf(buf, 600, "hi! %d, %d, %d\n", 1, 2, 3); // MSVC
#endif
puts(buf);
};
```

`snprintf` 函数的作用类似于 `printf()`，但它不是将结果输出到 stdout（例如在终端或控制台中），而是将结果写入 `buf` 缓冲区中。`puts()` 函数将 `buf` 的内容复制到 stdout。当然，这两个函数调用可以被一个 `printf()` 调用代替，但我们必须说明小内存缓冲区的用法。

## MSVC

让我们进行编译（MSVC 2010）：

列表 1.40：MSVC 2010

```
mov     eax, 600      ; 00000258H
call    _alloc_probe_16
       esi, esp
push     3
push     2
push     1
push     OFFSET $SG2672
push     600      ; 00000258H
push     esi
call    _snprintf
push     esi
call    _puts
add      esp, 28
```

唯一的 `alloca()` 参数是通过 `EAX` 传递的（而不是推入栈中） 63。

## GCC + Intel 语法

GCC 4.4.1 在调用外部函数时执行相同的操作：

> 63 这是因为 `alloca()` 是一个编译器内置函数（第 125 页的 11.4）。我们需要一个单独的函数而不是代码中仅仅几条指令的原因，是因为 MSVC64 的实现也包含从分配的内存中读取的代码，以便让操作系统将物理内存映射到这个 VRE 区域。`alloca()` 调用中，`ESP` 指向 600 字节块，我们可以将其作为 `buf` 数组的内存。

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的电子邮箱。谢谢！

## 列表 1.41：GCC 4.7.3

```
.LC0:\  .string "hi! %d, %d, %d\n"
push     ebp
mov      ebp, esp
push     ebx
sub      esp, 660 ; [esp+39]
lea      ebx, -16
mov      DWORD PTR [esp], ebx    ; 按 16 字节边界对齐指针
mov      DWORD PTR [esp+20], 3   ; s
mov      DWORD PTR [esp+16], 2
mov      DWORD PTR [esp+12], 1
mov      DWORD PTR [esp], OFFSET:LC0 ; "hi! %d, %d, %d\n"
mov      DWORD PTR [esp], 600      ; maxlen
call     printf
mov      DWORD PTR [esp], ebx    ; s
call     puts
mov      ebx, DWORD PTR [esp-4]
ret
```

## GCC + AT&T 语法

让我们看看代码，但使用 AT&T 语法：

## 列表 1.42：GCC 4.7.3

```
.LC0:\  .string "hi! %d, %d, %d\n"
push    %ebp
movl    %esp, %ebp
push    %ebx
subl    $660, %esp
leal    -16(%esp), %ebx
andl    %ebx, (%esp)
mvl    $3, 20(%esp)
mvl    $2, 16(%esp)
mvl    $1, 12(%esp)
mvl    $LC0, 8(%esp)
mvl    $600, 4(%esp)
call    printf
mvl    %ebx, (%esp)
call     puts
mov    -4(%esp), %ebx
leave
ret
```

如果你发现了拼写错误、错误或有任何建议，请随时给我写信：我的电子邮箱。谢谢！

代码与上一个列表相同。

顺便说，`movl $3, 20(%esp)` 对应 Intel 语法中的 `mov DWORD PTR [esp+20], 3`。在 AT&T 语法中，内存寻址寄存器+偏移量格式为 `offset(%register)`。

## (Windows) SEH

SEH 记录也存储在栈上（如果存在的话）。更多信息请参阅：（第 973 页的 6.5.3）。

## 缓冲区溢出保护

更多信息见此处（第 340 页的 1.26.2）。

## 栈存储的自动释放

或许将局部变量和 SEH 记录自动存储在栈中的原因是，它们在函数退出时会被释放，只需一条指令来控制栈指针。函数参数同样在函数结束时自动释放。与此相反，存储在堆中的一切内容都必须显式释放。

### 1.9.3 典型的栈布局

在 32 位环境下，函数开始时第一条指令执行之前的典型栈布局如下：

| 偏移量 | 内容 |
| :--- | :--- |
| ESP-0xC | 局部变量#2，在 IDA 中标记为 var 8 |
| ESP-8 | 局部变量#1，在 IDA 中标记为 var 4 |
| ESP-4 | EBP 的保存值 |
| ESP | 返回地址 |
| ESP+4 | 参数#1，在 IDA 中标记为 arg 0 |
| ESP+8 | 参数#2 |
| ESP+0xC | 参数#3 |
