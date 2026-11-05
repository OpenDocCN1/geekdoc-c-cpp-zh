
算法开发完成后，应检查设计的正确性。你现在可以使用标准计算器创建一个包含测试值的表格。对伪代码进行桌面检查，以确保得到预期结果。程序运行后，你可以将程序产生的结果与在设计走查期间用计算器产生的值进行比较，以验证正确性。

## 编写解决方案

完成设计并验证算法的正确性后，将设计转换为源代码。最终的应用程序清单如下：

```csharp
/* TempAgency.cs
 * This application is used by a temporary work agency to
 * set projections for sales for new hires. The program enables the
 * user to input salesmen's names and expected sales goals.
 * The sales figure is placed in a two-dimensional array
 * and expected sales figures for four months are added.
 * These projections are based on increasing sales at
 * least 5% each month over the four-month period.
 * For testing purposes, four salesmen data are entered.
 */

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace TempAgency
{
    public class TempAgency
    {
        public static void Main(string[] args)
        {
            double[,] sales = new double[4, 5];
            string[] salesman = new string[4];

            DisplayInstructions();
            GetSalesData(salesman, sales);
            ProduceSalesProjectionTable(sales);
            DisplaySalesProjections(salesman, sales);

            Console.ReadKey();
        }

        public static void DisplayInstructions()
        {
            Console.WriteLine("You will be asked to enter data for " +
                "four salesmen. \nFor their name, " +
                "enter their first " +
                "name followed \nby a space and then " +
                "their last name." +
                "\n\nNext you will enter the " +
                "expected sales for the 1st month." +
                "\n\n\nFor testing purposes enter " +
                "data for four (4) salesmen.\n\n");
            Console.WriteLine();
        }

        public static void GetSalesData(string[] salesman,
            double[,] sales)
        {
            for (int row = 0; row < salesman.Length; row++)
            {
                string fullname;
                string[] name = new string[3];

                Console.Write("Name of the New Salesman: ");
                salesman[row] = Console.ReadLine();
                fullname = salesman[row];
                name = fullname.Split(' ');
                Console.Write("Please enter {0}'s Initial Sales " +
                    "Goal: ", name[0]);
                sales[row, 0] = double.Parse(Console.ReadLine());
                Console.Clear();
            }
        }

        public static void ProduceSalesProjectionTable(double[,] sales)
        {
            double salesIncrease;

            DisplayHeading(sales);
            for (int row = 0; row < sales.GetLength(0); row++)
            {
                salesIncrease = 0.05;
                for (int col = 1; col < sales.GetLength(1); col++)
                {
                    sales[row, col] = sales[row, col - 1] *
                        salesIncrease + sales[row, col - 1];
                    salesIncrease += 0.05;
                }
            }
        }

        public static void DisplayHeading(double[,] sales)
        {
            double inc = 0.05;

            Console.Write("{0,-20}  {1,-10}", "Salesman",
                "Initial ");
            for (int col = 0; col < sales.GetLength(1) - 1; col++)
            {
                Console.Write("{0, -6} {1,-1}   ", "Month", col + 1);
            }

            Console.WriteLine();

            Console.Write("{0,-20}    {1,-7}", "  Name", " Sales  ");
            for (int col = 0; col < sales.GetLength(1) - 1; col++)
            {
                Console.Write("{0, 8}    ", inc.ToString("P0"));
                inc += 0.05;
            }
            Console.WriteLine();
        }

        public static void DisplaySalesProjections(string[] salesman, double[,] sales)
        {
            string[] name = new string[3];

            Console.WriteLine();
            for (int row = 0; row < sales.GetLength(0); row++)
            {
                name = salesman[row].Split(' ');
                Console.Write("{0,-20}", (name[1] + ", " + name[0]));
                for (int col = 0; col < sales.GetLength(1); col++)
                {
                    Console.Write("{0, 11:N2}", sales[row, col]);
                }
                Console.WriteLine();
            }
        }
    }
}
```

一次测试运行的输出如图 8–12 所示。

![](img/e33ae760e23d89eac66541252ad65de8_483_0.png)

**图 8–12** TempAgency 应用程序输出

## 编码标准

你开发的每个项目都应遵循商定的编码标准。它们使你的代码更易读，并有助于减少错误数量。

### 集合命名指南

- 使用单数名词作为集合对象的标识符。
- 实例化集合对象时使用驼峰命名约定。

## 高级数组建议

- 如果方法返回集合且没有值可返回，则返回空集合而不是 null。
- 处理集合时，尽可能使用 .NET 预定义的方法和属性，而不是编写新代码。

## 资源

你可能想探索的其他站点：

- 数据结构的深入探讨  
  http://msdn.microsoft.com/en-us/library/aa289148(VS.71).aspx
- MSDN C# 数据结构系列  
  http://www.andrewconnell.com/blog/archive/2004/02/17/262.aspx
- 实现一个简单的哈希算法  
  http://blog.roblevine.co.uk/?p=15

## 快速回顾

- 1. 二维和多维数组可以包含任意数量的相同类型变量。一个通用标识符命名整个结构。
- 2. 二维和多维数组应使用单数名词命名。
- 3. 要访问二维或多维数组元素，请使用声明中包含的索引数量。索引用逗号分隔并括在方括号中。
- 4. 当使用二维或多维数组作为方法参数时，需指定数组标识符和类型；但不包括数组的长度或大小。需要开方括号、闭方括号和逗号。对该方法的调用只包括数组名。
- 5. 二维和多维数组可以作为参数传递给方法，此外，方法可以具有二维或多维数组作为返回类型。方法名之前包含的方括号是空的，但有一个或多个逗号例外。逗号分隔符标识维数。
- 6. 二维和其他多维数组遵循与一维数组相同的准则。
- 7. 二维数组通常可视化为分成行和列的表格。第一个索引表示行数。
- 8. 当各行中的列数可能需要不同时，可以使用交错数组（jagged 或 ragged array）。它被称为“数组的数组”。
- 9. ArrayList 类创建类似列表的结构，可以动态增加或减少长度。与传统数组一样，ArrayList 对象的索引从零开始。包含许多预定义方法。
- 10. 要创建多维数组，指定每个秩的类型和维数。这些值用逗号分隔。三维数组将定义为 `type [ , , ] identifier = new type [length_of_planes, length_of_rows, length_of_columns]`。

```csharp
type [ , , ] identifier = new type [length_of_planes, length_of_rows, length_of_columns]
```

- 11. **string 类**存储不可变的字符序列。为 **string** 赋值后，它不能被修改。
- 12. **string 类型**是 .NET Framework 中 **System.String 类**的别名。你可以使用索引访问单个字符，第一个索引为零。
- 13. **字符串变量**是 **string 类**的对象；因此，可以使用许多预定义方法，包括以下：`Trim( )`、`ToUpper( )`、`ToLower( )`、`Substring( )`、`Split( )`、`Replace( )`、`Insert( )` 和 `Copy( )`。
- 14. **Hashtable 类**表示基于键的哈希码组织的键/值对集合。重写 `GetHashCode( )` 方法以为哈希函数提供新算法。
- 15. **BitArrays** 对于处理大型数据集非常有用。它们最常用于表示一组简单的布尔标志。
- 16. **Queue 类**表示对象的先进先出 (FIFO) 集合。`Enqueue( )` 方法将对象添加到队列末尾。`Dequeue( )` 移除并返回队列开头的对象。
- 17. **Stack 类**表示对象的简单后进先出 (LIFO) 集合。`Push( )` 方法将对象添加到堆栈末尾。`Pop( )` 移除并返回堆栈开头的对象。

## 练习

- 1. 当方括号内包含三个值时，最后一个数字表示：
  - a. 类
  - b. 行
  - c. 平面
  - d. 列
  - e. 以上都不是
- 2. 以下哪种数组声明使你能够存储一整周每天的高温和低温？
  - a. `int temp1lo, temp2lo, temp3lo, temp4lo, temp5lo, temp6lo, temp7lo, temp1Hi, temp2Hi, temp3Hi, temp4Hi, temp5Hi, temp6Hi, temp7Hi;`
  - b. `int temp [7, 2] = new int [7, 2];`
  - c. `temp int [ , ] = new temp[7, 2];`
  - d. `int [ , ] temp = new temp [7, 2];`
  - e. `int [ , ] temp = new temp [8, 3];`

