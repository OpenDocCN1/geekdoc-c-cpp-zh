

## 在深入代码分析之前，请注意第 [3] 行的 using namespace std 结构。它打开了当前编译软件（即编译单元）中所有已包含标准头文件的整个标准命名空间。因此，标准函数和类可以省略 `std::` 前缀。缺点是，如果已经存在一个与打开的命名空间中的函数或类同名的函数或类，就可能发生名称冲突。因此，应避免使用前面的结构，尤其是在头文件中。这意味着应显式使用 `std::` 前缀，尤其是当这样做不会降低代码可读性时。另一种替代方法（也在我们的大多数示例中使用）是逐字引入我们希望使用的每个构造而不带 `std::` 前缀，例如 using std::cout、using std::string 等。尽管如此，在源文件（.cpp）中使用该命名空间中的数十个函数和类时，如果潜在名称冲突得到良好控制（如 Functions_Lambdas.cpp 中所示，清单 3.16 仅展示了其中的一小部分），有时打开整个 std 或其他命名空间也是合理的。我们的首要目标应该是软件的正确性，这条规则和其他规则都应谨慎选择，并且只有在支持这一首要目标时才应用。

我们的第一个 lambda 表达式（lambda 函数）完全写在清单 3.16 的第 [11] 行。与“经典的”函数定义相比，它没有名称，而是有一对方括号：[ ]。然后，在括号中，我们看到形式参数 cm 的定义，后面是在花括号 { } 中的函数体。它的作用很简单——接受以厘米表示的参数 cm，并通过乘以 2.54 将其转换为英寸。我们提到 lambda 表达式没有名称；在许多情况下，不需要给 lambda 命名。然而，在必要时，整个 lambda 表达式可以赋给一个对象，例如我们示例中第 [9] 行的做法。这是一个 lambda 闭包对象，它允许我们进一步引用该表达式，例如第 [20] 行的调用。但请注意，除了使用 `auto` 关键字外，没有其他方法可以声明此 lambda 闭包对象的类型。在本节末尾，我们将进一步探讨这个特性。

如图 3.20 所示，lambda 表达式由以下部分组成：

+   - **捕获**（**Caption**）——将外部对象引入 lambda 的作用域
+   - **形式参数列表**（**Formal arguments list**）——定义形式参数的类型和名称列表，与任何其他函数一样
+   - **可选返回类型**（**Optional return type**）——`->` 运算符后跟返回对象的类型
+   - **lambda 体**（**Lambda body**）——包含在花括号 { } 中的一组语句和表达式，包括 `return`

每个 lambda 都包含一个运行时对象，称为 lambda 闭包。如果 lambda 表达式附加到一个标识符，它可以像任何其他对象一样用于传递函数，或将其存储在

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_141_0.png)

**图 3.20** lambda 表达式由三个部分组成：捕获、形式参数列表和可选返回类型。lambda 体包含在花括号 { } 中。

## 考虑到参数 o 可以表示任何流，例如 `std::cout`，也可以表示打开的文件或网络端口，第 [18–20] 行应该很容易理解。为了打印可读信息，在第 [21] 行，输出了第 [16] 行定义的 vector 中的文本。

现在我们创建一个简单的数据库，包含一些参加水肺潜水课程的人员信息。这由一个名为 SCUBA_Class 的 vector 表示，其中包含 StudentInfo 对象：

```cpp
// 让我们创建一个 SCUBA 班级
vector<StudentInfo> SCUBA_Class {

    { L"Phil", L"Curtis",     18,   StudentInfo::SCUBA_Cert::kAdvanced },
    { L"Kamil", L"Cyganek",   15,   StudentInfo::SCUBA_Cert::kOpenWater },
    { L"John", L"Kowalski",   23,   StudentInfo::SCUBA_Cert::kOpenWater },
    { L"Michal", L"Brajta",   61,   StudentInfo::SCUBA_Cert::kInstructor },
    { L"Anna", L"McLachlan",  18,   StudentInfo::SCUBA_Cert::kAdvanced },
    { L"Boż", L"Cyganek",     49,   StudentInfo::SCUBA_Cert::kInstructor },
    { L"Megan", L"Plant",     26,   StudentInfo::SCUBA_Cert::kMaster }

};
```

最后，在下面的 SCUBA_Course 函数中，我们显示满足某些条件的 SCUBA 学员的信息。首先，使用 std::sort 函数对 SCUBA_Class vector 进行排序，该函数在第 [43–44] 行调用。由于每个 StudentInfo 对象包含许多数据字段，我们需要告诉 sort 应使用哪个字段进行排序。这是通过提供在第 [44] 行定义的 lambda 函数来实现的。它接受两个对 StudentInfo 对象的常量引用，并返回 fFamilyName 字符串进行字典序比较的布尔值。这不需要任何进一步干预，因为编译器已经“知道”如何比较字符串。然后，在第 [47–48] 行，使用 std::copy 函数将排序后的 vector 复制到屏幕上（参见表 3.6）。

类似的排序和打印在函数的接下来几行 [54–59] 中完成。然而，这次我们按 fAge 排序。此外，还使用了 `auto` 关键字来自动推导对象类型。

最后，在第 [65] 行，调用了 std::copy_if：它只输出那些 fCert 字段与外部提供的 cert 对象相同的对象。此检查由另一个 lambda 函数完成，该函数在第 [67] 行定义。然而，与前两个 lambda 不同，这个 lambda 使用拷贝捕获将 cert 引入其作用域：

```cpp
void SCUBA_Course( void )
{
    wcout << endl << L"按姓氏排序：" << endl;

    // -----------------------
    // 按姓氏排序
    sort( SCUBA_Class.begin(), SCUBA_Class.end(),
          [] ( const StudentInfo & a, const StudentInfo & b )
          { return a.fFamilyName < b.fFamilyName; } );

    // 将它们打印到屏幕上
    copy( SCUBA_Class.begin(), SCUBA_Class.end(),
          ostream_iterator<StudentInfo, wchar_t> wcout, L"\n" );

    wcout << endl << L"按年龄排序：" << endl;

    // -----------------------
    // 按年龄排序
```

```cpp
sort( SCUBA_Class.begin(), SCUBA_Class.end(),
      [] ( const auto & a, const auto & b )
      { return a.fAge < b.fAge; } );

// 将它们打印到屏幕上
copy( SCUBA_Class.begin(), SCUBA_Class.end(),
      ostream_iterator< StudentInfo, wchar_t >( wcout, L"\n" ) );

wcout << endl << L"小组中的教练：" << endl;

// 查找所有具有给定证书的学员
const auto cert = StudentInfo::SCUBA_Cert::kInstructor;
copy_if( SCUBA_Class.begin(), SCUBA_Class.end(),
         ostream_iterator< StudentInfo, wchar_t >( wcout, L"\n" ),
         [ cert ] ( const auto & a ) { return a.fCert == cert; } );

wcout << endl << endl;
}
```

运行时，程序打印以下关于 SCUBA 班级的信息：

```
按姓氏排序：
Michal Brajta,  61      Instructor
Phil Curtis,    18      Advanced
Kamil Cygánek,  15      OpenWater
Bog Cyganek,    49      Instructor
John Kowalski,  23      OpenWater
Anna McLaughlan, 18     Advanced
Megan Plant,    26      Master

按年龄排序：
Kamil Cygánek,  15      OpenWater
Phil Curtis,    18      Advanced
Anna McLaughlan, 18     Advanced
John Kowalski,  23      OpenWater
Megan Plant,    26      Master
Bog Cyganek,    49      Instructor
Michal Brajta,  61      Instructor

小组中的教练：
Bog Cyganek,    49      Instructor
Michal Brajta,  61      Instructor
```

# 我们从这个示例中学到了什么？

+   - Lambda 函数可以通过拷贝和引用进行捕获
+   - 一个简单的 `StudentInfo` 结构体持有个人信息，其中包含作用域枚举类型 `SCUBA_Cert`
+   - 为 `StudentInfo` 重载的流插入运算符 `<<`
+   - 来自 SL 的 `std::sort` 和 `std::copy_if` 函数，带有提供的 lambda 函数和不同的捕获方式

# 3.14.7 (✕) 更多关于 Lambda 函数的内容

在使用 lambda 时，正确指定其捕获类型非常重要。具有不同捕获和不同调用条件的 lambda 示例见表 3.10。

