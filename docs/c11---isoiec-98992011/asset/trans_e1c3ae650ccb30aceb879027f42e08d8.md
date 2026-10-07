

# ISO/IEC 9899:2011 (E)

© ISO/IEC 2011 – 版权所有

```c
extern int *x;
extern int y[];
```

第一个声明 x 为指向 int 的指针；第二个声明 y 为一个大小未指定的 int 数组（不完全类型），其存储在别处定义。

- **9 示例 3** 下面的声明演示了变体类型（variably modified types）的兼容性规则。

```c
extern int n;
extern int m;
void fcomp(void)
{
    int a[n] [6][m];
    int (*p) [4] [n+1];
    int c[n] [6][m];
    int (*r) [n] [n+1];
    p = a; // 无效：不兼容，因为 4 != 6
    r = c; // 兼容，但仅当 n=6 且 m=n+1
}
```

- **10 示例 4** 所有对变体类型（VM）的声明都必须处于作用域范围（scope scope）或原型作用域（prototype scope）。使用 Thread_local、static 或 extern 存储类说明声明的数组对象不能具有变长数组（VLA）类型。然而，使用 static 存储类说明声明的对象可以具有 VM 类型（即指向 VLA 的指针）。最后，所有具有 VM 类型的标识符必须是普通标识符，因此不能是结构体或联合体的成员。

```c
extern int n; // 无效：文件作用域 VLA
int A[n]; // 无效：文件作用域 VM
extern int (*p2) [n]; // 无效：文件作用域但不是 VM
int B[100];

void fla(int m, int C[m]); // 有效：原型作用域 VLA
void fva(int m, int C[m]) // 有效：调整为指向 VLA 的指针
{
    typedef int VLA[m][m]; // 有效：块作用域 VLA
    struct tag {
        int (*y) [n]; // 无效：y 不是普通标识符
        int z[n]; // 无效：z 不是普通标识符
    } D[m]; // 有效：自动 VLA
    static int E[m]; // 有效：静态块 VLA
    extern int F[m]; // 无效：F 有链接且是 VLA
    int (*s) [m]; // 有效：指向 VLA 的自动指针
    extern int (*r) [m]; // 无效：r 有链接且指向 VLA
    static int (*q) [m] = &B; // 有效：q 是指向 VLA 的静态块指针
}
```



前向引用：函数声明（6.7.6.3）、函数定义（6.9.1）、初始化（6.7.9）。

## 6.7.6.3 函数声明符（包括原型）

约束

- 1 声明符不应指定一个类型为函数类型或数组类型的返回类型。
- 2 在参数声明中，唯一出现的唯一存储类说明符是 register。
- 3 在函数声明符中，若不是该函数定义的一部分，标识符列表应为空。
- 4 调整后，作为函数定义部分的函数声明符中参数类型列表的参数不应具有不完全类型。

语义

- 5 如果在声明“T D1”中，D1 的形式为：
  D ( parameter-type-list )
  或
  D ( identifier-list-opt )
  且声明“T D”中为 ident 指定的类型为“derived-declarator-type-list T”，那么为 ident 指定的类型为“返回 T 的派生声明符列表函数”。
- 6 参数类型列表列出了函数参数的类型，并可能为这些参数声明标识符。
- 7 将声明为“类型为...的数组”的参数调整为“指向...类型的限定指针”，其中类型限定符（若有）在数组类型推导的 [ ] 内指定。如果关键字 static 同样出现在数组类型推导的 [ ] 内，则对于函数的每次调用，相应实际参数的值应提供对具有与大小表达式指定的相同数量的数组第一个元素的访问权限。
- 8 将声明为“返回...类型的函数”的参数应调整为“指向返回类型的指针”，如 6.3.2.1。
- 9 如果以省略号（ , ... ）结束，则不提供关于逗号后参数数量或类型的信息。
- 10 特殊情况，将 void 无名参数作为列表中的唯一项表示没有参数。

