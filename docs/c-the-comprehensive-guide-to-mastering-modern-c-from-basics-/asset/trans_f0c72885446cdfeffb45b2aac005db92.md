
每个这些测试都会重新设置并销毁。

![](img/290cf954dfcaad53865de6b98cca8e6f_613_0.png)

**图 14.3** 测试用例包含带有断言的测试函数，并组合成测试套件。

## 14.2.1 准备、执行、断言 (Arrange, Act, Assert)

你会很快发现，在编写测试时，某些模式总是重复出现。我通常会在函数内部分为三个部分：

```cpp
// https://godbolt.org/z/sTaegfxr
void testDouble5() {
  // arrange
  auto param = 5;
  // act
  auto result = doubleIt(param);
  // assert
  assertTrue(result == 10);
}
```

有时 arrange 是空的，因为我完全可以直接写 `doubleIt(5)`。然而，其他部分总是被填充的；没有了它们，测试就失去了意义。这个原则被称为准备、执行、断言。[ 29 ]

之后，建议你也将待测试的代码清晰地划分为这三个部分。这使得编写和理解变得更容易。在前面的示例中，这看起来可能极其微不足道，但如果你在执行之前必须先创建一个间谍对象和 Mock 对象场景，那么清晰的划分是有帮助的：

- 在 arrange 中，你声明并初始化变量，并准备实际测试期间需要的物品。
- 然后，在 act 中，你调用待测试的程序代码。
- 在 assert 部分，对预期结果与实际结果进行所有检查。[ 30 ]

按照原则，你的每个测试都应该遵循这种模式。在特殊情况下，你可以将所有三个部分合并为一行。这样，并且只有这样，你可以在测试例程中多次调用待测试的代码——这就是我的建议。它看起来如下：

```cpp
// https://godbolt.org/z/rn5oK3M6e
void testDoubleIt() {
  assertTrue(doubleIt(0) == 0);
  assertTrue(doubleIt(-1) == -2);
  assertTrue(doubleIt(1) == 2);
  assertTrue( double It(5) == 10 );
}
```

## 测试边界情况

你的测试应该特别（但不仅限于）覆盖边界情况，例如带有参数 θ 的调用和负数。典型用例的良好组合也很重要，在这里使用了 1 和 5。

对于整数，θ 和 -1 往往是边界情况的良好值；字符串可以为空 ("")，而 C 风格字符串和其他指针可以为 `nullptr`。在各种正常用例和边界情况（corner cases）的组合上测试你的函数。

## 14.2.2 可供选择的框架

有许多测试框架的实现。有些只支持单元测试，而另一些适用于其他类型的测试。这里是侧重于单元测试和可移植性的少量选择，完整的列表要大得多：[ 31 ]

- **Boost.Test**
该框架是 Boost 库集合的一部分。它可以既作为仅头文件版本使用，也可以作为需要链接的库使用。我在这里用它来解释这些示例。
- **C++ Unit Testing Easier (CUTE)**
一个简单但先进的单元测试框架，可以通过插件集成到 Eclipse 中。[ 32 ]
- **CppUnit**
这是一个相当广泛的单元测试框架，深受 JUnit 的启发。[ 33 ]
- **doctest**
这是一个小型的仅头文件库。[ 34 ]
- **Google Test**
Google 也使用 C++ 进行开发，并提供了其测试框架。[ 35 ]

## 14.3 Boost.Test

让我们直接开始看一个我们想要测试的程序。我们在这里使用的框架是 Boost.Test。

### 安装 Boost.Test

你可以从 Boost 网站的 [http://www.boost.org/users/download](http://www.boost.org/users/download) 下载完整包 Boost。对于 Windows 和 MSVC，提供了预编译的库。在 Ubuntu 上，运行 `sudo apt-get install libboost-dev` 可以安装整个库。其他发行版也有相应的包。仅安装 Boost 的子库是不够的。

下面的示例显示了 `fib` 函数：

```cpp
#define BOOST_TEST_MAIN
#include <boost/test/included/unit_test.hpp>

int fib(int n) {
    if (n <= 0) return 0;
    if (n == 1) return 1;
    int a = 0, b = 1, sum = 0;
    for (int i = 2; i <= n; i++) {
        sum = a + b;
        a = b;
        b = sum;
    }
    return b;
}

using namespace boost::unit_test;

BOOST_AUTO_TEST_CASE(fib) {
    BOOST_CHECK(fib(0) == 0);
    BOOST_CHECK(fib(1) == 1);
    BOOST_CHECK(fib(2) == 1);
    BOOST_CHECK(fib(3) == 2);
    BOOST_CHECK(fib(4) == 3);
    BOOST_CHECK(fib(5) == 5);
    BOOST_CHECK(fib(6) == 8);
}
```

通过 `BOOST_TEST_MAIN` 宏，你告诉 Boost.Test 在此模块中自动生成一个 `main()` 函数。`BOOST_AUTO_TEST_CASE` 宏创建一个指定名称的测试用例并将其添加到默认测试套件中。

`BOOST_CHECK` 是简单的断言宏。它只接受一个可以转换为 `bool` 的参数。如果在测试运行期间结果为 `false`，则测试失败。除了 `BOOST_CHECK`，还有几种其他断言宏：稍后介绍。

> 先实际值，后预期值

注意，在 Boost.Test 中，你应该先提实际结果，后提预期结果。对于表 14.1 中的宏，这没有太大区别，但如果你使用库 1.59 或更高版本的 `BOOST_TEST`，框架的输出会更详细：

等待，如果你将比较运算符尽可能靠右侧，框架的输出会更详细：

```cpp
BOOST_AUTO_TEST_CASE(expected_to_right) {
    int a = 13, b = 2;
    BOOST_TEST(a % b == 7); // check a % b == c failed [13 % 2 != 7]

    BOOST_TEST(7 == a % b); // check a == c % b failed [7 != 13 % 2]
}
```

你通过将两个模块编译为可执行文件来编译测试程序：

```bash
g++ fib.cpp test_fib.cpp -o test_fib.x
```

运行它时，你没有看到错误：

```bash
$ ./test_fib.x
Running 1 test case...
*** No errors detected
```

此版本的 Boost.Test 库仅包含头文件，没有在编译时需要指定的静态或动态库。`<boost/test/included/unit_test.hpp>` 文件包含 `main()` 及其所有的辅助函数——它不是通常意义上的头文件。因此，该文件不应包含任何实现，特别是那些在项目中多次包含时会阻止编译的实现。而且由于 .../included/unit_test.hpp 包含了 `main()`，它它会在程序中多次出现，这会导致

