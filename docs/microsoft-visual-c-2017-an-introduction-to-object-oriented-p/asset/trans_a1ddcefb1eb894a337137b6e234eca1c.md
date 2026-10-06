
将数据写入文件，或者你也可以创建一个与你在书中看到的许多类相似的 Employee 类。图 14-10 显示了一个典型的 `Employee` 类，它包含三个字段以及每个对应的属性。

```
class Employee
{
    public int EmpNum {get; set;}
    public string Name {get; set;}
    public double Salary {get; set;}
}
```

**图 14-10** Employee 类

为了将 Employee 数据存储到持久化存储设备中，你需要声明一个 `FileStream` 对象来定义存储文件的特征。例如：

```
FileStream outFile = new FileStream(FILENAME,
Mode.Create, FileAccess.Write);
```

然后将 `FileStream` 对象传递给 `StreamWriter` 的构造函数，以便写入文本。例如：

```
StreamWriter writer = new StreamWriter(outFile);
```

然后你可以使用对象的 `writeLine()` 方法将 Employee 数据写入输出流中。你可以使用文本字段和逗号来组合字符串。字符串中表示实体或字段的文本块称为标记（token）。分隔标记的每个逗号都是分隔符（delimiter），它是用于指定文件中数据边界的字符。如果没有分隔符，分离和解释标记的过程将变得更加困难。例如，假设你在以下语句中将逗号定义为分隔符：

```
const string DELIM = ",";
```

那么，当向文件写入数据时，可以使用如下语句通过逗号分隔符分隔字段：
writer.WriteLine(emp.EmpNum + DELIM + emp.Name + DELIM + emp.Salary);

分隔符可以是任何不需要作为文件中数据一部分的字符，但通常使用逗号。包含逗号分隔值的文件通常被称为 CSV 文件。当由于逗号需要作为数据内部的字符而不能用作分隔符时，有时你会使用 Tab 字符、管道符 (|) ，或者使用引号内的逗号。

`WriteLine()` 方法以回车符结束输出。当你使用此方法创建文件输出时，自动追加的回车符就构成了记录分隔符。

图 14-11 包含一个完整的程序，该程序打开一个文件并持续提示用户输入 Employee 数据。图中第一个阴影语句是“引导读入”（priming read）——一个提供第一个数据项或记录的输入语句。在这种情况下，第一个项目是员工编号。如果第一个输入是 `END` 值，则永远进入 `while` 循环。如果输入了有效的员工编号，则在循环内检索记录的其余数据，并在循环底部的第二个阴影语句输入下一个员工。当一个员工的三个字段都输入后，这些字段被写入文件，并用逗号分隔。当用户为员工 ID 输入哨兵值 999 时，数据循环结束，文件关闭。图 14-12 显示了典型的执行过程，图 14-13 显示了创建的顺序数据文件的内容。

```
using System;
using static System.Console;
using System.IO;
class WriteSequentialFile
{
    static void Main()
    {
        const int END = 999;
        const string DELIM = ",";
        const string FILENAME = "EmployeeData.txt";
        Employee emp = new Employee();
        FileStream outfile = new FileStream(FILENAME,
FileMode.Create, FileAccess.Write);
        StreamWriter writer = new StreamWriter(outfile);
        writer.Write("Enter employee number or " + END + ");
        emp.EmpNum = Convert.ToInt32(ReadLine());
        while(emp.EmpNum != END)
        {
            writer.Write("Enter last name >> ");
            emp.Name = ReadLine();
            writer.Write("Enter salary >> ");
            emp.Salary = Convert.ToDouble(ReadLine());
            writer.WriteLine(emp.EmpNum + DELIM + emp.Name + DELIM + emp.Salary);
            writer.Write("Enter next employee number or " + END + ") to quit >> ");
            emp.EmpNum = Convert.ToInt32(ReadLine());
        }
        writer.Close();
        outfile.Close();
    }
}
```

**图 14-11** WriteSequentialFile 程序

## 写入和读取顺序访问文件

在图 14-11 的 `WriteSequentialFile` 程序中，分隔符被定义为字符串而不是字符，以便强制使用 `readline()` 组合的参数。如果发送到 `WriteLine()` 的第一个数据字段是字符串，那么 `DELIM` 可以声明为 `char`。

在图 14-11 的 `WriteSequentialFile` 程序中，常量 `END` 被定义为 999，以便用于检查哨兵值。你首先在第 2 章学习了使用命名常量。定义命名常量可以消在在程序中使用“魔数”（magic number）。魔数一术是指在代码中没有解释的情况下硬编码数字（未命名的字面量）的坏习惯。在大多数情况下，这使得程序更难以阅读、理解和维护。

```
enter employee number or 999 to quit >> 217
enter last name >> Santini
enter salary >> 42000
enter employee number or 999 to quit >> 344
enter last name >> Perez
enter salary >> 51500
enter employee number or 999 to quit >> 510
enter last name >> Schmidt
enter salary >> 61000
enter employee number or 999 to quit >> 510
```

**图 14-12** 典型执行

**图 14-13** 创建的顺序数据文件的内容

```
enter employee number or 999 to quit >> 217
enter last name >> Santini
enter salary >> 42000
enter employee number or 999 to quit >> 344
enter last name >> Perez
enter salary >> 51500
enter employee number or 999 to quit >> 510
enter last name >> Schmidt
enter salary >> 61000
```

## 读取顺序文件

在图 14-11 的 `WriteSequentialFile` 程序中，分隔符被定义为字符串而不是字符，以便强制使用 `readline()` 组合的参数。如果发送到 `WriteLine()` 的第一个数据字段是字符串，那么 `DELIM` 可以声明为 `char`。

在图 14-11 的 `WriteSequentialFile` 程序中，常量 `END` 被定义为 999，以便用于检查哨兵值。你首先在第 2 章学习了使用命名常量。定义命名常量可以消除在程序中使用“魔数”。魔数一术是指在代码中没有解释的情况下硬编码数字（未命名的字面量）的坏习惯。在大多数情况下，这使得程序更难以阅读、理解和维护。

## 文件与流

`WriteLine()` 方法以回车符结束输出。当你使用此方法创建文件输出时，自动追加的回车符就构成了记录分隔符。

图 14-11 包含一个完整的程序，该程序打开一个文件并持续提示用户输入 Employee 数据。图中第一个阴影语句是“引导读入”（priming read）——一个提供第一个数据项或记录的输入语句。在这种情况下，第一个项目是员工编号。如果第一个输入是 `END` 值，则永远进入 `while` 循环。如果输入了有效的员工编号，则在循环内检索记录的其余数据，并在循环底部的第二个阴影语句输入下一个员工。当一个员工的三个字段都输入后，这些字段被写入文件，并用逗号分隔。当用户为员工 ID 输入哨兵值 999 时，数据循环结束，文件关闭。图 14-12 显示了典型的执行过程，图 14-13 显示了创建的顺序数据文件的内容。

为了将 Employee 数据存储到持久化存储设备中，你需要声明一个 `FileStream` 对象来定义存储文件的特征。例如：

```
FileStream outFile = new FileStream(FILENAME,
Mode.Create, FileAccess.Write);
```

然后将 `FileStream` 对象传递给 `StreamWriter` 的构造函数，以便写入文本。例如：

```
StreamWriter writer = new StreamWriter(outFile);
```

然后你可以使用对象的 `writeLine()` 方法将 Employee 数据写入输出流中。你可以使用文本字段和逗号来组合字符串。字符串中表示实体或字段的文本块称为标记（token）。分隔标记的每个逗号都是分隔符（delimiter），它是用于指定文件中数据边界的字符。如果没有分隔符，分离和解释标记的过程将变得更加困难。例如，假设你在以下语句中将逗号定义为分隔符：

```
const string DELIM = ",";
```

那么，当向文件写入数据时，可以使用如下语句通过逗号分隔符分隔字段：
writer.WriteLine(emp.EmpNum + DELIM + emp.Name + DELIM + emp.Salary);

分隔符可以是任何不需要作为文件中数据一部分的字符，但通常使用逗号。包含逗号分隔值的文件通常被称为 CSV 文件。当由于逗号需要作为数据内部的字符而不能用作分隔符时，有时你会使用 Tab 字符、管道符 (|) ，或者使用引号内的逗号。

`WriteLine()` 方法以回车符结束输出。当你使用此方法创建文件输出时，自动追加的回车符就构成了记录分隔符。

图 14-11 包含一个完整的程序，该程序打开一个文件并持续提示用户输入 Employee 数据。图中第一个阴影语句是“引导读入”（priming read）——一个提供第一个数据项或记录的输入语句。在这种情况下，第一个项目是员工编号。如果第一个输入是 `END` 值，则永远进入 `while` 循环。如果输入了有效的员工编号，则在循环内检索记录的其余数据，并在循环底部的第二个阴影语句输入下一个员工。当一个员工的三个字段都输入后，这些字段被写入文件，并用逗号分隔。当用户为员工 ID 输入哨兵值 999 时，数据循环结束，文件关闭。图 14-12 显示了典型的执行过程，图 14-13 显示了创建的顺序数据文件的内容。

```
using System;
using static System.Console;
using System.IO;
class WriteSequentialFile
{
    static void Main()
    {
        const int END = 999;
        const string DELIM = ",";
        const string FILENAME = "EmployeeData.txt";
        Employee emp = new Employee();
        FileStream outfile = new FileStream(FILENAME,
FileMode.Create, FileAccess.Write);
        StreamWriter writer = new StreamWriter(outfile);
        writer.Write("Enter employee number or " + END + ");
        emp.EmpNum = Convert.ToInt32(ReadLine());
        while(emp.EmpNum != END)
        {
            writer.Write("Enter last name >> ");
            emp.Name = ReadLine();
            writer.Write("Enter salary >> ");
            emp.Salary = Convert.ToDouble(ReadLine());
            writer.WriteLine(emp.EmpNum + DELIM + emp.Name + DELIM + emp.Salary);
            writer.Write("Enter next employee number or " + END + ") to quit >> ");
            emp.EmpNum = Convert.ToInt32(ReadLine());
        }
        writer.Close();
        outfile.Close();
    }
}
```

**图 14-11** WriteSequentialFile 程序

在图 14-11 的 `WriteSequentialFile` 程序中，分隔符被定义为字符串而不是字符，以便强制使用 `readline()` 组合的参数。如果发送到 `WriteLine()` 的第一个数据字段是字符串，那么 `DELIM` 可以声明为 `char`。

在图 14-11 的 `WriteSequentialFile` 程序中，常量 `END` 被定义为 999，以便用于检查哨兵值。你首先在第 2 章学习了使用命名常量。定义命名常量可以消除在程序中使用“魔数”。魔数一术是指在代码中没有解释的情况下硬编码数字（未命名的字面量）的坏习惯。在大多数情况下，这使得程序更难以阅读、理解和维护。

```
enter employee number or 999 to quit >> 217
enter last name >> Santini
enter salary >> 42000
enter employee number or 999 to quit >> 344
enter last name >> Perez
enter salary >> 51500
enter employee number or 999 to quit >> 510
enter last name >> Schmidt
enter salary >> 61000
```

**图 14-12** 典型执行

**图 14-13** 创建的顺序数据文件的内容

```
enter employee number or 999 to quit >> 217
enter last name >> Santini
enter salary >> 42000
enter employee number or 999 to quit >> 344
enter last name >> Perez
enter salary >> 51500
enter employee number or 999 to quit >> 510
enter last name >> Schmidt
enter salary >> 61000
```

