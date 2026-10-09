

void testComputeLengthOfString() {
  const char* quotation="To be or not to be";
  int l1 = computeLengthOfString( quotation );
  int l2 = strlen( quotation ); // built in
  ASSERT( l1==l2 );
}

在处理数组和内存段时，必须非常小心，切勿试图访问数组边界之外的数据。例如，下面的代码行为将是不可预测的，并且很可能导致严重崩溃。

char* shortText = new char [20];
for (int i=0; i<1000; i++) {
  shortText[i] = 'x';
}
delete[] shortText;

如果您下载了项目 **PointerExamples**，可以通过取消注释 main 方法中的 **testOverrunning** 测试来运行此测试。我预计您会得到一条相当糟糕的错误信息。

在调试模式下使用 **string** 和 **vector** 等类时，会包含各种额外的检查，以便您获得更有用的错误信息。您可以尝试使用 **vector\<char\>** 重写此代码，并比较获得的错误信息。这是使用类而不是直接使用指针的另一个非常有说服力的理由。

## 提示：避免使用 char\*

**string** 的设计初衷是为了解决程序员历史上在 **char\*** 方面遇到的诸多问题。如果您正在进行复杂的字符串操作，例如编写 Web 服务器，即使使用 **string** 也无法胜任，因为它无法处理国际字符。

## 11.4 按指针传递

我们已经了解了*按值传递*和*按引用传递*的概念（见第 7.2.1 节）。原则上，您也可以使用*按指针传递*的方式将数据传递给函数。

void polarToCartesian(double r, double theta,
double* x, double* y) {
    *x = r*cos(theta);
    *y = r*sin(theta);
}

void testPolarToCartesian() {
    double r = 2;
    double theta = atan(1);
    double x;
    double y;
    polarToCartesian(r, theta, &x, &y);
    ASSERT_APPROX_EQUAL(x, sqrt(2), 0.0001);
    ASSERT_APPROX_EQUAL(y, sqrt(2), 0.0001);
}

这段代码以通常的方式按值传递参数 **r** 和 **theta**，但将参数 **x** 和 **y** 的指针传递过去。这些是测试函数的局部变量。当调用 **polarToCartesian** 时，它直接修改这些局部变量。之所以能够这样做，是因为它获取了存储变量 **x** 和 **y** 的内存地址。

使用指针传递数据和使用引用传递数据之间几乎没有实际区别。在 C 语言中，由于不存在引用的概念，因此必须使用按指针传递。

在 C++ 语言中，使用按引用传递是首选的方法。

最实际的差异在于，函数 **polarToCartesian** 的使用者被迫使用 & 符号来获取变量 **x** 和 **y** 的指针。在某些方面，这是一件好事，因为它清楚地表明 **x** 和 **y** 可能会被函数调用修改。另一方面，使用指针确实增加了一层概念上的难度。

在使用指针和引用时能实现的事情之间唯一的真正区别在于：如果你传递的是一个指针，那么是否可以使用指针运算符（例如使用 ++ 递增指针或调用 **delete**）并不完全清楚。另一方面，如果使用按引用传递，则很清楚对象不会被删除，++ 运算符也不会被调用，因为你根本不能将这些运算符应用于引用。这就是为什么在 C++ 中按引用传递是首选方法的原因。

与引用一样，你可以在指针中使用关键字 **const**。将关键字 **const** 与指针结合使用有两种可能的方式。在 * 的右侧书写 **const** 意味着指针本身不能被修改。在 * 的左侧书写 **const** 意味着*被指向的数据*不能被修改，而不是指针本身。下面的代码说明了这种区别。如果你去掉注释字符，代码将无法编译。

void constPointerExamples() {
    const char* ptr = "A string";
    ptr++;
    std::cout << (*ptr);
    // (*ptr)='a';  // You can't change the data
    // using a const char*
    
    char* fiveChars = new char[5];
    char *const constPtr = fiveChars;
    // constPtr++;  // You can't change a char *const
    (*constPtr) = 'h'; // but you can change
    // what it points to
}

如果你觉得 `const char*` 和 `char *const` 之间的区别令人困惑，那么你不是唯一这样想的人。有人可能会认为，使用 `const` 引入的概念难度超过了编译时检查带来的好处。正如我们之前所说，项目的主开发者应该对此持有观点，因为应该一致地使用 `const` 或完全避免使用它。

如果你计划使用 `const`，那么这段讨论给出了另一个偏好按引用传递而非按指针传递的理由：将 `const` 与引用结合使用只有一种方式，因此少了一些需要思考的事情。注意，这也许可以帮助你记住在使用指针时 `const` 应该放在哪里。`*` 左侧的 `const` 等同于 `&` 左侧的 `const`。你甚至不能将 `const` 写在 `&` 的右侧，因为不能对引用使用 `++` 等运算。

## 11.5 不要返回指向局部变量的指针

与数组一样，你必须确保在返回指针时，没有返回一个即将被删除的局部变量的指针。例如，下面的代码是不正确的：

char* thisFunctionReturnsAnArray() {
    /* This produces a compiler warning */
    char text[] = "Don't do this";
    return text;
}

void someOtherFunction() {
    char text[] = "Alternative text\n";
    cout << text;
    cout << "\n";
}

void testDontReturnArrays() {
  char* text = thisFunctionReturnsAnArray();
  someOtherFunction();
  cout << text;
  cout << "\n";
}

这里的 text 是一个 char 数组，因此在函数退出的那一刻就会被删除。这意味着代码的行为将是不可预测的。运行它时，它很可能会打印出一些垃圾数据。

你可以毫无问题地返回一个 string，因为它是按值返回的：字符串的新副本会提供给调用者。返回 vector 的情况也是如此。

允许返回通过 new [] 创建的数据的指针。然而，届时你必须确保调用者知道他们是否被期望在某个时间点调用 delete[]。

在 C 和 C++ 中约定俗成的做法是，如果函数返回一个指针，调用者不被期望调用 delete[]。例如，如果你在 string 上调用 c_str()，你不应该对返回值调用 delete[]。当你调用 c_str 时，它会在内存中创建一个临时的 C 风格字符串，该字符串可能会在字符串被修改或被删除时被删除。这是 C++ 中推荐的标准模式。如果你创建了某样东西，删除它是你的责任。

作为一个例子，下面的代码及其测试在技术上是有效的，但违反了你不应该删除由其他函数返回的指针的约定。因此，大多数 C++ 程序员都会认为这是糟糕的代码。

char* thisFunctionReturnsAPointer() {
  char text[] = "This works";
  int n = strlen(text);
  char* ret = new char[n+1];
  /* We now get a compiler warning here */
  strcpy( ret, text );
  return ret;
}

void testReturnPointerJustAboutOK() {
  char* text = thisFunctionReturnsAPointer();
  someOtherFunction();
  cout << text;
  cout << "\n";
  // don't forget to free the memory
  delete[] text;
}

### 提示：返回指针

切勿返回指向局部变量的指针。如果愿意，你可以返回指向对象成员变量的指针。在这种情况下，确保数据被删除是对象的职责，而不是调用者的职责。（有关如何使用*析构函数*实现此功能的信息，请参阅第 16.2 节）

## 11.6 使用指针共享数据

下面是我们现在希望解决的此类问题的一个示例：

**示例 1：** 我们有一个类 *Instrument*。它包含关于交易工具的许多数据。例如，工具的类型、彭博代码、路透代码等。你应该想象每个 *Instrument* 都占用相当多的内存。

我们还有另一个类，*Position*，它仅由工具、持有该工具的数量以及持有该头寸的交易员名称组成。

我们希望通过重用相同的 *Instrument* 实例来节省内存。图 11.4 对此进行了说明。

![](img/70e8b6971c8420e92597c05233ce9700_213_0.png)

**图 11.4：** 两个 Position 对象共享一个 Instrument。

