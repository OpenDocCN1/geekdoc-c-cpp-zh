
最简单的例子是：一个函数接受一个结构体作为参数，但该结构体在多年的开发中不断被扩展。假设它最初是这样的：

```
struct myStruct{
    int a;
    int b;
};
```

而函数是：

```
void myFunction(struct myStruct *myPointer){
    printf( "%d\n", myPointer->a);
    printf( "%d\n", myPointer->b);
}
```

现在假设后来该结构体被扩展以包含一个新字段，而这个字段对于项目的进一步发展至关重要：

```
struct myStructEx{
    int a;
    int b;
    int c;
};
```
好消息是，新函数可以使用新的结构体，而旧函数可以通过类型转换继续使用新的结构体，就像使用旧的结构体一样：

```
myFunction((struct myStruct *) myPointer);
```

其中 myPointer 现在是指向 myStructEx 的指针。显然，myFunction 并不知道扩展后的结构体，因此只会使用字段 a 和 b。这是结构体对子类的类比 – myStructEx 以与子类从基类派生完全相同的方式从 myStruct 派生。转换为“基”结构体是类型双关（type punning）的一个例子，其中一块内存被当作不同类型来处理。

你可以通过在派生结构体中包含基结构体，将“继承”想法进一步拓展：

```
struct myStruct
{
        int a;
        int b;
};
struct myStructEx
{
        struct myStruct base;
        int c;
};
```

此时，任何接受 myStructEx 的新函数都必须通过 base 来引用基结构体，例如：

```
myPointer->base.a;
```
但如果你将 myStructEx 转换为 myStruct，原始代码仍然有效：

```
(myStruct *)myPointer->a
```

如果你觉得这种情况很少见，而且你不太可能使用或遇到它，那么值得指出的是 CPython 正是基于这种实现类和对象的方式。然而，重要的是要知道，几乎所有的类型双关都违反了严格别名规则（strict aliasing rule）。该规则基本上规定，一块内存只能由指向兼容类型的指针来引用，详见 Dive 16。换句话说，C 语言最常用的高级特性之一，根据最新的 C 标准通常都是非法的。这当然是荒谬的。在任何有意义的地方使用类型双关，如有必要，可以将编译器配置为直接接受它，因为替代方案要糟糕得多。

请注意，当更改结构体类型时，必须小心处理填充（padding）可能不同。例如，如果你有一个类似的结构体：

```
struct test1 {
    char c;
    int i;
};
```

并且你用如下方式进行类型双关：

```
struct test2{
    char c[1];
    char i[4];
};
```

那么你就是在假设内存布局是一个字节的 char，紧接着是四个字节的 int。如果你在 64 位机器上尝试这样做，你会发现 c[0] 等同于 c，但 i[4] 并不能正确表示该整数。原因是该结构体被打包，使得 int 从字边界开始。因此，布局是一个字节的 char，然后是三个字节的填充，以使 int 的四个字节从字边界开始。正确的双关方式是：

```
struct test2{
    char c[4];
    char i[4];
};
```

其中 c 对应 c[0]，而 int 对应 i[0] 到 i[3]。显然，这是依赖于机器的，没有机器独立的方法来获取组成 int 的字节。

## 将结构体作为对象

结构体非常接近对象，因此我们无需做太多改动就能让它们更像对象。对象具有存储数据或函数的字段。这些函数是对象的方法，用于操作对象中的数据。

例如，列表对象可以具有存储数据的字段以及指定方法（如 `sort`）的字段。要使用该方法，你可以这样写：

```python
myObject.sort();
```

你会预期 sort 方法在 myObject 中的数据上执行排序操作。请注意，非对象版本的实现方式是简单地拥有一个排序函数，它接受待排序的数据作为参数：

```python
sort(myObject)
```

对象导向编程和非对象导向编程之间的唯一区别真的只是从 sort(myObject) 切换到 myObject.sort() 吗？显然，事情并没有那么简单，但这确实是该思想的重要组成部分。核心思想是 myObject 与 sort 函数相关联，该函数“知道”如何对其进行排序。

通常，当像 sort(myObject) 这样的函数作为对象的一部分实现时，它们被称为方法，区别在于排序函数绑定到了对象上。这种绑定通常通过在函数内部提供一个额外的局部变量来实现，通常称为 self 或 this，它引用该对象。方法可以使用 self 或 this 来标识正在调用该函数的对象实例。

在 C 语言中，函数可以拥有引用它们的指针，参见 Dive 13，因此它们可以是结构体中的字段。例如：

```c
struct MyClass
{
  int data[10];
  void (*sort)(struct MyClass*);
  void (*display)(struct MyClass*);
};
```
这定义了一个结构体，它有一个 data 字段和两个旨在对数据进行排序和显示的函数。其中较难理解的部分是指定函数指针的类型，更多示例请参见 Dive 13。

方法被声明为标准函数：

```c
void Sort(struct MyClass *self)
{
    printf("sort called\n");
}
void Display(struct MyClass *self)
{
    for (int i = 0; i < 10; i++)
    {
        printf("%d\n", self->data[i]);
    }
}
```
为了利用这一点，我们需要创建一个类实例：

```c
int main(int argc, char **argv)
{
    struct MyClass myObject = {
        .data = {0,1,2,3,4,5,6,7,8,9},
        .sort = &Sort, 
        .display = &Display
    };
    myObject.sort(&myObject);
    myObject.display(&myObject);
}
```
这设置了一个结构体实例，并对其进行初始化，使其拥有一个待排序的数组和两个执行任务的函数。函数可以以常规方式调用，但请注意它们是普通函数，我们必须将结构体实例的指针作为第一个参数传递。函数无法“推导”出要操作哪个结构体实例，用行话来说，这些函数不会自动绑定到它们操作的对象实例。

在 C 语言中，无法以让函数“知道”它是被哪个结构体调用的方式将函数“附加”到结构体上。要做到这一点，我们需要生成一个新的“绑定”函数，即通过偏应用（partial application）生成一个方法，该方法在函数调用中消除 self 但自动提供它，参见 Dive 13 和偏应用。

虽然可以做到，因为 C 语言处于如此底层，任何事都能实现，但这需要了解函数调用和返回是如何实现的，而且这高度依赖于机器。

我们可以引入一个构造函数，使整个结构看起来更像对象：

```c
struct MyClass *new_MyClass(int data[10])
{
    struct MyClass *instance = malloc(sizeof(struct MyClass));
    memcpy(instance->data, data, sizeof(int) * 10);
    instance->sort = Sort;
    instance->display = Display;
    return instance;
}
```
构造函数允许我们使用数据数组初始化对象，该数据通过 memcpy 复制到结构体的 data 字段 – 这非常高效。现在我们自然地构造并使用对象：

```c
int main(int argc, char **argv)
{
    int data[10] = {0,1,2,3,4,5,6,7,8,9};
    struct MyClass *myObject = new_MyClass(data);
    myObject->sort(myObject);
    myObject->display(myObject);
}
```
虽然这样更好，但我们仍受到必须重复 myObject 参数（由于无法将函数绑定到结构体）的困扰。解决这个问题的最简单方法是使用预处理器扫描程序文本，检测在结构体上调用的函数并将其转换：

```
myObject.function(args) →  myObject.function(&myObject,args)
```

以及：

```
myObject->function(args) → myObject->function(myObject,args)
```

当然，这正是 C++ 最初作为 C 的扩展被实现的方式。文本预处理器将 C++ 扩展转换成了纯标准 C。直到后来，C++ 编译器才成为常态。

有许多方法可以为 C 添加功能使其更易于使用并具备面向对象特性，但在大多数情况下，结构体和指向函数的指针就足够了。

