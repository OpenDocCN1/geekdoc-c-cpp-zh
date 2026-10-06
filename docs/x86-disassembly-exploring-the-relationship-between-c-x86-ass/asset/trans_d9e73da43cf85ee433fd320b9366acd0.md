

# 调用约定

```
ST1 := ST1 + ST0
FPU POP ST0
```

将 ST(1) 和 ST(0) 相乘并将结果存储在 ST(1) 中。然后，ST(0) 被标记为空，栈指针递增。因此，ST(1) 的内容位于栈顶。所以，栈顶的两个值被相乘，结果存储在栈顶。因此，在我们上面的指令 `fmul ST(1), ST(0)*` 中（这也是该函数的最后一条指令），我们可以看到最后一个结果存储在 ST0 中。因此，浮点数参数是通过普通栈传递的，但浮点数结果是通过 FPU 栈栈传递的。

最后的一点是，`MyFunction` 清理了它自己的栈空间，如末尾的 **ret 20** 命令所示。由于没有参数通过寄存器传递，该函数看起来完全符合我们预期的 STDCALL 函数一模一样：参数从右到左传递在栈上，并且由函数自己清理栈空间。我们将在下面看到，这实际上是一个假设。

作为对比，这里是 GCC 的列表：

```
LC1:
  .long
  .long
  .align 8 0 1073741824

LC2:
  .long
  .long 0 1074266112
.global MyFunction
  .def MyFunction;    .scl 2;    .type 32;    .endf
  MyFunction:
    push
    movl %esp,%eb
    subl $16,,(eb)
    fld
    -8(%eb)
    fstpl
    fld
    -16(%eb)
    fstpl
    -8(%eb)
    fld
    fadd
    %st, xst(1)
    fld
    -16(%eb)
    LC1
    fadd
    %st, xst(1)
    %st, xst(1)
    fmul
    24(%eb)
    fld
    LC2
    fadd
    %st, xst(1)
    fmul
    %st, xst(1)
    leave
    ret
    .align 8
```

这是一个非常复杂的列表，所以我们将逐步分析它（尽管速度很快）。在栈上分配了 16 字节的额外空间。然后，通过 `fld` 和 `fstpl` 指令的组合，将前两个参数从偏移 +8 和 +16 移动到相对于 ebp 的偏移 -8 和 -16。这看起来是在浪费时间，但请记住，此时优化是关闭的。**fld1** 将浮点值 1.0 加载到 FPU 栈上。fadd 将栈顶的值（1.0）加到 ST1 中的值 [ebp - 8] 上，该值原本是 [ebp + 8]。

# 浮点数

# 21.2.2 MyFunction 的 FASTCALL：

这里是 MyFunction 的清晰列表：

```
PUBLIC          @MyFunction2020
PUBLIC          __real83ff000000000000
PUBLIC          __real8400000000000000
PUBLIC          __real848000000000000
EXTRN           floatused:NEAR
CONST           COMDAT          __real83ff000000000000
                               SEGMENT
CONST           __real83ff000000000000 DQ 03ff000000000000r ; 1
                                ENDS
CONST           COMDAT          _
                               SEGMENT
CONST           __real8400000000000000 DQ 0400000000000000r ; 2
                                ENDS
CONST           COMDAT          _
                               SEGMENT
CONST           __real8480000000000000 DQ 040000000000000r ; 3
                                ENDS
TEXT            _
x$ = 8                                     ; size = 8
y$ = 16                                     ; size = 8
z$ = 24                                     ; size = 4
@MyFunction2020 PROC NEAR
; Line 7
    mov             ebp, ebp
; Line 8
    fld             QWORD PTR y$[ebp]
    fadd            QWORD PTR [__real83ff000000000000]
    fld             QWORD PTR [__real8400000000000000]
    fmul            QWORD PTR ST(1)
    fld             QWORD PTR [ebp]
    fadd            QWORD PTR [__real8480000000000000]
    fmul            ST(1), ST(0); Line 9
    pop             ebp
    set             20                              ; 0000014H
@MyFunction20 END
TEXT            ENDS
```

我们可以看到这个函数占据了 20 字节的空间，因为名称末尾有 @20 装饰。这是合理的，因为该函数接收了两个 **double**（双精度）参数（每个 8 字节）和一个 **float**（单精度）参数（4 字节）。总共是 20 字节。无需深入分析代码，一眼就能看出有一个寄存器被访问了：ebp。这看起来很奇怪，考虑到 FASTCALL 通过寄存器传递参数。但事实并非如此：所有浮点参数（甚至是 32 位的 z）都是在栈上传递的。我们通过观察代码知道这一点，因为没有其他参数来源。

# 调用约定

注意在 CDECL 示例中，fmul 是最后执行的指令。我们不需要深入研究就能推断出结果传递到了浮点栈。同样注意到 x (偏移 [ebp + 8])、y (偏移 [ebp + 16]) 和 z (偏移 [ebp + 24]) 是反序入栈的：这意味着浮点参数是从右到左传递的。这与 CDECL 代码完全相同，尽管我们使用的是浮点值。这里是 MyFunction2 的 GCC 汇编：

```
.align 8
LC5:
  .long 0
  .long 1073741824
.align 8
LC6:
  .long 0
  .long 1074266612
  .glob @MyFunction20
  .def @My2020; .type 32; .endf
@MyFunction220:
  push %ebp
  movl %esp, %ebp
  subl $16, %esp
  fstpl -8(%ebp)
  fld 16(%ebp)
  fstpl -10(%ebp)
  fld
  fadd %st, xst(1)
  fld -6(%ebp)
LC5:
  fadd %st, xst(1)
  fmul 24(%ebp)
LC6:
  fadd %st, xst(1)
  fmul
  leave
```

这是一这是一段棘手的代码，但幸运的是我们不需要读得很仔细。首先，注意除了 ebp 之外没有访问其他寄存器。再次，GCC 将所有浮点值（32 位的 z）传递在栈上。同样，浮点值传递到了浮点栈顶。

我们可以看到 GCC 在开头做了一些奇怪的操作，从栈 [ebp + 8] 和 [ebp + 16] 取值，并将它们移动到 [ebp - 8] 和 [ebp - 16]。在移动后，这些值被加载到浮点栈并进行运算。z 直到后面才加载，尽管存在这种模式，它从未移动到 [ebp - 24]。LC5 和 LC6 很可能代表浮点值（因为数字本身 1073741824 和 1074266612 在我们的示例上下没有任何意义）。注意 LC5 和 LC6 都包含两个 .long 项，总共 8 字节。因此它们绝对是 double 值。

# 21.2.3 STDCALL

这里是 MyFunction 的 c.exe 列表：

```
PUBLIC      MyFunction3#20
PUBLIC      __real83ff000000000000
PUBLIC      __real8400000000000000
PUBLIC      __real848000000000000
EXTRN           floatused:NEAR
CONST           COMDAT          __real83ff000000000000
                               SEGMENT
CONST           __real83ff000000000000 DQ 03ff000000000000r ; 1
                                ENDS
CONST           COMDAT          _
                               SEGMENT
CONST           __real8400000000000000 DQ 0400000000000000r ; 2
                                ENDS
CONST           COMDAT          _
                               SEGMENT
CONST           __real8480000000000000 DQ 0400000000000000r ; 3
                                ENDS
TEXT            _
x$ = 8                                     ; size = 8
y$ = 16                                     ; size = 8
z$ = 24                                     ; size = 4
@MyFunction2020 PROC NEAR
; Line 7
    mov             ebp, ebp
; Line 8
    fld             QWORD PTR y$[ebp]
    fadd            QWORD PTR [__real83ff000000000000]
    fld             QWORD PTR [__real8400000000000000]
    fmul            QWORD PTR ST(1)
    fld             QWORD PTR [ebp]
    fadd            QWORD PTR [__real8480000000000000]
    fmul            ST(1), ST(0); Line 9
    pop             ebp
    set             20                              ; 0000014H
@MyFunction20 END
TEXT            ENDS
```

x 在栈的顶端，z 在栈的底部，因此这些参数是从右到左传递的。我们可以看出 x 是最小的偏移（偏移 +8），而 z 是最大的偏移（偏移 +24）。我们同样在最后一条 fmul 指令中看到结果在浮点栈上。该函数也根据需要清理栈，通过调用 `ret` 实现。它清理了栈上的 20 字节，碰巧也就是我们最初传递的总量。

我们还可以注意到，该函数的实现方式与该函数的 FASTCALL 版本完全相同。这是因为 FASTCALL 只通过寄存器传递 DWORD 大小的的参数，而浮点数不符合条件。这意味着我们上面的假设是正确的。

这里是 MyFunction3 的 GCC 列表：

```
.LC9:
    align 8
  .long 0
```

