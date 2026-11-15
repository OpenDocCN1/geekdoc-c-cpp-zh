

![](img/f2bfa570e453b020c16e048c79a3ea0e_244_0.png)

图 6.1 示例结构图。

## 6.2 程序员定义的函数

程序的执行总是从 main 函数开始。当程序遇到函数名时，会调用（或称作激活）其他函数。这些其他函数必须定义在包含 main 函数的文件中，或在另一个可用文件或文件库中。（如果函数包含在系统库文件中，例如 sqrt 函数，则通常称为库函数；其他函数通常称为程序员编写的，或程序员定义的，函数。）执行完函数中的语句后，程序执行将继续执行调用该函数的语句。

考虑将摄氏度转换为华氏度的简单任务。我们可以编写一个程序员定义的函数来执行此计算，并从任何需要此转换的程序解决方案中调用该函数。我们的转换函数将有一个输入参数，即摄氏度温度，并将返回等效的华氏度温度。为了说明，我们将编写一个程序解决方案，从输入文件读取摄氏度温度，并将华氏度写入输出文件。该程序解决方案将包含两个程序员定义的函数，即用于执行输入和输出的 main() 函数，以及用于执行转换的 CelsiusToFahr() 函数。我们转换程序的结构图和流程图在图 6.2 中提供，随后是我们的解决方案和一个程序跟踪。

![](img/f2bfa570e453b020c16e048c79a3ea0e_245_0.png)

图 6.2 温度转换程序的结构图和流程图。

```
#include<iostream> //Required for cin, cerr
#include<fstream> //Required for ifstream, ofstream
#include<string> //Required for string, c_str()
using namespace std;

//Function prototype.
double celsiusToFahr(double celsius); //Programmer defined function.

/*--------------------------------------------------------------*/
/* Program chapter6_1 */
/* This program reads temperatures in degrees Celsius */
/* from an input file, calls a conversion function */
/* and writes converted temperatures to an output file. */
/*--------------------------------------------------------------*/
int main()
{
//Declare variables.
ifstream fin;
ofstream fout;
string filename;
double cels, fahr;

//Open files.
cout << "Enter name of input file\n";
cin >> filename;
fin.open(filename.c_str());
if(fin.fail())
{
cerr << "Could not open the file " << filename << endl;
exit(1);
}
fout.open((filename + "ToFahr").c_str());
fin >> cels;

//while not end of file
while(!fin.eof())
{
//Convert temperature and write to file.
fahr = celsiusToFahr(cels); //Function call.
fout << cels << fahr << endl;
fin >> cels;
}
fin.close();
fout.close();
return 0;
}
/*--------------------------------------------------------------*/
/* This function performs a conversion from */
/* degrees Celsius to degrees Fahrenheit. */
/* Precondition: celsius holds a temperature in degrees Celsius */
/* Postcondition: returns degrees Fahrenheit */
```

```
double celsiusToFahr(double celsius) //Function header.
{
    //Declare local variables.
    double temp;

    //Convert from degrees celsius to degrees Fahrenheit.
    temp = (9.0/5.0)*celsius + 32.0;

    return temp;
}
```

请注意，函数 celsiusToFahr() 不包含输入语句和输出语句，只包含执行温度转换并返回新值所需的语句。输入和输出在 main() 中执行。我们将为程序 chapter6_1 提供一个部分程序跟踪，从语句 fin >> cels; 开始。

### 程序跟踪

| main() | celsiusToFahr (double cels) |
| :--- | :--- |
| 步骤 1: >> cels; | 步骤 2B: double temp; |
| 步骤 2: while (end of file) | 步骤 2C: temp = 9.0/5.0 * cels + 32; |
| 步骤 2A: fahr = celsiusToFahr(cels); | 步骤 2D: return temp; |
| 步骤 2E: fout << fahr; | |
| 步骤 2F: fin >> cels; | |
| 步骤 3: fin.close(); | |
| 步骤 4: fout.close(); | |
| 步骤 5: return 0; | |

### 函数定义

当我们更仔细地查看迄今在文本中定义的函数时，我们会发现函数定义由函数头和随后的语句块组成。函数头定义函数返回的值的类型；前一节示例中 main() 为 int，celsiusToFahr() 为 double。如果函数不返回值，则返回类型为 void。函数名和参数列表跟在返回类型之后。请注意，参数列表可以为空，如我们对 main() 的定义所示。

函数定义的一般形式为

```
Return-type function_name(parameter list)
{
    declarations;
    statements;
}
```

参数列表表示传递给函数的信息；如果没有输入参数，可以省略参数列表。但是，函数名后面必须始终跟一组括号，如定义 int main() 时所做的那样。函数使用的其他对象在定义函数体的语句块中定义。

![](img/f2bfa570e453b020c16e048c79a3ea0e_247_0.png)

应选择有助于记录函数目的的函数名。函数内部还应包含注释，以进一步描述函数目的并记录步骤。我们还使用带有破折号的注释行来将程序员定义的函数与 main 函数以及其他程序员定义的函数分开。

所有返回值的函数都必须包含 return 语句。return 语句的一般形式为

```
return expression;
```

表达式指定要返回给引用该函数的语句的值。return 语句中使用的表达式类型应与函数定义中指示的 return_type 匹配，以避免潜在错误。如果有必要，可以使用强制转换运算符（在第 2 章中讨论）来显式指定表达式的类型。void 函数不返回值，因此具有此一般函数头：

```
void function_name(parameter declarations)
```

void 函数中的 return 语句是可选的，且不包含表达式。一般形式为

```
return;
```

| | |
|---|---|
| 函数定义 | 函数定义由函数头和随后的语句块组成。 |
| 语法 | `return-type function_name(parameter list) //function header { declarations; statements; }` |
| 示例 | `int main() { cout << "hello world" << endl; return 0; }`<br>`void drawBlock(ostream& out, int size) { int width, height; for(height=0; height<size; ++height) { for(width=0; width<size; ++width) { out << " *"; } out << endl; } }` |

![](img/f2bfa570e453b020c16e048c79a3ea0e_249_0.png)

图 6.3 [-20, 20] 范围内的 Sinc 函数。

函数可以定义在 main 函数之前或之后。请记住，右大括号指定定义函数体的语句块的结束。但是，一个函数必须在另一个函数定义开始之前完全定义；函数定义不能互相嵌套。在我们的程序中，我们首先包含 main 函数，然后按程序中引用它们的顺序包含其他函数。

我们将展示使用程序员定义函数的程序的第二个示例。如图 6.3 所示绘制的 sinc(x) 函数，通常用于许多工程应用中。sinc(x) 最常见的定义如下：

```
f(x) = sinc(x)
= \frac{\sin(x)}{x}.
```

此函数的值易于计算，但 sinc(0) 除外，它给出 0/0 的不定式。在这种情况下，可以使用微积分中的洛必达法则来证明 sinc(0) = 1。

假设我们想要开发一个允许用户输入区间限值 a 和 b 的程序。程序随后应计算并打印 a 和 b 之间（包含两端）均匀间距的 x 值的 21 个 sinc(x) 值。因此，x 的第一个值应为 a。然后应添加一个增量以获得下一个 x 值，以此类推，直到第 21 个值，它应为 b。因此，x 的增量为

```
x_increment = \frac{interval_width}{20} = \frac{b - a}{20}.
```

为 a 和 b 选择值，并让自己相信，使用此增量，并以 a 作为第一个值，第 21 个值将是 b。

