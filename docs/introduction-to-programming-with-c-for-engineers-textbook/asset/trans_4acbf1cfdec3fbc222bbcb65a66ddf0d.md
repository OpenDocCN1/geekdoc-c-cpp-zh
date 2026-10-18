
## 625

测试软件需要正确分层。在我们的示例中，`Decimal_2_Roman_Chain_UnitTest` 测试函数属于主 *RomanApp* 项目。另一方面，*Google Test* 为 *RomanApp_GTest* 提供的测试框架仅用于插入待测试的函数，例如我们示例中的 `Decimal_2_Roman_Chain_UnitTest`，如在清单 A.6 中所示。

**清单 A.6** *Google Test* 宏在 *RomanApp_GTest* 项目的源文件中，用于通过调用 *RomanApp* 项目中的 `Decimal_2_Roman_Chain_UnitTest` 函数来验证十进制到罗马数字的转换（在 `test.cpp`）。

```cpp
#include "pch.h"

#include "../../../include//Dec2Roman.h"

TEST(TestCaseName, TestName) {
    EXPECT_EQ(1, 1);
    EXPECT_TRUE(true);
}
```

```cpp
}

TEST( DecRoman_TestSuite, ChainTest )
{
    bool result = Decimal_2_Roman_Chain_UnitTest();

    // Nonfatal assertion
    EXPECT_EQ( result, true ) << "All decimals 1..3999 should pass and vice versa";

    // Fatal assertion
    ASSERT_EQ( result, true ) << "All decimals 1..3999 should pass and vice versa";
}
```

之前的 *test.cpp* 源文件是由创建 *RomanApp_GTest* 时的项目向导自动生成的，如图 A.12 所示。该文件包含了一些预定义的 *Google Test* 构造。在第 1 行，通过 *pch.h* 文件包含预编译头文件，这是针对 Microsoft Visual Studio 平台的特有功能，出于兼容性原因，我们在本书的其他项目中避免使用该功能。可以在为源文件打开的设置面板中关闭预编译头的使用。然后，第 3 行包含 *Dec2Roman.h* 头文件，这使我们能够从主 *RomanApp* 项目中调用 `Decimal_2_Roman_Chain_UnitTest` 测试函数。因此，头文件的名称前加上相对路径。

TEST 宏（在第 5–7 行调用 EXPECT_EQ 和 EXPECT_TRUE 宏）是由向导自动添加的，用于展示 *Google Test* 平台的基本功能。同样，在第 11 行，我们添加自己的测试。首先，在第 13 行，调用 `Decimal_2_Roman_Chain_UnitTest` 测试函数，并将其返回结果保存到 *result* 标志中。随后，在第 16 行和第 19 行分别通过非致命的 EXPECT_EQ 和致命的 ASSERT_EQ 进行检查。只需点击 Test Explorer 窗格中的绿色按钮即可运行测试，如图 A.14 所示。

**图 A.14** Visual Studio 包含两个项目：*RomanApp* 和其 *RomanApp_GTest* 测试项目，基于 Google Test 库。使用 Google Test 宏编写的软件单元测试会调用针对 *RomanApp* 具体行为的单元测试。如 Test Explorer 窗格所示，第一个测试（来自 test.cpp）通过，而第二个测试失败。

## 626

+   阅读并尝试使用 C++20 的实验性模块在 Visual Studio 中的功能（[https://docs.microsoft.com/en-us/cpp/cpp/modules-cpp?view=msvc-190](https://docs.microsoft.com/en-us/cpp/cpp/modules-cpp?view=msvc-190)）。然后，将 Section 4.7 中的简单项目（如 EMatrix）重构为使用 C++20 模块，而不是传统的头文件。
+   
+   设计并实现一个应用程序，用于显示浮点数值及其在 IEEE 754 标准的不同格式中的对应位设置（参见第 7.4 节及表 A.4）。
+   
+   增强 Section 2 中的简单文本游戏，加入图形和用户界面。
+   
+   设计并实现一个简单的房屋安防应用程序，用于检测是否有人在房屋周围徘徊。提示：安装 OpenCV 库用于 AI 和计算机视觉操作；编写一个组件，将从摄像头获取的视频信号分割为静态背景和前景移动物体，然后尝试开发区分人形剪影与动物或汽车的规则。
+   
+   设计并实现一个照片演示应用程序，给定包含照片的目录后在屏幕上显示这些照片。提示：尝试使用 SFML 或 ImGui 库（见表 A.4）。下一步，添加平滑图像溶解效果和音乐。
+   
+   设计并实现一个 PDF 文档转换为简易演示文稿的应用程序。例如，仅从输入文档中复制章节标题、图表、表格及其标题到输出演示文稿。提示：使用 PoDoFo 库打开和操作 PDF 文件（http://podofo.sourceforge.net/about.html）。更多 C++ 库可参考 https://en.cppreference.com/w/cpp/links/libs。

## 628

# Bibliography

Aho, A., Lam, M., Sethi, R., and Ullman, J. (2006). *Compilers: Principles, Techniques, and Tools.* Addison-Wesley.
Alexander, C. (1977). *A Pattern Language: Towns, Buildings, Construction.* Oxford University Press.
Allison, C. (2006). Where did all my decimals go? *Journal of Computing Sciences in Colleges* 21 (3): 47–59.
Augustin, (2017). C++ unit testing in Visual Studio. C++ Team Blog. https://blogs.msdn.microsoft.com/vcblog/2017/04/19/cpp-testing-in-visual-studio.
Filipek, B. R. (2018). *C++17 in Detail.* Independently published. https://www.bfilipek.com/2018/08/cpp17indetail.html.
Boccara, J. (2016). Strong types for strong interfaces. Fluent {C++}. https://www.fluentcpp.com/2016/12/08/strong-types-for-strong-interfaces.
Boccara, J. (2018). Getting the benefits of strong typing in C++ at a fraction of the cost. Fluent {C++}. https://www.fluentcpp.com/2018/04/06/strong-types-by-struct.
Boost.org (2020). Boost C++ libraries. https://www.boost.org.
Bryant, R. and O’Hallaron, D. (2015). *Computer Systems: A Programmer’s Perspective.* Prentice Hall.
Catch Org (2019). Catch2. https://github.com/catchorg/Catch2.
Cohn, J. (2019). *Scrum Fundamentals: A Beginner’s Guide to Mastery of the Scrum Project Management Methodology.* Independently published.
Coplien, J. (1995). Curiously recurring template patterns. *C++ Report* 7 (2): 24–27.
Cormen, T.H., Leiserson, C.E., Rivest, R.L., and Stein, C. (2009). *Introduction to Algorithms.* MIT Press.
Cover, T.M.i. and Thomas, J.A. (2006). *Elements of Information Theory.* Wiley-Interscience.
Cplusplus.com (2020). http://cplusplus.com.
Cppreference.com (2018). Filesystem library. https://en.cppreference.com/w/cpp/experimental/fs.
Cppreference.com (2019a). Date and time utilities. https://en.cppreference.com/w/cpp/chrono.
Cppreference.com (2019b). Template argument deduction. https://en.cppreference.com/w/cpp/language/template_argument_deduction.
Cppreference.com (2020a). Template parameters arguments. https://en.cppreference.com/w/cpp/language/template_parameters.
Cppreference.com (2020b). http://cppreference.com.
Cppreference.com (2020c). Operator overloading. https://en.cppreference.com/w/cpp/language/operators.
Čukić, I. (2019). *Functional Programming in C++.* Manning Publications Co.

## 630

# Bibliography

Cyganeк, B. (2013). *Object Detection and Recognition in Digital Images: Theory and Practice.* New-York: Wiley.

Cyganeк, B. (2020). CppBook web page. *http://home.agh.edu.pl/~cyganek/BookCpp.htm*.

Dalheimer, M.K. and Welsh, M. (2006). *Running Linux: A Distribution-Neutral Guide for Servers and Desktops*, 5e. O’Reilly Media.

Dick, G., van Reeuwijk, K., Bal, H.E. et al. (2012). *Modern Compiler Design.* Springer.

Dick, J., Hull, E., and Jackson, K. (2017). *Requirements Engineering.* Springer.

Douglass, B. (2006). *Real Time UML.* Boston: Addison Wesley.

Fan, X. (2015). *Real-Time Embedded Systems: Design Principles and Engineering Practices.* Kidlington: Newnes-Elsevier.

FLTK Team (2019). *Fast Light Toolkit (FLTK).* *www.fltk.org*.

Fowler, M. (1999). *Refactoring: Improve the Design of Existing Code.* Boston: Addison Wesley.

Gamma, E., Helm, R., Johnson, R., and Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented software.* New-York: Addison-Wesley Professional.

Goldberg, D. (1991). What every computer scientist should know about floating-point arithmetic. *ACM Computing Surveys* 23 (1): 5–48.

Google (2019). Googletest Google testing and mocking framework. *https://github.com/google/googletest*.

Grune, D., van Reeuwijk, K., Bal, H.E. et al. (2012). *Modern Compiler Design.* Heidelberg: Springer.

Hinde, D. (2018). *PRINCE2 Study Guide: 2017 Update.* Sybex.

Josuttis, N.M. (2012). *The C++ Standard Library: A Tutorial and Reference.* New-York: Addison-Wesley Professional.

Kahan, W. (1965). Further remarks on reducing truncation errors. *Communications of the ACM* 8 (1): 40.

Kernighan, B. and Ritchie, D. (1988). *C Programming Language*, 2e. Chicago: Prentice Hall.

Kerrisk, M. (2010). *The Linux Programming Interface: A Linux and UNIX System Programming Handbook.* The Starch Press.

Knuth, D. (1998). *The Art of Computer Programming. Seminumerical Algorithms*, 3e, vol. 2. New York: Addison-Wesley.

Korn, G. and Korn, T. (2000). *Mathematical Handbook for Scientists and Engineers: Definitions, Theorems, and Formulas for Reference and Review*, 2e. Dover: Dover Publications.

Liskov, B. (1988). Data abstraction and hierarchy. OOPSLA ’87. *https://doi.org/10.1145/62138.62141*.

Martin, R.C. (2009). Getting a SOLID start. Clean Coder. *https://sites.google.com/site/unclebobconsultingllc/getting-a-solid-start*.

Matloff, N. and Salzman, J. (2008). *The Art of Debugging with GDB, DDD and Eclipse.* No Starch Press.

McConnell, S. (2004). *Code Complete (Developer Best Practices)*, 2e. New-York: Microsoft Press.

Meyer, B. (1997). *Object-Oriented Software Construction*, 2e. New-York: Prentice Hall.

Meyers, S. (2014). *Effective Modern C++: 42 Specific Ways to Improve Your Use of C++11 and C++14.* Chicago: O’Reilly Media.

Niebler, E. (2019). *Range-v3.* *https://ericniebler.github.io/range-v3*.

OpenMP (2020). *www.openmp.org*.

O’Regan, G. (2019). *Concise Guide to Software Testing.* Springer.

Pas, R.v., Stotzer, E., and Terboven, C. (2017). *Using OpenMP – The Next Step.* The MIT Press.

Patterson, D. and Hennessy, J. (2018). *Computer Organization and Design. The Hardware/Software Interface.* Morgan Kaufmann.

Press, W., Teukolsky, S., Vetterling, W., and Flannery, B. (2007). *Numerical Recipes: The Art of Scientific Computing*, 3e. Cambridge: Cambridge University Press.
