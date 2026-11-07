

```cpp
{
   string text = "9" ;
   string term( "9" );
   string info = "Toys" ;
   string color ;
   // Add more statements here.
   return 0 ;
}
```

- 3. 在 main 函数中，在变量声明之后插入语句，声明并初始化一个字符数组，然后将其值赋给未初始化的**字符串**变量
  
  ```cpp
  char hue[4] = { 'R', 'e', 'd', '\0' } ;
  color = hue ;
  ```

- 4. 将一个较长的文本**字符串**赋给其中一个**字符串**变量
  
  ```cpp
  info = "Balloons" ;
  ```

- 5. 通过将第一个**字符串**变量中的所有**字符串**变量值组合起来，构建一个长**字符串**，然后输出组合后的**字符串**值
  
  ```cpp
  text += ( term + color + info ) ;
  cout << endl << text << endl ;
  ```

- 6. 保存、编译并运行程序以查看输出

![](img/bf8dbdfb89042fadbaa73b4160c74bac_62_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_62_1.png)

记住添加特殊的 \0 字符，以标记字符数组中字符串的结束。

## 获取字符串输入

上一章介绍的用于输入数值的 C++ **cin** 函数，也可以将文本输入赋给**字符串**变量。但这有一个限制：它一次只能用于输入单个单词——**cin** 函数在遇到空格时停止读取输入，并将其他任何文本留在“输入缓冲区”中。

当你想允许用户输入带空格的字符串（例如一句话）时，可以使用 **getline()** 函数。该函数需要两个参数来指定字符串的源和目标。例如，**cin** 函数作为源，名为“str”的字符串变量作为目标：

```cpp
getline( cin , str ) ;
```

**getline()** 函数从输入“流”中读取，直到遇到行末的 **\n** 换行符——该换行符是在按 Return 键时产生的。

混合使用 **cin** 和 **getline()** 函数时必须小心，因为 **getline()** 函数会自动读取输入缓冲区中遗留的任何内容——让人感觉程序跳过了一条指令。可以使用 **cin.ignore()** 函数忽略输入缓冲区中遗留的内容，从而克服此问题。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_63_0.png)

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀，开始一个新程序
  
  ```cpp
  #include <string>       // Include string support.
  #include <iostream>
  using namespace std ;
  ```

- 2. 添加一个 main 函数，其中包含一个字符串变量声明和最后的 **return** 语句
  
  ```cpp
  int main()
  {
      string name ;
      // Add more statements here.
      return 0 ;
  }
  ```

- 3. 在 main 函数中，插入语句，将用户名输入赋给一个字符串变量，然后输出其值
  
  ```cpp
  cout << "Please enter your full name: " ;
  cin >> name ;
  cout << "Welcome " << name << endl ;
  ```

- 4. 接下来，插入一条再次请求用户名的语句，但这次在输出其值之前，使用 **getline** 函数将输入赋给**字符串**变量
  
  ```cpp
  cout << "Please re-enter your full name: " ;
  getline( cin , name ) ;
  cout << "Thanks," << name << endl ;
  ```

- 5. 保存、编译并运行程序，并在要求时输入你的全名

![](img/bf8dbdfb89042fadbaa73b4160c74bac_64_0.png)

这个不理想的结果表明，**cin** 会一直读取到第一个空格，将第二个名字留在输入缓冲区中，随后该名字会被 **getline()** 读取并输出。即使你只输入名字，问题仍然存在，因为 **cin** 会将按 Return 键时产生的换行符留在输入缓冲区中。

- 6. 编辑程序以解决此问题：在调用 **getline** 函数之前插入一条语句，指示它忽略输入缓冲区中的内容。
  
  ```cpp
  cin.ignore(256, '\n');
  ```

- 7. 再次保存、编译并运行程序，然后重新输入你的全名，以查看程序按需运行。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_64_1.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_64_2.png)

数值输入或单个单词输入使用 **cin** 函数，但字符串输入使用 **getline()** 函数。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_64_3.png)

**cin.ignore()** 函数的参数指定它应丢弃最多 256 个字符，并在遇到换行符时停止。

## 解决字符串问题

当你需要将**字符串**变量转换为其他数据类型时（例如要用这些值执行算术运算），就会出现问题。由于 **字符串** 对象不是 C++ 原生数据类型，**字符串**变量值无法通过强制转换转换为 **int** 或任何其他常规数据类型。

C++ **<sstream>** 库提供了解决方案，它允许 **stringstream** 对象充当中间媒介，通过该媒介可以将**字符串**值转换为数值数据类型，也可以将数值转换为**字符串**数据类型。要让程序具备此能力，必须在程序开头使用 **#include <sstream>** 指令添加该库。

可以使用与 **cout** 语句一起使用的熟悉输出流 **<<** 运算符，将值加载到 **stringstream** 对象中。然后可以使用与 **cin** 语句一起使用的 **>>** 输入流运算符，从 **stringstream** 对象中提取内容。

为了重新使用 **stringstream** 对象，必须先将其恢复为原始状态。这需要将其内容设置为空**字符串**，并清除其位标志。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_65_0.png)

- 1. 通过指定要包含的 C++ 库类和要使用的命名空间前缀，开始一个新程序
  
  ```cpp
  #include <string>      // Include string support.
  #include <sstream>      // Include stringstream support.
  #include <iostream>
  using namespace std;
  ```

- 2. 添加一个 main 函数，其中包含最后的 **return** 语句，并声明两个已初始化、要转换的变量
  
  ```cpp
  int main()
  {
      string term = "100";
      int number = 100;
      // Add more statements here.
      return 0;
  }
  ```

- 3. 在 main 函数中，插入语句以声明一个整数变量、一个**字符串**变量和一个 **stringstream** 对象
  
  ```cpp
  int num;              // To store a converted string.
  string text;          // To store a converted integer.
  stringstream stream;  // To perform conversions.
  ```

- 4. 接下来，使用流输出运算符将已初始化的**字符串**值加载到 **stringstream** 对象中
  
  ```cpp
  stream << term;      // Load the string.
  ```

- 5. 使用流输入运算符从 **stringstream** 对象中提取内容到未初始化的整数变量中
  
  ```cpp
  stream >> num;       // Extract the integer.
  ```

- 6. 对该整数执行算术运算并输出结果
  
  ```cpp
  num /= 4;
  cout << "Integer value: " << num << endl;
  ```

- 7. 重置 **stringstream** 对象以备重新使用
  
  ```cpp
  stream.str("");      // Empty the contents.
  stream.clear();       // Empty the bit flags.
  ```

- 8. 现在，使用流输出运算符将已初始化的整数值加载到 **stringstream** 对象中
  
  ```cpp
  stream << number ;    // Load the integer.
  ```

- 9. 使用流输入运算符从 **stringstream** 对象中提取内容到未初始化的**字符串**变量中
  
  ```cpp
  stream >> text ;    // Extract the string.
  ```

- 10. 对该**字符串**执行拼接并输出结果
  
  ```cpp
  text += " Per Cent" ;
  cout << "String value: " << text << endl ;
  ```

- 11. 保存、编译并运行程序以查看转换后的输出值

![](img/bf8dbdfb89042fadbaa73b4160c74bac_66_0.png)

![](img/bf8dbdfb89042fadbaa73b4160c74bac_66_1.png)

请注意，这里如何使用 **stringstream** 对象的 `str()` 函数将其内容重置为空字符串。

![](img/bf8dbdfb89042fadbaa73b4160c74bac_66_2.png)

非空 **stringstream** 对象具有指示其状态为 good、bad、eof 或 fail 的位标志——如这里所示，在重新使用之前，应通过 **stringstream** 对象的 `clear()` 函数清除这些标志。

