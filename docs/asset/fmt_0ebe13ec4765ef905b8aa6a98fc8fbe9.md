
输入的浮点值通过 `XMM0-XMM3` 寄存器传递，其余所有内容通过栈传递 [180]。

`a` 通过 `XMM0` 传递，`b` 通过 `XMM` 寄存器传递——`XMM` 寄存器是 128 位的（正如我们在 SIMD 节中了解到的；第 53 页的示例 1.36），而 `double` 值是 64 位的，因此只使用了寄存器的一半。

`DIVSD` 是一条 SSE 指令，全称为“标量双精度浮点数除法”，它仅将一个 `double` 值除以另一个 `double` 值，且在操作数的低半部分进行。

常量由编译器以 IEEE 754 格式编码。`MULSD` 和 `ADDSD` 的工作原理相同，只是 `double` 分对应乘法和加法。

函数执行的 `double` 结果保存在 `XMM0` 寄存器中。

这就是非优化版 MSVC 的工作方式：

## 列表 1.402: MSVC 2012 x64

```assembly
real@4010066666666666r DQ 04010066666666666r : 4.1

real@40091eb851eb851f DQ 040091eb851eb85fr : 3.14

a = 8

b = 16

PROC

    movsd xmm0, QWORD PTR [rsp+16], xmm1

    movsd xmm0, QWORD PTR [rsp+8], xmm0

    movsd xmm0, QWORD PTR a[rsp]

    divsd xmm0, QWORD PTR  real@40091eb851eb851f

    movsd xmm1, QWORD PTR b[rsp]

    mulsd xmm1, QWORD PTR  real@40100666666666666

    addsd xmm0, xmm1

    ret

0

ENDP
```

> 180 MSDN：参数传递

如果你发现任何拼写错误、错误或有任何建议，请随时给我留言：我的邮箱。谢谢！

略显冗余。输入参数保存在“影子空间”中（第 129 页的 1.14.2），但只保留了它们寄存器的低半部分，即 `double` 类型的 64 位值。GCC 生成的代码相同。

## x86

让我们为 x86 编译这个示例。尽管是为 x86 生成的，MSVC 2012 使用了 SSE 指令：

## 列表 1.403: 非优化 MSVC 2012 x86

```assembly
tv0 = -8      ; size = 8

$a = 8       ; size = 8

$b = 16      ; size = 8

f    PROC

    push    ebp

    mov     esp, esp

    sub     esp, 8

    movsd xmm0, QWORD PTR a$[esp]

    divsd xmm0, QWORD PTR real@40091eb851eb851f

    movsd xmm1, QWORD PTR b$[esp]

    mulsd xmm1, QWORD PTR real@40100666666666666

    addsd xmm0, xmm1

    movsd QWORD PTR tv0[esp], xmm0

    fld QWORD PTR tv0[esp]

    mov     esp, esp+8

    pop     ebp

    ret
```

## 列表 1.404: 优化 MSVC 2012 x86

```assembly
tv0 = -8      ; size = 8

$a = 8       ; size = 8

$b = 16      ; size = 8

f    PROC

    movsd xmm0, QWORD PTR a$[esp]

    divsd xmm0, QWORD PTR real@40091eb851eb851f

    movsd xmm1, QWORD PTR b$[esp]

    mulsd xmm1, QWORD PTR real@40100666666666666

    addsd xmm0, xmm1

    movsd QWORD PTR tv0[esp-4], xmm0

    fld QWORD PTR tv0[esp-4]

    ret
```
