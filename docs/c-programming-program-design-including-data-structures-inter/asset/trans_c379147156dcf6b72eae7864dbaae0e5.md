

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_853_0.png)

**图 12-14** 对象 objectOne 及其数据

回顾一下，如果一个类有析构函数，那么每当类对象离开作用域时，析构函数就会自动执行（见第 10 章）。因此，我们可以把必要的代码放入析构函数中，以确保当 objectOne 离开作用域时，指针 p 所创建的内存被释放。例如，类 ptrMemberVarType 的析构函数定义如下：

```
ptrMemberVarType::~ptrMemberVarType()
{
    delete [] p;
}
```

当然，你必须在类的定义中将析构函数作为类的成员包含进来。让我们通过包含析构函数来扩展类 ptrMemberVarType 的定义。此外，本节其余部分假设析构函数的定义如前面给出的一样——也就是说，析构函数释放 p 所指向的内存空间。

```
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

> 为了让析构函数正常工作，指针 p 必须具有有效的值。如果 p 没有被正确初始化（也就是说，如果 p 的值是垃圾值）并且析构函数执行，那么程序要么以错误消息终止，要么析构函数释放一个不相关的内存空间。因此，在使用指针时，你应该格外小心。

## 赋值运算符

本节描述带有指针成员变量的类在使用内置赋值运算符时的局限性。假设 objectOne 和 objectTwo 如图 12-15 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_854_0.png)

**图 12-15** 对象 objectOne 和 objectTwo

回顾一下，对类内置的操作之一是赋值运算符。例如，语句：

```
objectTwo = objectOne;
```

将 objectOne 的成员变量复制到 objectTwo 中。也就是说，objectOne.x 的值被复制到 objectTwo.x 中，objectOne.p 的值被复制到 objectTwo.p 中。因为 p 是一个指针，这种逐成员复制数据会导致数据的浅拷贝。也就是说，objectTwo.p 和 objectOne.p 都会指向同一块内存空间，如图 12-16 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_854_1.png)

**图 12-16** 执行语句 objectTwo = objectOne; 后对象 objectOne 和 objectTwo

现在，如果 objectTwo.p 释放了它所指向的内存空间，那么 objectOne.p 就会变得无效。如果类 ptrMemberVarType 有一个析构函数，并且当 ptrMemberVarType 类型的对象离开作用域时该析构函数会释放 p 所指向的内存，那么这种情况很可能会发生。这表明必须有一种方法来避免这个陷阱。为了避免带有指针成员变量的类出现这种数据浅拷贝，C++ 允许程序员扩展赋值运算符的定义。这个过程称为重载赋值运算符。第 13 章将解释如何通过使用运算符重载来完成这项任务。一旦赋值运算符被正确重载，objectOne 和 objectTwo 就都拥有自己的数据，如图 12-17 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_855_0.png)

## 复制构造函数

在声明类对象时，你可以使用同一类型的现有对象的值来初始化它。例如，考虑以下语句：

```
ptrMemberVarType objectThree(objectOne);
```

这里声明了对象 objectThree，并且还使用 objectOne 的值来初始化它。也就是说，objectOne 的成员变量的值被复制到 objectThree 的对应成员变量中。这种初始化称为默认逐成员初始化。默认逐成员初始化是由（编译器提供的）复制构造函数完成的。正如赋值运算符的情况一样，因为类 ptrMemberVarType 有指针成员变量，这种默认初始化会导致数据的浅拷贝，如图 12-18 所示。（假设 objectOne 如前所述。）

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_855_1.png)

在描述如何克服这个缺陷之前，让我们再描述一种也可能导致数据浅拷贝的情况。这两个问题的解决方案是相同的。

回顾一下，作为函数的参数，类对象既可以按引用传递，也可以按值传递。请记住，类 ptrMemberVarType 有析构函数，它会释放 p 所指向的内存空间。假设 objectOne 如图 12-19 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_856_0.png)

**图 12-19** 对象 objectOne

让我们考虑以下函数原型：

```
void destroyList(ptrMemberVarType paramObject);
```

函数 destroyList 有一个形式值参数 paramObject。现在考虑以下语句：

```
destroyList(objectOne);
```

在这条语句中，objectOne 作为参数传递给函数 destroyList。因为 paramObject 是值参数，所以复制构造函数将 objectOne 的成员变量复制到 paramObject 的对应成员变量中。正如前一种情况一样，paramObject.p 和 objectOne.p 会指向同一块内存空间，如图 12-20 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_856_1.png)

**图 12-20** 对象 objectOne 和 paramObject 的指针成员变量指向同一个数组

因为 objectOne 是按值传递的，所以 paramObject 的成员变量应该拥有自己的数据副本。特别是，paramObject.p 应该拥有自己的内存空间。我们如何确保实际上确实如此呢？

如果一个类有指针成员变量：

-   在对象声明期间，如果允许默认的逐成员数据复制，那么使用一个对象的值初始化另一个对象会导致数据的浅拷贝。
-   如果对象作为参数按值传递，并且允许默认的逐成员数据复制，那么会导致数据的浅拷贝。

在这两种情况下，为了强制每个对象拥有自己的数据副本，我们必须覆盖编译器提供的复制构造函数的定义；也就是说，我们必须提供自己的复制构造函数定义。通常的做法是在类的定义中放入包含复制构造函数的声明，然后编写复制构造函数的定义。这样，每当需要执行复制构造函数时，系统就会执行我们提供的定义，而不是编译器提供的定义。因此，对于类 ptrMemberVarType，我们可以通过将复制构造函数包含在类 ptrMemberVarType 中来克服这种浅拷贝问题。示例 12-8 说明了这一点。

复制构造函数在三种情况下自动执行（前两种情况已在前文描述）。

-   当声明一个对象并使用另一个对象的值初始化它时
-   当对象作为参数按值传递时
-   当函数的返回值是一个对象时

因此，一旦为类 ptrMemberVarType 正确定义了复制构造函数，objectOne.p 和 objectThree.p 就都会拥有自己的数据副本。同样，objectOne.p 和 paramObject.p 也会拥有自己的数据副本，如图 12-21 所示。

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_857_0.png)

**图 12-21** 对象 objectOne 和 paramObject 的指针成员变量拥有各自的数据

当函数 `destroyList` 退出时，形式参数 `paramObject` 离开作用域，对象 `paramObject` 的析构函数释放 `paramObject.p` 所指向的内存空间。然而，这种释放对 `objectOne` 没有影响。

在类的定义中包含复制构造函数的一般语法是：

```
className(const className& otherObject);
```

请注意，复制构造函数的形式参数是一个常量引用参数。

示例 12-8 说明了如何在类中包含复制构造函数以及它如何工作。

### 示例 12-8

考虑以下类：

```
class ptrMemberVarType
{
public:
    void print() const;
        //Function to output the data stored in the array p.

    void insertAt(int index, int num);
        //Function to insert num into the array p at the
        //position specified by index.
        //If index is out of bounds, the program is terminated.
        //If index is within bounds, but greater than the index
        //of the last item in the list, num is added at the end
        //of the list.

    ptrMemberVarType(int size = 10);
        //Constructor
        //Creates an array of the size specified by the
        //parameter size; the default array size is 10.

    ~ptrMemberVarType();
        //Destructor
        //deallocates the memory space occupied by the array p.

    ptrMemberVarType(const ptrMemberVarType& otherObject);
        //Copy constructor

private:
    int maxSize; //variable to store the maximum size of p
    int length;  //variable to store the number of elements in p
    int *p;      //pointer to an int array
};
```

假设类 `ptrMemberVarType` 的成员定义如下：

