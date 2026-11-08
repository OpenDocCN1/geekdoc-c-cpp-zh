

> **注意** 关于将固定大小数组传递给函数，存在一种常见且可能危险的误解。考虑 average() 函数的以下变体：

```cpp
double average10(double array[10]) /* The [10] does not mean what you might expect! */
{
    double sum {};                 // Accumulate total in here
    for (size_t i {}; i < 10; ++i)
        sum += array[i];           // Sum array elements
    return sum / 10;               // Return average
}
```

显然，这个函数的作者编写它是为了精确计算十个值的平均值；不多也不少。我们邀请你将 Ex8_05.cpp 中的 average() 替换为前面的 average10() 函数，并相应地更新 main() 中的函数调用。生成的程序应该能够正常编译和运行。那么问题出在哪里？问题在于，这个函数的签名——不幸的是，它完全是合法的 C++ 语法——造成了一种错误预期：编译器会强制规定只能将大小恰好为十的数组作为参数传递给这个函数。为了验证，让我们看看如果修改示例程序中 main() 函数的主体，只传递三个值会发生什么（你可以在 Ex8_05A.cpp 中找到生成的程序）：

```cpp
double values[] { 1.0, 2.0, 3.0 };      // Only three values!!!
std::cout << "Average = " << average10(values) << std::endl;
```

尽管我们现在用一个远短于所需十个值的数组调用了 average10()，生成的程序仍然应该可以编译。如果你运行它，average10() 函数将盲目地读取远超 values 数组边界的内存。显然，这不会有什么好结果。程序要么崩溃，要么产生垃圾输出。

问题的根源在于，不幸的是，C++ 语言规定编译器应将这种形式的函数签名

```cpp
double average10(double array[10])
```

视为与以下两者同义：

```cpp
double average10(double array[])
double average10(double* array)
```

因此，在按值传递数组时，绝不应使用维度说明；它只会造成错误预期。按值传递的数组总是作为指针传递，编译器不会检查其维度。我们稍后会看到，可以改用按引用传递而不是按值传递，将给定大小的数组安全地传递给函数。

理论上，你也可以在第一个参数的类型说明中指定数组的第一维，但最好不要这样做。编译器同样会直接忽略这一点，类似于我们之前讨论的 average10() 函数的情况。不过，数组第二维的大小确实会产生预期效果——C++ 在这方面就是这么反复无常。任何以 4 作为第二维的二维数组都可以传递给这个函数，但以 3 或 5 作为第二维的数组则不行。

让我们通过一个具体示例尝试将二维数组传递给函数：

```cpp
// Ex8_06.cpp
// Passing a two-dimensional array to a function
import <iostream>;
import <array>;                // For std::size()

double yield(const double values[][4], size_t n);

int main()
{
  double beans[3][4] { { 1.0,  2.0,  3.0,  4.0},
                       { 5.0,  6.0,  7.0,  8.0},
                       { 9.0, 10.0, 11.0, 12.0} };

  std::cout << "Yield = " << yield(beans, std::size(beans))
            << std::endl;
}

// Function to compute total yield
double yield(const double array[][4], size_t size)
{
  double sum {};
  for (size_t i {}; i < size; ++i)   // Loop through rows
  {
    for (size_t j {}; j < std::size(array[i]); ++j) // Loop through elements in a row
    {
      sum += array[i][j];
    }
  }
  return sum;
}
```

这会产生以下输出：

```cpp
Yield = 78
```

yield() 函数的第一个参数被定义为由任意行、每行四个 double 类型元素组成的 const 数组。调用该函数时，第一个参数是 beans 数组，第二个参数是数组的长度。其计算结果为数组中的行数。

指针表示法并不特别适用于多维数组。在指针表示法中，嵌套 for 循环中的语句将如下所示：

```cpp
sum += *(*(array+i)+j);
```

想必你会同意，用数组表示法进行计算更清晰！

**注意** 由于编译器知道 array[i] 的大小，你可以将 Ex8_06 中 yield() 函数的内层循环替换为如下所示的基于范围的 for 循环：

```cpp
for (double val : array[i])    // Loop through elements in a row
{
    sum += val;
}
```

不过，你也不能同样地将外层循环替换为基于范围的 for 循环，也不能在那里使用 std::size()。请记住，编译器无法知道 double[][4] 数组的第一维；按值传递数组时，只能固定数组的第二维或更高维。

### 按引用传递

你可能还记得，*引用*是另一个变量的别名。你也可以将函数参数指定为引用，在这种情况下，函数对该参数使用*按引用传递*机制。调用函数时，与引用参数对应的实参不会被复制。相反，引用参数会用该实参进行初始化。因此，它成为调用函数中该实参的别名。在函数体中使用该参数名的任何地方，都好像是在直接访问调用函数中的实参值。

通过在类型名后添加 & 来指定引用类型。例如，要将参数类型指定为“对 string 的引用”，你会将该类型写为 string&。调用具有引用参数的函数与调用按值传递实参的函数没有区别。不过，对于 string 等类型的对象，使用引用可以提高性能。按值传递机制会复制对象，对于长字符串来说，这会耗时，而且也会耗内存。使用引用参数时，不会发生复制。

### 引用与指针

在许多方面，引用与指针相似。为了看出这种相似性，让我们使用 Ex8_04 的一个变体，其中包含两个函数：一个接受指针作为参数，另一个则接受引用：

```cpp
// Ex8_07.cpp
// Modifying the value of a caller variable - references vs pointers
import <iostream>;

void change_it_by_pointer(double* reference_to_it);    // Pass pointer (by value)
void change_it_by_reference(double& reference_to_it);  // Pass by reference

int main()
{
    double it {5.0};
    change_it_by_pointer(&it);        // Now we pass the address
    std::cout << "After first function execution, it = " << it << std::endl;

    change_it_by_reference(it);       // Now we pass a reference, not the value!
    std::cout << "After second function execution, it = " << it << std::endl;
}

void change_it_by_pointer(double* pit)
{
    *pit += 10.0;        // This modifies the original double
}
void change_it_by_reference(double& pit)
{
    pit += 10.0;        // This modifies the original double as well!
}
```

结果是 main() 中原来的 it 值被更新了两次，每次函数调用更新一次：

```cpp
After first function execution, it = 15
After second function execution, it = 25
```

最明显的区别是，要传递指针，你需要先使用取地址运算符取得该值的地址。当然，在函数内部，你还必须再次解引用该指针才能访问该值。对于按引用接受实参的函数，这两者都不需要做。但请注意，这种区别纯粹是语法上的；最终，两者效果相同。事实上，编译器大多会以与指针相同的方式编译引用。

那么，既然它们在功能上似乎等价，你应该使用哪种机制呢？这是个合理的问题。因此，让我们考虑一些在这个决定中起作用的方面。

指针最显著的特征是它可以是 nullptr，而引用必须始终引用某个对象。因此，如果你想允许空实参的可能性，就不能使用引用。当然，正因为指针参数可以为空，你几乎被迫在使用它之前始终检查 nullptr。引用的优点是你不必担心 nullptr。

如 Ex8_07 所示，调用具有引用参数的函数，其语法确实与调用按值传递实参的函数没有区别。一方面，由于不需要取地址和解引用运算符，引用参数允许更优雅的语法。然而，另一方面，恰恰因为没有语法上的区别，引用有时会带来意外。而令人意外的代码是糟糕的代码，因为意外会导致缺陷。例如，考虑以下函数调用：

```cpp
do_it(it);
```

如果没有 do_it() 的原型或定义，你无法知道这个函数的实参是按引用传递还是按值传递。因此，你也无法知道前面的语句是否会修改 it 值——当然，前提是 it 本身不是 const。按引用传递的这一特性有时会使代码更难理解；如果你没有预料到作为实参传递的值会被修改，就可能导致意外。因此：

