
Although string interpolation has very nearly made this version of the *WriteLine* method redundant, this overload was frequently used in previous editions of the C# language. This overload enables the *WriteLine* method to support a format string argument that contains numeric placeholders, each of which can be replaced at run time with a variable of any type that is specified as a list of parameters (placeholder {i} is replaced with the ith variable in the list that follows). Here’s an example of a call to this method (the variables *fname* and *lname* are *strings*, *mi* is a *char*, and *age* is an *int*):

```
Console.WriteLine("Forename:{0}, Middle Initial:{1}, Last name:{2}, Age:{3}", fname, mi, lname, age);
```

The compiler resolves this call into the following:

```
Console.WriteLine("Forename:{0}, Middle Initial:{1}, Last name:{2}, Age:{3}", new object[4]{fname, mi, lname, age});
```

## Using a *params* array

In the following exercise, you will implement and test a static method named `Sum`.

The purpose of this method is to calculate the sum of a variable number of int arguments passed to it, returning the result as an int. You will do this by writing `Sum` to take a `params int[]` parameter. You will implement two checks on the params parameter to ensure that the `Sum` method is completely robust. You will then call the `Sum` method with a variety of different arguments to test it.

### Write a params array method

1. Start Microsoft Visual Studio 2015 if it is not already running.
2. Open the `ParamsArray` project, which is located in the `\Microsoft Press\VCSBS\Chapter 11\ParamsArray` folder in your Documents folder.
   The `ParamsArray` project contains the `Program` class in the `Program.cs` file, including the `doWork` method framework that you have seen in previous chapters. You will implement the `Sum` method as a static method of another class called `Util` (short for “utility”), which you will add to the project.
3. In Solution Explorer, right-click the `ParamsArray` project in the `ParamsArray` solution, point to Add, and then click Class.
4. In the Add New Item – ParamsArray dialog box, in the middle pane, click the Class template. In the Name box, type `Util.cs`, and then click Add.
   The `Util.cs` file is created and added to the project. It contains an empty class named `Util` in the `ParamsArray` namespace.
5. Add a public static method named `Sum` to the `Util` class. This method should return an int and accept a params array of int values named `paramList`. It should look like this:

```
public static int Sum(params int[] paramList)

{

}
```

The first step in implementing the `Sum` method is to check the `paramList` parameter. Apart from containing a valid set of integers, it can also be null or it can be an array of zero length. In both of these cases, it is difficult to calculate the sum, so the best option is to throw an `ArgumentException` exception. (You could argue that the sum of the integers in a zero-length array is 0, but you’ll treat this situation as an exception in this example.)

6. Add to `Sum` the following code shown in bold. This code throws an `ArgumentException` exception if `paramList` is null. The `Sum` method should now look like this:

```
public static int Sum(params int[] paramList)

{

    if (paramList == null)

{

    throw new ArgumentException("Util.Sum: null parameter list");

}

}
```

7. Add code to the `Sum` method to throw an `ArgumentException` exception if the length of the parameter list array is 0, as shown here in bold:

```
public static int Sum(params int[] paramList)

{

    if (paramList == null)

    {

        throw new ArgumentException("Util.Sum: null parameter list");

    }

    if (paramList.Length == 0)

    {

        throw new ArgumentException("Util.Sum: empty parameter list");

    }

}
```

If the array passes these two tests, the next step is to add together all the elements inside the array. You can use a foreach statement to do this, and you will need a local variable to hold the running total.

8. Declare an integer variable named `sumTotal` and initialize it to 0, directly following the code from the preceding step.

```
public static int Sum(params int[] paramList)

{

    ...

    if (paramList.Length == 0)

    {

        throw new ArgumentException("Util.Sum: empty parameter list");

    }

    int sumTotal = 0;

}
```

9. Add a foreach statement to the `Sum` method to iterate through the `paramList` array. The body of this foreach loop should add each element in the array to `sumTotal`. At the end of the method, return the value of `sumTotal` by using a return statement, as shown in bold here:

```
public static int Sum(params int[] paramList)

{

```
...
int sumTotal = 0;
foreach (int i in paramList)
{
    sumTotal += i;
}
return sumTotal;
}
```

10. 在“生成”菜单上，单击“生成解决方案”，然后确认解决方案在没有任何错误的情况下生成。

### 测试 Util.Sum 方法

1. 在代码和文本编辑器窗口中显示 `Program.cs` 文件。
2. 在代码和文本编辑器窗口中，删除 `// TODO:` 注释并在 `doWork` 方法中添加以下语句：

```
Console.WriteLine(Util.Sum(null));
```

3. 在“调试”菜单上，单击“不调试启动”。

程序生成并运行，将以下消息写入控制台：

```
Exception: Util.Sum: null parameter list
```

这证实了该方法中的第一个检查有效。

4. 按 Enter 键关闭程序并返回 Visual Studio 2015。
5. 在代码和文本编辑器窗口中，按如下所示更改 `doWork` 中的 `Console.WriteLine` 调用：

```
Console.WriteLine(Util.Sum());
```

这次，方法不带任何参数调用。编译器将空参数列表转换为一个空数组。

6. 在“调试”菜单上，单击“不调试启动”。

程序生成并运行，将以下消息写入控制台：

```
Exception: Util.Sum: empty parameter list
```

这证实了该方法中的第二个检查有效。

7. 按 Enter 键关闭程序并返回 Visual Studio 2015。
8. 按如下方式更改 `doWork` 中的 `Console.WriteLine` 调用：

```
Console.WriteLine(Util.Sum(10, 9, 8, 7, 6, 5, 4, 3, 2, 1));
```

9. 在“调试”菜单上，单击“不调试启动”。

验证程序生成、运行并将值 55 写入控制台。

10. 按 Enter 关闭应用程序并返回 Visual Studio 2015。

### 比较参数数组和可选参数

第 3 章“编写方法并应用作用域”说明了如何定义接受可选参数的方法。乍一看，使用参数数组的方法和接受可选参数的方法之间似乎存在一定程度的重叠。然而，它们之间存在根本差异：

+ 接受可选参数的方法仍然具有固定的参数列表，并且你不能传递任意的实参列表。编译器会在方法运行之前为任何缺失的参数生成插入默认值到栈上的代码，并且方法无法得知哪些参数是由调用方提供的，哪些是编译器生成的默认值。
+ 使用参数数组的方法实际上具有完全任意的参数列表，并且其中没有任何一个参数有默认值。此外，方法可以准确地确定调用方提供了多少个参数。

通常，你对可以接受任意数量参数（包括零个）的方法使用参数数组，而仅在不方便强制调用方为每个参数提供实参时才使用可选参数。

还有一个最后值得思考的情况。如果定义了一个接受参数列表的方法并提供了一个接受可选参数的重载，如果调用语句中的实参列表同时匹配两个方法签名，则并不总是立即清楚将调用哪个版本的方法。你将在本章的最后练习中研究此场景。

#### 比较 params 数组和可选参数

1. 返回 Visual Studio 2015 中的 `ParamsArray` 解决方案并在代码和文本编辑器窗口中显示 `Util.cs` 文件。
2. 在 `Util` 类的 `Sum` 方法开头添加以下以粗体显示的 `Console.WriteLine` 语句：

```
public static int Sum(params int[] paramList)
{
    Console.WriteLine("Using parameter list");
    ...
}
```

3. 向 `Util` 类添加另一个 `Sum` 方法的实现。此版本应接受四个可选的 int 参数，每个参数的默认值均为 0。在方法体中，输出消息“Using optional parameters”然后计算并返回四个参数的和。完成的方法应如下所示的代码以粗体显示：

```
class Util
{
    ...
    public static int Sum(int param1 = 0, int param2 = 0, int param3 = 0, int param4 = 0)
    {
        Console.WriteLine("Using optional parameters");
        int sumTotal = param1 + param2 + param3 + param4;
        return sumTotal;
    }
}
```

4. 在代码和文本编辑器窗口中显示 `Program.cs` 文件。
5. 在 `doWork` 方法中，注释掉现有代码并添加以下语句：

```
Console.WriteLine(Util.Sum(2, 4, 6, 8));
```

此语句调用 `Sum` 方法，传递四个 int 参数。此调用同时匹配 `Sum` 方法的两个重载。

6. 在“调试”菜单上，单击“不调试启动”以生成并运行应用程序。

应用程序运行时，显示以下消息：

```
Using optional parameters
20
```

在这种情况下，编译器生成了调用接受四个可选参数的方法的代码。这是与方法调用最接近匹配的方法版本。

7. 按 Enter 并返回 Visual Studio。
8. 在 `doWork` 方法中更改调用 `Sum` 方法的语句并删除最后一个参数（8），如下所示：

```
Console.WriteLine(Util.Sum(2, 4, 6));
```

9. 在“调试”菜单上，单击“不调试启动”以生成并运行应用程序。

应用程序运行时，显示以下消息：

```
Using optional parameters
12
```

编译器仍然生成了调用接受可选参数的方法的代码，即使方法签名与调用不完全匹配。C# 编译器在参数数组方法和可选参数方法之间进行选择时，将使用接受可选参数的方法。

10. 按 Enter 并返回 Visual Studio。
11. 在 `doWork` 方法中再次更改调用 `Sum` 方法的语句并添加两个更多参数：
