

```
int* p1 = v2+2; // p1 = &v2[2]
int* p2 = v2-2; // *p2 undefined
}
```

复杂的指针运算通常是不必要的，最好避免。指针的加法没有意义也不被允许。

数组不是自描述的，因为数组的元素个数不保证与数组一起存储。这意味着要遍历一个不包含像 C 风格字符串那样的终止符的数组，我们必须以某种方式提供元素个数。例如：

```
void fp(char v[], int size)
{
for (int i=0; i!=size; ++i)
use(v[i]); // hope that v has at least size elements
for (int x : v)
use(x); // error :range-for does not work for pointers

const int N = 7;
char v2[N];
for (int i=0; i!=N; ++i)

use(v2[i]);
for (int x : v2)
use(x); // range-for works for arrays of known size
```

这种数组概念本质上是低级的。通过使用标准库容器 array (§8.2.4, §34.2.1) 可以获得内置数组的大部分优点和很少的缺点。某些 C++ 实现为数组提供可选的范围检查。然而，这种检查可能相当昂贵，因此通常仅用作开发辅助工具（而不是包含在生产代码中）。如果你不为单个访问使用范围检查，尝试保持一致的策略，只在定义良好的范围内访问元素。这最好在通过更高级别的容器类型的接口操作数组时完成，例如 vector，在这种情况下，很难对有效元素的范围感到困惑。

## 7.4.2 多维数组

多维数组表示为数组的数组；一个 3×5 的数组声明如下： int ma[3][5]; // 3 个数组，每个有 5 个 int
我们可以这样初始化 ma：

```
void init_ma()
{
for (int i = 0; i!=3; i++) for (int j = 0; j!=5; j++) ma[i][j] = 10*i+j; }
or graphically:
ma: 00 01 02 03 04 10 11 12 13 14 20 21 22 23 24
```

数组 ma 只是我们作为 3 个包含 5 个 int 的数组访问的 15 个 int。特别是，内存中没有单个对象是矩阵 ma —— 只有元素被存储。

维度 **3** 和 **5** 仅存在于编译器源代码中。当我们编写代码时，我们的工作是 somehow 记住它们并在需要时提供维度。例如，我们可以这样打印 `ma`：

```
void print_ma()
{
for (int i = 0; i!=3; i++) {
for (int j = 0; j!=5; j++)
cout << ma[i][j] << '\t';
cout << '\n';
}
}
```

在某些语言中用于数组边界的逗号记法不能在 C++ 中使用，因为逗号 (,) 是一个序列运算符 (§10.3.2)。幸运的是，大多数错误都被编译器捕获。例如：

```
int bad[3,5];
int good[3][5];
int ouch = good[1,4]; int nice = good[1][4];

// error : comma not allowed in constant expression
// 3 arrays with 5 ints each
// error : int initialized by int* (good[1,4] means good[4], which is an int*)
```

## 7.4.3 传递数组

数组不能直接按值传递。相反，数组作为指向其第一个元素的指针传递。例如：

```
void comp(double arg[10]) // arg is a double*
{
for (int i=0; i!=10; ++i) arg[i] +=99;
}

void f() {
double a1[10]; double a2[5]; double a3[100];

comp(a1);
comp(a2); // disaster!
comp(a3); // uses only the first 10 elements
};
```

这段代码看起来合理，但事实并非如此。代码可以编译，但调用 `comp(a2)` 将会写出 `a2` 的边界之外。此外，任何猜测数组是按值传递的人都会失望：对 `arg[i]` 的写入是直接写入 `comp()` 参数的元素，而不是写入副本。该函数也可以等价地写成

```
void comp(double* arg)
{
```

```
for (int i=0; i!=10; ++i)
arg[i]+=99;
}
```

现在这种荒谬性（希望）是显而易见的。当用作函数参数时，数组的第一个维度简单地被视为指针。指定的任何数组边界都将被忽略。这意味着如果你想在不丢失大小信息的情况下传递一系列元素，就不应该传递内置数组。相反，你可以将数组作为成员放在类中（如对 std::array 所做的那样）或定义一个充当句柄的类（如对 std::string 和 std::vector 所做的那样）。

如果你坚持直接使用数组，你将不得不处理错误和混淆，而得不到明显的优势。考虑定义一个用于操作二维矩阵的函数。如果维度在编译时已知，就没有问题：

```
void print_m35(int m[3][5])
{
for (int i = 0; i!=3; i++) {
for (int j = 0; j!=5; j++) cout << m[i][j] << '\t'; cout << '\n';
}
```

第 7.4.3 节 传递数组 185

作为多维数组表示的矩阵是作为指针传递的（而不是复制；§7.4）。数组的第一个维度与查找元素的位置无关；它只是说明存在多少个适当类型的元素（这里是 int[5]）。例如，查看上面 ma 的布局并注意，仅知道第二个维度是 5，我们就可以定位任意 i 的 ma[i][5]。因此，第一个维度可以作为参数传递：

```
void print_mi5(int m[][5], int dim1)
{
for (int i = 0; i!=dim1; i++) {
for (int j = 0; j!=5; j++)
cout << m[i][j] << '\t';
cout << '\n';
}
}
```

当两个维度都需要传递时，“显而易见的解决方案”不起作用：

```
void print_mij(int m[][], int dim1, int dim2) // doesn’t behave as most people would think {
for (int i = 0; i!=dim1; i++) {
for (int j = 0; j!=dim2; j++)
cout << m[i][j] << '\t'; // sur prise!
cout << '\n';
}
}
```

幸运的是，参数声明 m[][] 是非法的，因为为了找到元素的位置，多维数组的第二个维度必须已知。

然而，表达式 m[i][j] 被（正确地）解释为 *(* (m+i)+j)，尽管这可能不是程序员的本意。正确的解决方案是：

```
void print_mij(int* m, int dim1, int dim2)
{
for (int i = 0; i!=dim1; i++) {
for (int j = 0; j!=dim2; j++)
cout << m[i*dim2+j] << '\t'; // obscure
cout << '\n';
}
}
```

在 print_mij() 中用于访问成员的表达式等价于编译器在知道最后一个维度时生成的表达式。

要调用此函数，我们将矩阵作为普通指针传递：

```
int test()
{
int v[3][5] = {
{0,1,2,3,4}, {10,11,12,13,14}, {20,21,22,23,24} ;
print_m35(v);
print_mi5(v,3);
print_mij(&v[0][0],3,5);
}
```

注意最后一次调用中使用了 &v[0][0]；v[0] 也会起作用，因为它等价，但 v 会是类型错误。这种微妙而混乱的代码最好被隐藏。如果你必须直接处理多维数组，请考虑封装依赖于它的代码。以这种方式，你可能会减轻下一个触及该代码的程序员的任务。提供一个具有适当下标运算符的多维数组类型可以让大多数用户不必担心数组中数据的布局 (§29.2.2, §40.5.2)。

标准 vector (§31.4) 不会遭受这些问题。

## 7.5 指针和 const

C++ 对“常量”提供了两种相关的含义：

- **constexpr**: 在编译时求值 (§2.2.3, §10.4)。
- **const**: 在此作用域内不修改 (§2.2.3)。

基本上，constexpr 的作用是启用并确保编译时求值，而 const 的主要作用是指定接口中的不可变性。本节主要关注第二种作用：接口规范。

许多对象在初始化后其值不会被更改：

- 使用符号常量比在代码中直接使用文字更易于维护。
- 许多指针经常被读取但从不通过它们写入。
- 大多数函数参数是只读不写的。

为了表达这种初始化后不可变的概念，我们可以在对象的定义中添加 const。例如：

```
const int model = 90; const int v[] = { 1, 2, 3, 4 }; const int x;
```

```
// model is a const // v[i] is a const
// error : no initializer
```

因为声明为 const 的对象不能被赋值，所以它必须被初始化。声明某物为 const 确保其值在其作用域内不会改变：

```
void f()
{
model = 200; // error
v[2] = 3; // error
}
```

请注意 const 修改一个类型；它限制了对象的使用方式，而不是指定常量的分配方式。例如：

```
void g(const X* p)
{
// can’t modify *p here
```

第 7.5 节 指针和 const 187

```
void h() {
X val; // val can be modified here
g(&val);
// ...
}
```

在使用指针时，涉及两个对象：指针本身和指向的对象。“前缀”指针声明的 const 使对象而不是指针成为常量。要声明指针本身而不是指向的对象为常量，我们使用声明符运算符 *const 而不是普通的 *。例如：

```
void f1(char* p) {
char s[] = “Gorm”;

const char * pc = s; pc[3] = ‘g’;
pc = p;

// pointer to constant
// error :pc points to constant // OK

char *const cp = s; cp[3] = ‘a’;
cp = p;

// constant pointer // OK
// error :cp is constant

const char *const cpc = s; cpc[3] = ‘a’;
cpc = p;
}
```

```
// const pointer to const
```
