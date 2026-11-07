
接下来，我们执行以下语句：

```
delete [] second;
```

该语句执行后，`second`所指向的数组被删除。该操作得到图14-11所示结果。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_857_0.png)

**图14-11** 语句`delete [] second;`执行后的`first`和`second`

由于`first`和`second`指向同一个数组，因此语句：

```
delete [] second;
```

执行后，`first`变得无效，也就是说，`first`（以及`second`）现在都是悬空指针。因此，如果程序之后试图访问`first`所指向的内存，那么程序要么会访问错误的内存，要么会因错误而终止。这种情况是浅拷贝的一个例子。更正式地说，在**浅拷贝**中，两个或多个同类型的指针指向同一块内存；也就是说，它们指向相同的数据。

另一方面，假设我们没有使用前面的语句`second = first;`（位于A行），而是使用以下语句：

```
second = new int[10];

for (int j = 0; j < 10; j++)
    second[j] = first[j];
```

第一条语句创建一个包含10个`int`类型分量的数组，并将该数组的基地址存储在`second`中。第二条语句将`first`所指向的数组复制到`second`所指向的数组中（见图14-12）。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_857_1.png)

**图14-12** `first`和`second`都指向各自的数据

现在`first`和`second`都指向各自的数据。如果`second`删除其内存，对`first`没有影响。这种情况是深拷贝的一个例子。更正式地说，在**深拷贝**中，两个或多个指针拥有各自的数据。

从前面的讨论可知，你必须知道何时使用浅拷贝、何时使用深拷贝。

## 类与指针：一些特殊之处

上一节讨论了当指针变量为类类型时，如何使用箭头表示法通过指针访问类成员。由于类可以拥有指针成员变量，本节讨论此类类的一些特殊之处。为便于讨论，我们将使用以下类：

```
class ptrMemberVarType
{
public:
    ⋮
    ⋮
    ⋮
private:
    int x;
    int lenP;
    int *p;
};
```

另外，考虑以下语句（见图14-13）：

```
ptrMemberVarType objectOne;
ptrMemberVarType objectTwo;
```

![](img/1fbe55537254baeb2b5b7dbaf64956ae_858_0.png)

**图14-13** 对象`objectOne`和`objectTwo`

### 析构函数

对象`objectOne`有一个指针成员变量`p`。假设在程序执行期间，指针`p`创建了一个动态数组。当`objectOne`超出作用域时，`objectOne`的所有成员变量都会被销毁。然而，`p`创建了一个动态数组，而动态内存必须使用运算符`delete`来释放。因此，如果指针`p`不使用`delete`运算符释放该动态数组，那么该动态数组的内存空间就会一直保持标记为已分配，即使它无法被访问。我们如何确保当`p`被销毁时，由`p`创建的动态内存也被销毁？假设`objectOne`如图14-14所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_859_0.png)

**图14-14** 对象objectOne及其数据

回想一下，如果类有析构函数，那么每当类对象超出作用域时，析构函数就会自动执行（见第12章）。因此，我们可以在析构函数中放置必要的代码，以确保当objectOne超出作用域时，由指针p创建的内存被释放。例如，类ptrMemberVarType的析构函数定义如下：

```cpp
ptrMemberVarType::~ptrMemberVarType()
{
    delete [] p;
}
```

当然，必须在类的定义中将析构函数包含为该类的成员。让我们通过加入析构函数来扩展类ptrMemberVarType的定义。此外，本节余下部分假定析构函数的定义如前所述——也就是说，析构函数会释放`p`所指向的内存空间。

```cpp
class ptrMemberVarType
{
public:
    ~ptrMemberVarType();
    .
    .
    .

private:
    int x;
    int lenP;
    int *p;
};
```

> **注意** 为使析构函数正常工作，指针p必须具有有效值。如果p未正确初始化（也就是说，如果p的值是垃圾值），并且析构函数执行，那么程序要么因错误消息而终止，要么析构函数释放了不相关的内存空间。因此，在使用指针时应格外小心。

### 赋值运算符

本节描述对于带有指针成员变量的类，内置赋值运算符的局限性。假设objectOne和objectTwo如图14-15所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_860_0.png)

**图14-15** 对象objectOne和objectTwo

回想一下，类上的内置操作之一是赋值运算符。例如，语句：

```
objectTwo = objectOne;
```

将objectOne的成员变量复制到objectTwo中。也就是说，objectOne.x的值被复制到objectTwo.x中，objectOne.p的值被复制到objectTwo.p中。由于p是指针，这种逐成员复制数据会导致数据的浅拷贝。也就是说，objectTwo.p和objectOne.p都会指向同一块内存空间，如图14-16所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_860_1.png)

**图14-16** 语句`objectTwo = objectOne;`执行后的对象objectOne和objectTwo

现在，如果objectTwo.p释放了它所指向的内存空间，objectOne.p就会变得无效。如果类ptrMemberVarType具有析构函数，并且当ptrMemberVarType类型的对象超出作用域时，该析构函数会释放p所指向的内存空间，那么这种情况很可能发生。这表明必须有一种方法来避免这个陷阱。为了避免带有指针成员变量的类出现这种数据浅拷贝，C++允许程序员扩展赋值运算符的定义。这个过程称为重载赋值运算符。第15章解释如何通过运算符重载来完成这项任务。一旦赋值运算符被正确重载，objectOne和objectTwo就都拥有各自的数据，如图14-17所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_861_0.png)

**图14-17** 对象objectOne和objectTwo

### 复制构造函数

声明类对象时，可以使用同类型现有对象的值来初始化它。例如，考虑以下语句：

```
ptrMemberVarType objectThree(objectOne);
```

对象objectThree正在被声明，同时也在使用objectOne的值进行初始化。也就是说，objectOne的成员变量的值被复制到objectThree的对应成员变量中。这种初始化称为默认逐成员初始化。默认逐成员初始化是由构造函数完成的，该构造函数称为复制构造函数（由编译器提供）。正如赋值运算符的情况一样，由于类ptrMemberVarType具有指针成员变量，这种默认初始化会导致数据的浅拷贝，如图14-18所示。（假设objectOne如前所述。）

![](img/1fbe55537254baeb2b5b7dbaf64956ae_861_1.png)

**图14-18** 对象objectOne和objectThree

在描述如何克服这一缺陷之前，让我们再描述一种也可能导致数据浅拷贝的情况。这两个问题的解决方案相同。

回想一下，作为函数的参数，类对象既可以按引用传递，也可以按值传递。记住，类ptrMemberVarType具有析构函数，它会释放`p`所指向的内存空间。假设objectOne如图14-19所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_862_0.png)

**图14-19** 对象objectOne

考虑以下函数原型：

```cpp
void destroyList(ptrMemberVarType paramObject);
```

函数destroyList有一个形式值参数paramObject。现在考虑以下语句：

```cpp
destroyList(objectOne);
```

在这条语句中，objectOne作为参数传递给函数destroyList。因为paramObject是值参数，所以复制构造函数会将objectOne的成员变量复制到paramObject的对应成员变量中。正如前一种情况一样，paramObject.p和objectOne.p会指向同一块内存空间，如图14-20所示。

![](img/1fbe55537254baeb2b5b7dbaf64956ae_862_1.png)

**图14-20** 对象objectOne和paramObject的指针成员变量指向同一个数组

