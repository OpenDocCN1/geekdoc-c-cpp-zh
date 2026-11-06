
```cpp
// First try storing the instances
map<StoreMe, StoreMe> instances;

StoreMe key1 = {10};  // braces notation!
StoreMe value1 = {20};
StoreMe key2 = {30};
StoreMe value2 = {40};

instances[key1] = value1;
instances[key2] = value2;
value1.Item = 12345;
cout << instances[key1].Item << endl;

instances[key1].Item = 34567;
cout << instances[key1].Item << endl;

// Next try storing pointers to the instances
map<StoreMe*, StoreMe*> pointers;

StoreMe key10 = {10};
StoreMe value10 = {20};
StoreMe key11 = {30};
StoreMe value11 = {40};

pointers[&key10] = &value10;
pointers[&key11] = &value11;
value10.Item = 12345;
cout << (*pointers[&key10]).Item << endl;

// Finally try storing references to the instances.
// (I commented it out because it will
//  get an error. See the text.)
//  map<StoreMe&, StoreMe&> pointers;
    return 0;
}
```

首先，请注意，为了创建 StoreMe 的实例，我们使用了花括号表示法。当您没有构造函数时，可以这样做。所以这一行：

```cpp
StoreMe key1 = {10};
```

创建了一个 StoreMe 的实例，并将 10 放入 Item 成员变量中。

还要注意，我们注释掉了这一行代码：

```cpp
// map<StoreMe&, StoreMe&> pointers;
```

这是我们尝试声明一个持有引用的 map 的地方。但这一行会产生编译错误。当您输入这段代码清单时，可以尝试取消注释那一行，看看错误消息。由于这一行，我们会得到几条错误消息，主要的两个错误如下：

```
error: conflicting declaration 'std::map<StoreMe&, StoreMe&> pointers'
error: 'pointers' has a previous declaration as 'std::map<StoreMe&,
        StoreMe&>* pointers'
```

显然，引用是不可能的。但为什么会这样呢？原因如下：事实证明，map 会复制您放入其中的一切。我们怎么知道这一点呢？通过输出。以下是您输入这个应用程序时所看到的内容（请注释掉您之前取消注释的那一行，使其重新成为注释行）：

```
20
34567
12345
```

啊哈！真是巧妙。确实巧妙！但现在我们需要确定这个输出的含义。对于第一行，我们在 map 中为 key1 和 value1 存储了一个键值对：

```cpp
instances[key1] = value1;
```

然后我们更改了 value1 中的 Item 成员变量：

```cpp
value1.Item = 12345;
```

接下来，我们从 map 中的键值对中取出了值，并打印了 Item 成员：

```cpp
cout << instances[key1].Item << endl;
```

当我们这样做时，我们看到的是 20，而不是 12345。这意味着存储在 *map* 中的值是一个副本，而不是原始对象。我们将原始对象的 Item 成员更改为 12345，但副本仍然保留着之前的值 20。

但接着我们这样做了：

```cpp
instances[key1].Item = 34567;
```

我们当时的期望是，这个操作会改变存储在 map 中的值的 Item 成员。于是我们再次打印了该值：

```cpp
cout << instances[key1].Item << endl;
```

而这一次，它*确实*改变了。我们看到了 34567。太棒了！有志者，事竟成；有值者，事竟变。（大概是诸如此类的话。）

既然我们已经明白了 *map* 存储的是我们放入其中的内容的副本，那么存储指针的想法就应该很清楚了：如果我们有一个指针变量，然后对它进行复制，虽然现在我们有了一个独立的指针变量，但原始指针和副本都指向同一个东西。这就是清单 6-4 第二部分背后的思想。我们这样创建了 *map*：

```cpp
map<StoreMe*, StoreMe*> pointers;
```

现在，这个 map 存储的是指针变量。请记住，指针变量只是保存一个表示地址的数字。如果两个独立的指针变量持有相同的数字，那就意味着它们指向同一个东西。此外，由于这个 map 持有的是指针，所以它*实际上*持有的是数字，而不是实例——这一点值得思考。

于是我们接下来创建了一些实例，然后建立了一个关联：

```cpp
pointers[&key10] = &value10;
```

注意这里使用了与号（&），我们将其用作引用运算符，以帮助我们将地址存储到`map`中。然后我们更改了其中一个值对象的`Item`成员：

```cpp
value10.Item = 12345;
```

而这一次，当我们使用这个精心添加了括号的代码行进行打印时：

```cpp
cout << (*pointers[&key10]).Item << endl;
```

我们看到：

```cpp
12345
```

又一次……啊哈！这次的更改生效了。这是为什么呢？因为尽管`map`保存的是一个副本，但它保存的是一个指针的副本。而这个指针恰好指向原始的`value10`对象。所以当我们更改`value10`的`Item`成员时，`map`能感知到这个更改。`map`本身没有改变，但`map`指向的是那个值。

![](img/6ba99460b0feb3585671a4612ff5fabb_586_0.png)

从以上关于容器保存副本的讨论中，您可以得出以下结论。因为`map`保存副本，您可以记住关于删除原始对象的这两条规则：

- **当容器保存实例时：** 如果您在`map`中放入实例，那么在实例进入`map`之后，您可以删除原始实例。这是可以的，因为`map`拥有这些实例的副本。
- **当容器保存指针时：** 如果您在`map`中放入指针，您不应该删除原始实例，因为`map`中的指针仍然指向这些实例。

那么哪种方法最好呢？这取决于您。但有几点需要考虑：

- **保留实例：** 如果您不想让实例一直留在周围，您可以将实例放入容器中，容器会制作副本。
- **可复制性：** 您的类是可复制的吗？某些类，例如充满了指向其他类的指针的类，或者非常庞大的类，复制效果并不好。在这种情况下，您可能希望将指针放入容器中。

## 比较实例

当您使用包含其他类（如`vector`）的类时，您需要为该类提供一种比较两个对象的方式。对我们人类来说，凭着我们所拥有的超级大脑，比较起来很容易。但对计算机来说，这并不那么容易。例如，假设您有两个指向 string 对象的指针。第一个指向一个包含`abc`的字符串。第二个指向另一个包含`abc`的字符串。这两个指针相同吗？

嗯，这取决于您如何看待它。如果您是指它们是否指向相同的字符序列，那么是的，它们是相同的。但如果您是指它们是否指向同一个对象，那么也许相同，也许不同。看看这段代码：

```cpp
    string *pointer1 = new string("abc");
    string *pointer2 = new string("abc");
```

`pointer1`和`pointer2`*相等？*同样，这取决于您如何看待它。如果您是指它们指向的字符串是等价的，那么是的，在这个意义上它们是相等的。如果您是指它们指向同一个对象，那么不，在这个意义上它们不相等。现在看看这段代码：

```cpp
    string *pointer3 = new string("abc");
    string *pointer4 = pointer3;
```

这两个指针指向同一个对象。所以在这个意义上，它们是相等的。而且因为它们指向同一个对象，它们也指向相同的字符序列。所以同样地，在这个意义上，它们是相等的。

如您所见，处理对象时，您有两种类型的比较：

- 您在比较两个对象，判断它们是否完全相同，即使它们是各自独立的对象。如果两个对象是独立但完全相同的，您会说它们是相等的。
- 您在比较两个对象，判断它们是否是同一个对象。这种情况可能发生在您有两个指针，并且它们都指向同一个对象时。在这种情况下，您说它们是相等的。

那么，除了有办法把人逼疯之外，您为什么还需要知道这一切呢？（“您说您的车和我们的车是一样的，但事实上它们是不同的：一辆是您的，其余的是我们的！”）您需要知道这种区别，因为当您创建一个保存对象实例的容器类时，该类通常需要知道如何比较对象。`map`的情况尤其如此，它保存的是成对的项目，您需要根据对中的第一个元素——即键元素——来定位项目。当您告诉`map`根据某个键查找项目时，`map`必须在其键值对列表中搜索，直到找到一对，其键与您传入搜索的键相等。
