

## 表3.10 Lambda捕获说明及示例

| 捕获说明 | 含义 | 示例 |
|---|---|---|
| `[ ]` | 不捕获任何对象。 | `vector<int > vec;` |
| `[&]`<br>`[&a]` | 按引用捕获：1. 按引用捕获所有局部对象。这使得lambda表达式能够访问其所有局部对象。按引用捕获存在潜在风险，因为lambda表达式可能比其参数存活更久。在这种情况下，lambda可能会尝试访问悬垂指针或引用。因此，更安全的方式是创建所传递对象的副本。2. 明确指定需要访问的局部对象（更安全）。按引用捕获对象 a。 | `12`<br><br>`// However, avoid default [0]`<br>`{`<br>`    if (&rand_strings[rand_index] != 0) {`<br>`        const auto &s = rand_strings[rand_index(rand_strings.size())];`<br>`        return s[rand_index(s.size())];`<br>`    }`<br>`}`<br>`// ---------------------------------------------`<br><br>`cout << "Proposed password: " << pwd << endl;`<br><br>第[4–8]行定义了一个向量 `rand_strings`，其中包含三个带有字符集的字符串。这是为了通过混合使用大写字母、小写字母以及数字和符号（如 `#` 和 `@`）来提高密码强度。这些将用于生成密码。由于我们期望简洁，因此使用 `rand` 和 `seed` 函数来初始化和生成随机数。不过，更好的选择是使用新的随机数生成器之一，例如第3.17.3节中介绍的那个。我们的第一个lambda表达式在第[18–22]行定义，并分配给标识符 `rand_index`（一个闭包）。它利用初始化捕获，将全局常量 `RAND_MAX` 复制到变量 `rn`，该变量仅对该lambda局部可见。形参 `max` 定义了这个lambda可以生成的最大值。最后，通过定义中的 `-> int` 部分显式定义了返回值。这确保了浮点值被显式转换为整数类型，因为此lambda用于生成随机整数值。由于应用了 `1.0` 整数类型转换，该函数可以生成范围在 `0 ... max_val - 1` 内的值（包括端点）。然后形成一个循环，生成几个示例随机密码，每个密码包含八个字符。<br><br>主要的密码生成由STL库中的 `generate_n` 函数执行。它的第一个参数 `back_inserter(pwd)` 告诉函数在长度为 `passwordLen` 的 `pwd` 字符串末尾插入新元素，`passwordLen` 是该函数的第二个参数。`generate_n` 最有趣的参数是第三个，它是一个定义在第[39–43]行的第二个lambda函数；它执行两次随机抽取。<br><br>这次我们使用捕获 `[& rand_strings, & rand_index]`，显式提供了已命名的对象 `rand_strings` 和 `rand_index`。同样有趣的是，这个lambda是之前定义的lambda闭包对象，因为它将被此lambda使用。同样有趣的是，这个lambda在其参数列表中没有接受任何参数，因此其参数列表为空。如前所述，有两个随机操作。第一个操作在第[41]行，从 `rand_strings` 容器中选择三个字符串之一。在选定的字符串中，第[42]行选择一个随机字符，返回给 `generate_n` 算法。结果，获得了一系列随机生成的八个字符的字符串。之前代码的输出如下所示（每次运行会有所不同）：<br>`Proposed password: tbFVH4k`<br>`Proposed password: 2sCxY_Ks`<br>`Proposed password: 12J8683A` |
| `{...}` | 使用可变参数模板捕获。 | 第61–77行：这个例子有点高级，但在实践中可用（模板在第4.8节讨论）。这里我们将创建一个模板函数 `multi_print_helper`，它接受任意数量的参数，这些参数将输出到输出流。例如，它将作为诊断工具使用，如下所示。<br><br>要定义一个可变参数模板函数，我们需要该函数的两个版本：在第[62–67]行定义的启动版本，以及在第[70–77]行定义的带有模板参数包 `Args` 的版本。此结构遵循第[76]行发生的递归调用类型。因此，在递归结束时，启动版本终止调用。<br><br>`void multi_print_helper_test( void )`<br>`{`<br>`    // Make a log file`<br>`    ofstream log_file("log_file.txt");`<br><br>`    // A helper variable lambda that joins multi_print_helper with the log file`<br>`    auto diagnostic_print = [& log = log_file]( auto... params ) -> ostream &`<br>`    {`<br>`        // Each output separate with "," then add end-of-line`<br>`        return multi_print_helper( log, ", ", params ... ) << endl;`<br>`    };`<br><br>`    int x( 1 ); double y( 2.0 ); string z ( "error" );`<br><br>`    // Output objects of arbitrary type to the log file`<br>`    diagnostic_print( x, y, z );`<br><br>`    diagnostic_print( x, y, z, "text", x == y, 5.0 );`<br>`}`<br><br>`multi_print_helper_test` 函数展示了可变参数模板 `multi_print_helper` 函数的使用情境。然而，因为我们绝不应该希望将输出重定向到第[81]行创建的文件，所以在第[84–87]行引入带可变参数辅助lambda。它执行的唯一操作，在第[86]行，是使用适当组织的参数调用 `multi_print_helper`。最后，前面的lambda在第[93]和第[95]行被调用，每次传入不同数量的任意类型输入参数。最终，`log_file.txt` 的内容如下所示：<br><br>`1 2 three`<br>`2 three Text: 0.5` |

Lambda可以在其捕获列表中混合对象访问类型。下表包含一些示例：

| Lambda捕获变体 | 含义 | Lambda捕获变体 | 含义 |
|---|---|---|---|
| `[a,&b]` | 按值（副本）捕获对象 a，按引用捕获 b |  |  |
| `[=, &a]` | 全部按值捕获，但对象 a 按引用捕获 | `[&, a]` | 全部按引用捕获，但 a 按值捕获 |
| `[a, this]` | 捕获 a 和 this 指针（见第4.4节）。 | `[&, this]` | 全部按引用捕获，但 `this` 按值捕获（`this` 只能按值访问） |
|  |  | `[this, ...]` | 捕获 this 指针和可变参数模板 |

如前所述，关于lambda表达式一个有趣的事情是，声明其类型的唯一方式是使用 `auto` 关键字。这是因为每个lambda表达式都有一个唯一且未命名的类型（其关联闭包对象的类型）。然而，lambda表达式可以转换（强制转换）为具有相同形参和相同返回类型的函数指针（在下一节讨论）。在这种情况下，与使用原始函数指针相比，更好的想法是使用 `std::function`（见第3.14.9节）。

Lambda函数是常量对象。这意味着它们不能更改在其捕获列表中传入的对象的值。然而，将它们声明为 mutable 将允许此类更改；见第7.4.7节。

## 3.14.8 (⚒) 函数指针

有时我们需要将一个函数作为参数传递给另一个函数，或将其作为结构体中的成员。有时函数提供者希望在事件发生时调用一个函数——这称为回调机制。处理这种情况有很多选择。C/C++中可用的最低级选择是简单的函数指针。其语法如图3.21所示：它遵循函数声明模式，不同之处在于函数名被 `(*function_ptr_name)` 替换，其中 `function_ptr_name` 只是函数指针的标识符。

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_150_0.png)

在下面的例子中，我们希望编写一个简短的程序来计算函数在单点处的导数。在开始之前，让我们回顾一些数学知识。对于给定的连续函数 $f$，其导数 $f'$ 定义如下（Korn and Korn 2000）

$$f'(x)=\lim_{\delta\to 0}\frac{f(x+\delta)-f(x)}{\delta} \tag{3.4}$$

