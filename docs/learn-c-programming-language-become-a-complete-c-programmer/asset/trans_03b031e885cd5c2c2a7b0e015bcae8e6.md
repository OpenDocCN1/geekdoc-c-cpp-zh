

此外，constexpr 函数不能有副作用。也就是说，constexpr 函数是一个纯函数。例如：

```
int glob;
constexpr void bad1(int a) // error :constexpr function cannot be void
{
glob = a; // error :side effect in constexpr function
}
constexpr int bad2(int a)
{
if (a>=0) return a; else return -a;
}
// error :if-statement in constexpr function
constexpr int bad3(int a) {
sum = 0;
for (int i=0; i<a; +=i) sum +=fac(i); return sum;
}
// error : local variable in constexpr function // error :loop in constexpr function
```

constexpr 构造函数的规则有所不同（§10.4.3）；在那里，只允许对成员进行简单的初始化。

constexpr 函数允许递归和条件表达式。这意味着如果你真的想的话，你可以用 constexpr 函数表达几乎任何东西。然而，你会发现除非你将 constexpr 函数的使用限制在它们 intended 的相对简单的任务上，否则调试会变得不必要地困难，并且编译时间会比你希望的更长。

通过使用字面值类型（§10.4.3），constexpr 函数可以被定义为使用用户定义的类型。像内联函数一样，constexpr 函数遵循 ODR（“一个定义规则”），因此不同翻译单元中的定义必须相同（§15.2.3）。你可以将 constexpr 函数视为内联函数（§12.1.5）的一种受限形式。

## 12.1.6.1 constexpr 和引用

constexpr 函数不能有副作用，因此写入非局部对象是不可能的。然而，constexpr 函数可以引用非局部对象，只要它不写入它们。

```
constexpr int ftbl[] { 1, 2, 3, 5, 8, 13 };
constexpr int fib(int n)
{
return (n<sizeof(ftbl)/sizeof(*ftbl)) ? ftbl[n] : fib(n);
}
```

constexpr 函数可以接受引用参数。当然，它不能通过此类引用写入，但 const 引用参数与以往一样有用。例如，在标准库（§40.4）中我们找到：

```
template<> class complex< float> { public:
// ...
explicit constexpr complex(const complex<double>&);
// ...
};
```

这允许我们写：

```
constexpr complex<float> z {2.0};
```

逻辑上为 const 引用参数构造的临时变量简单地成为编译器内部的值。

constexpr 函数可以返回引用或指针。例如：

```
constexpr const int * addr(const int& r) { return &r; } // OK
```

然而，这样做让我们远离了 constexpr 函数作为常量表达式求值的一部分的基本作用。特别是，确定此类函数的结果是否为常量表达式可能相当棘手。考虑：

```
static const int x = 5;
constexpr const int* p1 = addr(x); // OK
constexpr int xx = *p1; // OK
```

```
static int y;
constexpr const int* p2 = addr(y); // OK
constexpr int yy = *y; // error :attempt to read a variable
```

```
constexpr const int* tp = addr(5); // error :address of temporary
```

## 12.1.6.2 条件求值

在 constexpr 函数中，未被取的条件表达式的分支不会被求值。这意味着未被取的分支可能需要运行时求值。例如：

```
constexpr int check(int i)
{
return (low<=i && i<high) ? i : throw out_of_range();
}
```

```
constexpr int low = 0; constexpr int high = 99;
// ...
constexpr int val = check(f(x,y,z));
```

你可以想象 low 和 high 是在编译时已知但不在设计时已知的配置参数，并且 f(x,y,z) 计算某个实现相关的值。

initializer lists 的描述在 §12.2.3 中，以及向模板函数传递参数的方式在 §23.5.2 和 §28.6.2 中。

## 12.2.1 引用参数

考虑：

```
void f(int val, int& ref)
{
++val;
++ref;
}
```

当 f() 被调用时，++val 增加第一个实际参数的局部副本，而 ++ref 增加第二个实际参数。考虑：

```
void g()
{
int i = 1;
int j = 1;
f(i,j);
}
```

调用 f(i,j) 将增加 j 但不增加 i。第一个参数 i 按值传递；第二个参数 j 按引用传递。如 §7.7 中所述，修改按引用传递参数的函数会使程序难以阅读，通常应避免（但参见 §18.2.5）。然而，对于大型对象，按引用传递比按值传递明显更高效。在这种情况下，参数可能被声明为 const 引用以表明引用仅出于效率原因使用，而不是为了使被调用函数能够更改对象的值：

```
void f(const Large& arg)
{
// “arg” 的值不能被更改
// （除非使用显式类型转换；§11.5）
}
```

引用参数声明中缺少 const 被视为有意修改变量的声明：

```
void g(Large& arg); // 假设 g() 修改 arg
```

同样，声明指针参数为 const 告诉读者函数不会更改该指针指向的对象的价值。例如：

```
int strlen(const char *); // C 风格字符串中的字符数
char* strcpy(char* to, const char* from); // 复制 C 风格字符串
int strcmp(const char*, const char*); // 比较 C 风格字符串
```

随着程序规模的增大，使用 const 参数的重要性也随之增加。

请注意，参数传递的语义与赋值语义不同。这对于 const 参数、引用参数以及某些用户定义类型的参数很重要。

遵循引用初始化的规则，字面值、常量以及需要转换的参数可以作为 const T& 参数传递，但不能作为普通的（非 const）T& 参数传递。允许对 const T& 参数进行转换可确保此类参数可以获得与 T 参数完全相同的一组值，如果必要的话，通过在临时对象中传递值来实现。例如：

```
float fsqrt(const float&); // Fortran 风格的 sqrt 接受引用参数
void g(double d) {
float r = fsqrt(2.0f); r = fsqrt(r);
r = fsqrt(d);
}
// 传递对保存 2.0f 的临时对象的引用
// 传递对 r 的引用
// 传递对保存 static_cast<float>(d) 的临时对象的引用
```

禁止对非 const 引用参数进行转换（§7.7）可避免因引入临时对象而导致愚蠢错误的可能性。例如：

```
void update(float& i);
void g(double d, float r) {
update(2.0f); // error : const argument
update(r); // 传递对 r 的引用
update(d); // error :type conversion required
}
```

如果允许这些调用，update() 将悄悄地更新立即被删除的临时对象。通常，这对程序员来说会是一个不愉快的惊喜。

如果我们想精确一点，按引用传递将是按左值引用传递，因为函数也可以接受右值引用。如 §7.7 中所述，右值可以绑定到右值引用（但不能绑定到左值引用），左值可以绑定到左值引用（但不能绑定到右值引用）。例如：

```
void f(vector<int>&);
void f(const vector<int>&);
void f(vector<int>&&);
// （非 const）左值引用参数 // const 左值引用参数 // 右值引用参数
```

```
void g(vector<int>& vi, const vector<int>& cvi) {
f(vi); // 调用 f(vector<int>&)
f(cvi); // 调用 f(const vector<int>&)
f(vector<int>{1,2,3,4}); // 调用 f(vector<int>&&);
```

我们必须假设函数会修改右值参数，使其仅可用于销毁或重新赋值（§17.5）。右值引用的最明显用途是定义移动构造函数和移动赋值（§3.3.2，§17.5.2）。我确信有人会为 **const**-右值引用参数找到巧妙的用途，但到目前为止，我还没有看到真正的用例。

请注意，对于模板参数 **T**，模板参数类型推导规则使 **T&&** 与类型 **X** 的 **X&&** 有显著不同的含义（§23.5.2.1）。对于模板参数，右值引用最常用于实现“完美转发”（§23.5.2.1，§28.6.3）。我们如何选择参数传递的方式？我的经验法则是：[1] 对小型对象使用按值传递。[2] 使用按 **const**-引用传递来传递你不需要修改的大值。[3] 将结果作为 **return** 值返回，而不是通过参数修改对象。[4] 使用右值引用来实现移动（§3.3.2，§17.5.2）和转发（§23.5.2.1）。[5] 如果“无对象”是一个有效替代方案，则传递指针（并用 **nullptr** 表示“无对象”）。[6] 仅在必须时才使用按引用传递。

最后一条经验法则中的“当你必须时”指的是观察到传递指针通常是处理需要修改的对象（§7.7.1，§7.7.4）的一种比使用引用更不晦涩的机制。

## 12.2.2 数组参数

如果数组用作函数参数，则传递其初始元素的指针。例如：

```
int strlen(const char*);

void f()
{
  char v[] = “Annemarie”;
  int i = strlen(v);
  int j = strlen(“Nicholas”);
}
```

也就是说，类型为 **T[]** 的参数在传递时会被转换为 **T***。这意味着对数组参数的元素进行赋值会更改参数数组元素的价值。换句话说，数组与其他类型不同，数组不是按值传递的。相反，传递的是指针（按值）。

数组类型的参数等同于指针类型的参数。例如：

```
void odd(int * p);
void odd(int a[]);
void odd(int buf[1020]);
```

这三个声明是等价的，并声明了同一个函数。如 usual，参数名不影响函数的类型（§12.1.3）。传递多维数组的规则和技术可以在 §7.4.3 中找到。

