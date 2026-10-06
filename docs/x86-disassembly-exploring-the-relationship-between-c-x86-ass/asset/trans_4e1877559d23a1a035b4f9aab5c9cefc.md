

```
abc123 = pointer to object      offset
mov eax, [abc123]      eax = eax        offset = abc123+0*word_size
      abc123
mov ebx, [abc123+4]   ebx = ebx       offset = abc123+2*word_size
      abc123+4
mov ecx, [abc123+8]   ecx = ecx        offset = abc123+4*word_size
      abc123+8
```

**图 3：** 这展示了如何对指针进行偏移，并将变量 'a' 的地址取到 eax 中。第二行将变量 'b' 的地址放入 ebx 中。最后一行将变量 'c' 放入 ecx 中。

## 20.2.2 方法

在底层，函数（function）和方法（method）之间几乎没有区别。在反编译时，有时看起来很难区分两者。它们存在于文本内存空间，且调用方式也相同。方法调用的示例可以参见**图 4**。

A:

```
//method call
abc123->foo(1, 2, 3);
```

B:

```
push 3               ; int c
push 2               ; int b
push 1               ; int a
push [ebp-4]        ; 对象的地址
call 0x00434125      ; 调用到方法
```

**图 4：** C++ 语法下的一种方法调用。abc123 是指向拥有方法 foo() 的对象的指针。foo() 接受三个整数参数：1、2 和 3。

**图 4.B** x86 汇编语言中的相同方法调用。它接受四个参数：对象的地址和三个整数。指向对象的指针位于 ebp-4 和 00434125 处。

方法调用的一个显著特征是，作为参数传递的是一个对象的地址。然而，这并不总是一个好的判断依据。**图 5** 显示了一个第一个参数为引用传递的对象的函数。其结果是一个看起来与方法调用一模一样的函数。

A:

```
//function call
foo(abc123, 1, 2, 3);
```

B:

```
push 3               ; int c
push 2               ; int b
```

# 对象与类

```
push 1
push [ebp-4]
call 0x00498372
; int a
; 对象的地址
; 调用到函数
```

图 5：一个函数调用。
图 5.A：C++ 语法下的函数调用。foo() 接受四个参数：一个指针和三个整数。
图 5.B：x86 汇编中的相同调用。它接受四个参数：对象的地址和三个整数。指向对象的指针在 ebp-4，而方法在地址 0x00498372 处。

## 20.2.3 继承与多态

继承和多态完全改变了类的结构，对象不再仅仅包含变量，还包含了指向所继承方法的指针。这是由于多态需要在运行时确定主对象或内部对象的地址。

考虑图 6。应用程序如何知道要调用 `D::one` 还是 `C::one`？答案是编译器使用了一种约定，在对象内部对变量和方法指针进行排序，使得当它们被引用时，任何继承了其方法和变量的对象，其偏移量都是相同的。

```
* obj[2];
obj[0] = new C();
[1] = new D();

for(int i=0; i<2; i++)
obj[i]->one();
```

图 6：一个简单的 C++ 多态循环，它调用了函数 `one`。类 C 和 D 都继承自抽象类 A。为了让这段代码运行，类 A 必须有一个名为 "one" 的虚方法。

抽象类 A 充当编译器的蓝图，为 A 中的任何类定义了预期的结构，并且 A 中定义的每个虚方法对于任何子类都具有完全相同的偏移量。图 7 详细说明了一种可能的继承方案及其在内存中的存储方式。注意 `C::one` 的偏移量与 `D::one` 相同，且 C 的 A::a 拷贝的偏移量与 D 的拷贝相同。此时，我们的多态循环只需要遍历指针数组，就能确切知道在哪里找到每个方法。

A:

```cpp
class A{
public:
	int a;
	virtual void one() = 0;
};
class B {
public:
  int b;
  int c;
  virtual void two() = 0;
};
class C : public A {
public:
  int d;
  void one();
};
class D : public A, public B {
public:
  int e;
  void one();
  void two();
};
```

| 对象 C | 偏移 | 值 | 描述 |
| :--- | :--- | :--- | :--- |
| 0x00200000 | dd | 0x00423848 | C:: 的地址; 偏移 = word_size |
| 0x00200004 | dd | 1 | C 对 A:: 的拷贝; 偏移 = |
| 0x00200008 | dd | 4 | C::d; 偏移 = 4*word_size |

| 对象 D | 偏移 | 值 | 描述 |
| :--- | :--- | :--- | :--- |
| 0x00200100 | dd | 0x00412348 | D::one 的地址; 偏移 = word_size |
| 0x00200104 | dd | 1 | D 对 A:: 的拷贝; 偏移 = word_size |
| 0x00200108 | dd | 0x00431255 | D::two 的地址; 偏移 = 4*word_size |
| 0x002001BC | dd | 2 | D 对 B:: 的拷贝; 偏移 = 6*word_size |
| 0x00200110 | dd | 3 | D 对 B::c 的拷贝; 偏移 = 8*word_size |
| 0x00200114 | dd | 5 | D::e; 偏移 = 10*word_size |

图 7：一种多态方案。图 7.A 定义了继承方案，显示了类 C 继承类 A，而类 D 继承类 A 和类 B。图 7.B 展示了继承方案在内存中可能的结构。类 C 的对象在前两个双字中包含了类 A 中声明的所有内容。对象的其余部分由 C 定义。类 D 的对象在前两个双字中包含了类 A 中声明的所有内容。接下来的三个双字在 B 中声明。最后一个双字由 D 定义。

## 20.3 类对比 结构体

## 21 浮点数

本页将介绍浮点数在汇编语言中如何使用。本页将不会讨论构造函数，而是会解释 FPU 指令的作用、浮点数如何被存储或处理，以及浮点数据之间的差异。然而，本页将演示浮点数如何在我们已经考虑过的代码和结构中使用。x86 架构没有专门用于浮点数的寄存器，但确实有用于它们的栈。浮点栈是直接构建在处理器中的，且与普通栈类似。

## 21.2 调用约定

通过栈传递浮点数时，我们将这些调用约定以及它们如何受到浮点栈的影响。

__cdecl 约定：

```cpp
push 3               ; int c
push 2               ; int b
push 1               ; int a
push [ebp-4]        ; 对象的地址
call 0x00434125      ; 调用到方法
```

fastcall 约定：

```cpp
push 3               ; int c
push 2               ; int b
```

stdcall 约定：

```cpp
push 1
push [ebp-4]
call 0x00498372
; int a
; 对象的地址
; 调用到函数
```

图 5：一个函数调用。
图 5.A：C++ 语法下的函数调用。foo() 接受四个参数：一个指针和三个整数。
图 5.B：x86 汇编中的相同调用。它接受四个参数：对象的地址和三个整数。指向对象的指针在 ebp-4，而方法在地址 0x00498372 处。

## 21.2.1 CDECL

这里是 MyFunction 的汇编列表：

```assembly
PUBLIC      MyFunction
PUBLIC      _real3f0000000000000
PUBLIC      _real400000000000000
PUBLIC      _real400800000000000
EXTERN      _fused NEAR
            DATA      _real3f0000000000000
                        SEGMENT
            DB      03f0000000000000 ; 1
                        ENDS
            DATA      _real400000000000000
                        SEGMENT
            DB      0400000000000000 ; 2
                        ENDS
            DATA      _real400800000000000
                        SEGMENT
            DB      0400800000000000 ; 3
                        ENDS
            TEXT
            _x = 8
            _y = 16
            _z = 24
_MyFunction PROC NEAR
    Line 2
        push    eb
        mov     eb, esp
    Line 3
        fld     QWORD PTR _z[eb]
        fld     QWORD PTR _real3f0000000000000
        fadd    QWORD PTR _y[eb]
        fld     QWORD PTR _real400000000000000
        fmul    ST(0), ST(0)
        fld     QWORD PTR _z[eb]
        fadd    QWORD PTR _real400800000000000
        fmul    ST(0), ST(0)
    Line 4
        pop     eb
        ret     0
_MyFunction ENDP
ENDS
```

GCC 不使用这些指令来创建这些函数，而是使用 /Gd、/Gr 和 /Gz 选项分别编译。

