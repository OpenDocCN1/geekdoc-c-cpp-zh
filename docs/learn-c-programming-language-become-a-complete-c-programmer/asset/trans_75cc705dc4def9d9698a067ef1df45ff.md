

```cpp
while (*q!=0){
*p++ = *q++;
}
*p=0; // terminating zero
```

**`*p++ = *q++`** 的值是 **`*q`**。因此我们可以将示例重写如下：

```cpp
while ((*p++ = *q++) != 0) { }
```

在这种情况下，我们在已经将 **`*q`** 复制到 **`*p`** 并递增了 **`p`** 之后，才注意到 **`*q`** 为零。因此，我们可以消除对终止零的最后一次赋值。最后，通过观察我们不需要空块，并且 **`!=0`** 是多余的，因为积分条件的运算结果总是与零进行比较，我们可以进一步简化示例。于是，我们得到了我们要发现的版本：

```cpp
while (*p++ = *q++);
```

这个版本比之前的版本可读性更差吗？对有经验的 C 或 C++ 程序员来说，并不是。 这个版本在时间和空间上比之前的版本更高效吗？除了第一个调用了 **`strlen()`** 的版本之外，并不是；性能是等效的，并且通常会生成相同的代码。

复制以零结尾的字符字符串最有效的方法通常是标准的 C 风格字符串复制函数：

```cpp
char * strcpy(char*, const char*); // from <string.h>
```

对于更一般的复制，可以使用标准的 **`copy`** 算法（§4.5, §32.5）。在可能的情况下，优先使用标准库设施，而不是摆弄指针和字节。标准库函数可能会被内联（§12.1.3）甚至使用专门的机器指令实现。因此，在相信某段手工编写的代码优于库函数之前，你应该仔细测量。即使它确实更好，这种优势在其他硬件+编译器组合上可能不存在，而且你的替代方案可能会给维护者带来头痛。

## 11.2 Free Store

命名对象的生命周期由其作用域决定（§6.3.4）。然而，通常很有用的是创建一个与创建它的作用域无关而存在的对象。例如，创建在创建它们的函数返回后仍可使用的对象是很常见的。运算符 **`new`** 创建此类对象，而运算符 **`delete`** 可用于销毁它们。由 **`new`** 分配的对象被称为“在 *free store* 上”（也称为“在 *heap* 上”或“在 *dynamic memory* 中”）。

考虑我们如何以与台式计算器（§10.2）使用的风格编写编译器。语法分析函数可能会构建表达式树供代码生成器使用：

```cpp
struct Enode {
Token_value oper;
Enode* left;
Enode* right;
// ...
```
};
Enode* expr(bool get) {
Enode* left = term(get);
for (;;) {
switch (ts.current().kind) {
case Kind::plus:
case Kind::minus:
left = new Enode {ts.current().kind,left,term(true)};
break;
default:
return left; // returnnode
}
}
}
```

在 Kind::plus 和 Kind::minus 情况下，会在 free store 上创建一个新的 Enode 并通过值 {ts.current().kind,left,term(true)} 初始化它。 resulting 指针被赋给 left 并最终从 expr() 返回。

我使用了 {}-list 记法来指定参数。或者，我也可以使用旧式的 ()-list 记法来指定初始化器。然而，尝试对使用 new 创建的对象使用 = 记法进行初始化会导致错误：

```
int * p = new int = 7; // error
```

如果一个类型有默认构造函数，我们可以省略初始化器，但内置类型默认是未初始化的。例如：

```
auto pc = new complex<double>; auto pi = new int;
// the complex is initialized to {0,0} // the int is uninitialized
```

这可能会令人困惑。为了确保获得默认初始化，请使用 {}。例如： auto pc = new complex<double>{}; // the complex is initialized to {0,0} auto pi = new int{}; // the int is initialized to 0

代码生成器可以使用 expr() 创建的 Enodes 并删除它们：

```
void generate(Enode * n)
{
switch (n->oper) {
case Kind::plus:
// use n
delete n; // delete an Enode from the free store
}
}
```

由 new 创建的对象存在，直到它被 delete 显式销毁。然后，它占用的空间可以被 new 重用。C++ 实现不保证存在“垃圾收集器”，它会查找未引用的对象并使其可供 new 重用。因此，我假设使用 new 创建的对象会手动使用 delete 释放。

### Section 11.2 Free Store 279

**delete** 运算符只能应用于由 **new** 返回的指针或 **nullptr**。对 **nullptr** 应用 **delete** 没有效果。
如果被删除的对象是具有析构函数（§3.2.1.2, §17.2）的类，则在对象的内存被释放以供重用之前，**delete** 会调用该析构函数。

### 11.2.1 Memory Management

free store 的主要问题是：

- *Leaked objects*: 人们使用 **new** 然后忘记 **delete** 分配的对象。
- *Premature deletion*: 人们 **delete** 了他们还有其他指针指向的对象，然后后来使用该其他指针。
- *Double deletion*: 一个对象被删除两次，调用其析构函数（如果有）两次。

泄漏的对象可能是一个严重的问题，因为它们可能导致程序耗尽空间。过早删除几乎总是很糟糕的问题，因为指向“已删除对象”的指针不再指向有效对象（因此读取它可能会产生错误结果），并且可能确实指向已被重用于另一个对象的内存（因此写入它可能会破坏不相关的对象）。考虑这个非常糟糕的代码示例：

```
int * p1 = new int{99};
int* p2 = p1;
delete p1;
p1 = nullptr;
char* p3 = new char{'x'}; *p2 = 999;
cout << *p3 << '\n';
```

// potential trouble
// now p2 doesn't point to a valid object
// gives a false sense of safety
// p3 may now point to the memory pointed to by p2 // this may cause trouble
// may not print x

双重删除是一个问题，因为资源管理器通常无法跟踪代码对资源的拥有情况。考虑：

```
void sloppy() // very bad code
{
int* p = new int[1000]; // ... use *p ...
delete[] p;

// acquire memory
// release memory
// ... wait a while ...
delete[] p; }
// but sloppy() does not own *p
```

到第二次 **delete[]** 时，*p 指向的内存可能已被重新分配用于其他用途，并且分配器可能会被破坏。用 string 替换该示例中的 int，我们会看到 string 的析构函数试图读取已被重新分配并可能被其他代码覆盖的内存，并使用读取的内容尝试删除内存。总之，双重删除是未定义行为，结果不可预测且通常是灾难性的。

人们犯这些错误的原因通常不是恶意，而且往往也不是简单的粗心；在一大程序中始终释放每个已分配对象是真正困难的（并且恰好在计算的正确点释放一次）。首先，对程序的局部部分进行分析将检测不到这些问题，因为错误通常涉及多个独立部分。

作为使用“裸” new 和 delete 的替代方案，我可以推荐两种避免此类问题的资源管理通用方法：

- [1] 如果你不需要，就不要把对象放在 free store 上；优先使用作用域变量。
- [2] 当你在 free store 上构造一个对象时，将其指针放入一个管理器对象（有时称为句柄）中，该管理器对象具有将在销毁时销毁它的析构函数。示例有 string、vector 和所有其他标准库容器、unique_ptr（§5.2.1, §34.3.1）以及 shared_ptr（§5.2.1, §34.3.2）。在可能的情况下，让该管理器对象成为作用域变量。许多对 free store 的经典使用可以通过使用移动语义（§3.3, §17.5.2）将作为管理器对象的较大对象从函数返回来消除。这种规则 [2] 通常被称为 RAII（“Resource Acquisition Is Initialization”；§5.2, §13.3），它是避免资源泄漏并使使用异常进行错误处理变得简单和安全的基本技术。

标准库 vector 是这些技术的示例：

```
void f(const string& s)
{
vector<char> v;
for (auto c : s)
v.push_back(c);
// ...
}
```

vector 将其元素保存在 free store 上，但它自行处理所有分配和释放。在此示例中，push_back() 执行 new s 以获取其元素的空间，并执行 delete s 以释放不再需要的空间。然而，vector 的用户无需了解这些实现细节，只需依赖 vector 不会泄漏即可。

计算器示例中的 Token_stream 是另一个更简单的示例（§10.2.2）。在那里，用户可以使用 new 并将 resulting 指针交给 Token_stream 管理：

```
Token_stream ts{new istringstream{some_string}};
```

我们不需要仅仅为了从函数中获取一个大对象而使用 free store。例如：

```
string reverse(const string& s)
{
string ss;
for (int i=s.size()-1; 0<=i; --i)
```

