
```cpp
class Person {
    char d_name[80];
    char d_address[80];

public:
    void initialize(char const *nm, char const *adr);
    void print();
    // 等等
};
```

在 C++ 中，不使用结构体参数。C 函数可以这样调用：

```c
PERSON x;

initialize(&x, "some name", "some address");
```

## 3.3. C 语法的新增

### 3.3.1 引用

除了定义变量常用方式（普通变量或指针）外，C++ 还引入了变量的别名。对变量的引用就像别名；变量可以在语句中使用引用：

```cpp
int int_value;
int &ref = int_value;
```

在上面的示例中，定义了变量 `int_value`。随后定义了引用 `ref`（由于其初始化），它指向 `int_value` 相同的内存位置。在 `ref` 的定义中，`&` 运算符表示 `ref` 本身是一个引用。这两个语句：

```cpp
++int_value;
++ref;
```

效果相同：它们增加了 `int_value` 的值。无论调用 `int_value` 还是 `ref` 并不重要。引用在 C++ 中起重要作用，作为向函数传递可修改参数的方法。在标准 C 中，增加参数值的函数需要指针：

```c
void increase(int *valp)      // 期望指针
{
  *valp += 5;                   // 对于 int
}

int main() {
  int x;
  increase(&x);                // 传递 x 的地址
}
```

这种构造也可以用于 C++，但使用引用实现了相同的效果：

```cpp
void increase(int &valr)    // 期望引用
{
  valr += 5;                   // 对于 int
}
```

```cpp
int main() {
  int x;
  increase(x);    // 作为引用传递
}
```

可以说，`increase(x)` 语句建议传递的是拷贝，但 `x` 的值因为 `increase()` 的定义方式而改变了。然而，引用也可以用于传递那些仅被检查（不需要拷贝）或修改是副作用的对象。在这些情况下，引用强烈优于值或传递指针等替代方案。

在底层，对于编译器而言，引用是用指针实现的。然而，使用引用时，程序员并不知道间接层。普通指针和引用之间的一个重要区别是，引用没有发生间接。例如：

```cpp
extern int *ip;
extern int &ir;
ip = 0; // 分 ip，现在是一个指针
ir = 0; // ir 未改变，它指向的 int 变量现在是 0。
```

为了防止混淆，我们建议遵循以下：

- 在函数不更改其内置或指针类型参数的情况下，可以使用值参数：

```cpp
void some_func(int val) {
  cout << val << '\n';
}
```

```cpp
int main() {
  int x;
  some_func(x);    // 传递了一个拷贝
}
```

- 当函数必须显式更改参数的值时，选择指针参数。这些指针参数最好是函数的初始参数。这被称为按引用返回。

```cpp
void by_pointer(int *val) {
  *val += 5;
}
```

- 当函数没有改变其参数的值，或者如果参数的修改是微不足道的副作用（例如参数是一个流）时，可以使用引用。如果函数没有修改参数，应该使用常量引用：

```cpp
void by_reference(string &str) {
    cout << str; // 没有修改 str
}
int main() {
    int x = 7;
    by_pointer(&x); // 传递了一个指针
                    // x 可能会被改变
    string str("hello");
    by_reference(str); // str 没有改变
}
```

引用在函数没有更改参数但又不希望拷贝参数的情况下起着重要作用。这种情况通常发生在大型对象作为参数传递或由函数返回时。在这些情况下，复制操作往往成为一个显著因素，必须复制整个对象。在这些情况下，优选引用。

如果参数没有被函数修改，或者调用者不应该修改该信息，则应该使用 `const` 关键字。考虑以下示例：

```cpp
struct Person // 某些大型结构体
    char name[80];
    char address[90];
    double salary;
}
Person person[50]; // 人数据库
void printperson(Person const &subject) {
    // printperson 期望
    // 结构体的引用
    // 但不会改变它
    cout << "Name: " << subject.name << '\n'
         << "Address: " << subject.address << '\n';
}
Person const &personIdx(int index) // 根据索引值获取人员
{
    return person[index]; // 返回的是引用，
                          // 不是 person[index] 的拷贝
}
int main() {
    Person boss;
}
```

# 第 3 章 C++ 的初印象

```cpp
print(boss);      // 没有传递指针，
// 所以 'boss' 不会被
print(Idx(5));  // 通过引用修改，
// 而不是拷贝
```

此外，请注意在将对象作为函数参数传递时，使用引用的另一个原因。当传递对象的引用时，激活记录（activation record）的拷贝操作将在第 9 章中介绍。引用可能会导致“丑陋”的代码。函数可以返回一个变量的引用，如下例所示：

```cpp
int &func()
{
    static int value;
    return value;
}
```

这允许使用以下构造：

```cpp
func() = 20;
func() += func();
```

可能没必要说明不应该使用这种构造是多余的。尽管如此，在某些情况下是有用的。在我们之前讨论流（streams）时，实际上已经见过这种现象的例子。在像 `cout << "Hello" << '\n';` 这样的语句中，插入运算符返回的是 cout 的引用。因此，在该语句中，首先将 "Hello" 插入到 cout 中，产生一个 cout 的引用；然后将 '\n' 插入到 cout 中，产生一个 cout 的引用，而该引用被忽略了。

接下来的列表指指针和引用之间的几点区别：

- 引用不能独立存在，即没有没有指向的对象。
- 不允许出现像 `int &ref;` 这样的引用声明；ref 将指向什么？
- 引用可以声明为外部的（external）。这些引用在别处被初始化。
- 引用可以作为函数的参数存在：它们在函数被调用时初始化。在这些情况下，由函数决定返回值指向什么。
- 引用可以作为类的成员变量。
- 指针本身就是变量。它们指向某些东西或者什么都不指向。
- 引用是其他变量的别名，不能是另一个变量的别名。一旦定义了引用，它就指向那个特定的变量。

## 3.3 C++ 语法的若干补充

- 指针（`const` 除外）可以重新赋值指向不同的变量。
- 当取地址运算符 `&` 与引用一起使用时，表达式产生引用所作用变量的地址。相比之下，普通指针是变量，因此指针变量的地址与它所指向的地址没有关系。

### 3.3.2 右值引用

在 C++ 中，临时值（右值，rvalue）与 `const` 类型是不可区分的。C++ 引入了一种新的引用类型称为右值引用（rvalue reference），定义为 `&&`。rvalue 的名称源于赋值语句，赋值运算符左侧的变量被称为左值（lvalue）。右值通常是临时的、匿名的值，例如函数返回的值。在这些术语中，C++ 引用应该被视为左值引用（使用 `&`）。它们可以与右值引用（使用 `&&`）进行对比。

理解右值引用的关键在于匿名变量的概念。匿名变量没有名称，这是编译器理想地与右值引用操作的区分特征。在引入一些有趣的构造之前，让我们来看一些使用左值引用的标准情况。以下函数返回一个临时（匿名）值：

```cpp
int intVal() {
    return 5;
}
```

尽管 `intVal()` 的返回值可以赋值给 int 变量，但它需要拷贝，如果函数返回的不是 int 而是某个大对象，这种开销可能会变得不可接受。同样不能使用引用或指针来收集匿名右值引用作为返回值，因为返回值将存活。以下代码是非法的（编译器会指出）：

```cpp
int &ir = intVal();      // 失败：指向临时值
int const &ic = intVal();    // OK：不可变的临时值
int *ip = &intVal();         // 失败：没有可用的左值
```

显然，无法修改返回的临时值。但在引入一些有趣的构造之前，让我们看看这些函数：

```cpp
void receive(int &value)      // 左值引用
{
    cout << "value";
}
void receive(int &&value)     // 右值引用
{
    cout << "value";
}
```

在 `main` 函数中这样调用：

```cpp
int main()
{
    int value = 5;
    receive(value);  // 调用左值引用
    receive(intVal());////右值值
}
```

输出：
：
- 右值：
- 左值引用
- 右值引用

```cpp
void receive(intint &value)
{
    cout << "value";
}
void receive(int &&value)
{
    cout << "value";
}
```

### 3.3.3 Lvalues、rvalues 以及更多

尽管本节包含对第 5、7 和 16 章的前向引用，但其主题更适合当前章节。可以跳过本节而不影响连贯性，你可以在熟悉这些后续章节的内容后考虑返回此节。

从历史上看，C 编程语言区分了 lvalues（左值）和 rvalues（右值）。该术语基于赋值表达式，其中赋值运算符左侧的表达式接收一个值（例如，它指向一个可以写入该值的内存位置，如变量），而赋值运算符右侧的表达式必须表示一个值（它可以是一个临时变量、常量值或存储在变量中的值）：

```
lvalue = rvalue;
```

C++ 在此基础区分的基础上增加了几种引用表达式的新方式：

- *lvalue*: C++ 中 lvalue 的意义与 C 语言中相同。它指向一个可以存储值的位置，如变量、对变量的引用或解引的指针。
- *xvalue*: xvalue 表示即将过期的右值（expiring rvalue）。即将过期的右值指的是在其生命周期结束前的对象（参见第 7 章）。此类对象通常必须确保它们拥有的资源（如动态分配的内存）也停止存在，但在对象结束之前，这些资源可能会移动到另一个位置，从而防止它们的销毁。
- *glvalue*: 泛化左值（generalized lvalue）。泛化左值指的是任何可能接收值的实体。它要么是 lvalue 要是 xvalue。
- *prvalue*: prvalue 是纯右值（pure rvalue）：字面量值（如 1.2e3）或不可变对象（例如从返回常量 std::string 的函数返回的值，参见第 5 章）。

如果表达式满足以下条件，则其值值为 xvalue：

- 返回指向对象的右值引用的函数返回值；
- 被强制转换为右值引用的对象；
- 访问非静态类成员的表达式，其对象是：
    - 一个右值；
    - 一个**.**（成员指针）表达式（参见第 16 章），其中左侧操作数是 lvalue，右侧操作数是数据数据成员的指针。

此规则的效果是，命名的右值被视为 lvalues，而对象的匿名右值引用被视为 xvalues。
指向函数的右值引用无论是否匿名，都被视为 lvalues。

这里有一个小示例。考虑这个简单的结构结构体：

```
struct Demo
{
    int d_value;
};
```

## 3.3. 对 C 语法的若干补充

此外，我们还有这些函数声明和定义：

```
Demo &&operator+(Demo const &lhs, Demo const &rhs);
Demo &factory();
```

Demo demo;
Demo &rref = static_cast<Demo &&>(demo);

像下文所示的表达式

```
factory();
factory().*d_value;
static_cast<Demo &&>(demo);
demo + demo
```
