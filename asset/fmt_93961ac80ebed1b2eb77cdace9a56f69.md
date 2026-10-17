
```csharp
        MessageBox.Show("Done");

    } catch (Exception ex) {

        // 显示错误消息。

        MessageBox.Show(ex.Message);

    }

}
```

## 7.3 处理文件与数组

`try-catch`语句处理任何与文件相关的错误。以下是块内代码的摘要：

- 第 6 行创建了一个具有五个元素的`int`数组，初始化值为 10, 20, 30, 40 和 50。
- 第 9 行声明了一个名为`outputFile`的`StreamWriter`。（你在这个代码示例中没有看到它，但在文件顶部出现了使用`System.IO`的直接指令。这对于第 9 行中的`StreamWriter`声明是必须的）。
- 第 12 行创建了一个名为`Values.txt`的文件。在该语句执行后，`outputFile`将引用一个与关联的`StreamWriter`对象。
- 第 15 行是`for`循环的开始。循环为数组的每个元素迭代一次。在循环迭代期间，`index`变量将被赋值为 1, 2, 3, 4 和 5。
- 在循环内部，第 17 行将数组元素`numbers[index]`写入文件。
- 第 21 行关闭文件。
- 第 24 行显示一个消息框，让用户知道操作已完成。

图 7-13 显示了在点击 OK 按钮后，在记事本中打开的`Values.txt`文件的内容。

### 图 7-13 Values.txt 的内容

![](img/8a88e1d8c69a687988c05f162ce32cac_421_0.png)

### 从文件读取值并存储在数组中

将文件内容读取到数组也是直接的：打开文件并使用循环从文件中读取每个项，将每个项存储在数组元素中。循环应该一直迭代，直到数组填满或到达文件末尾。例如，在学生示例程序的`Chap07`文件夹中，你会找到一个名为`File Array`的程序。当你点击`Get Values`按钮时，应用程序从名为`Values.txt`的文件中读取值到`int`数组中。数组的内容将显示在列表框中。以下代码显示了`Get Values`的处理程序。

```csharp
private void getValues_ButtonClick(object sender, EventArgs e)
{
    try {
        // 创建一个数组来存放项。
        const int SIZE = 5;
        int[] numbers = new int[SIZE];
        // 一个 StreamReader 变量。
        StreamReader inputFile;
        // 打开文件并获取 StreamWriter 对象。
        inputFile = new StreamReader("Values.txt");
        // 将数组的内容读取到数组中。
        int index = 0;
        while (index < numbers.Length && !inputFile.EndOfStream)
        {
            // 读取一行文本，将其转换为 int，
            numbers[index] = int.Parse(inputFile.ReadLine());
            index++;
        }
        // 关闭文件。
        inputFile.Close();
        // 在列表框中显示数组。
        foreach (int value in numbers)
        {
            outputListBox.Items.Add(value);
        }
    } catch (Exception ex) {
        // 显示错误消息。
        MessageBox.Show(ex.Message);
    }
}
```

## 第 7 章 数组与列表

### 图 7-14 File Array 表单

![](img/8a88e1d8c69a687988c05f162ce32cac_423_0.png)

## 7.4 将数组作为参数传递给方法

**概念：** 数组可以作为参数传递给方法。传递数组时，传递引用该数组的变量。

有时你希望编写一个接受整个数组作为参数并对数组执行操作的方法。例如，下面的代码显示了一个名为`ShowArray`的方法。该方法接受字符串数组作为参数，并在消息框中显示每个元素。

```csharp
private void ShowArray(string[] strArray)
{
    foreach (string str in strArray)
    {
        MessageBox.Show(str);
    }
}
```

在第 1 行中，方法有一个名为`strArray`的参数，且该参数的数据类型为`string[]`，这表示该变量是字符串数组的引用。当你调用它时，必须传递一个字符串数组作为参数。

当你调用方法并将数组作为参数传递时，你只需要传递引用该数组的变量。接下来的代码显示了`ShowArray`方法（之前所示）的调用方式示例：

```csharp
// 创建一个字符串数组。
string[] people = { "Bill", "Jill", "Phil", "Will" };
// 将数组传递给 ShowArray 方法。
ShowArray(people);
```

记住，数组*总是*通过引用传递的。当你将数组作为参数传递时，传递到参数变量中的是对数组的引用。这在图 7-15 中有所插图。如图所示，当变量传递给`ShowArray`方法时，引用被传递到`strArray`参数变量。图 7-16 显示了当`ShowArray`方法执行时，`people`变量和`strArray`变量引用内存中的同一个数组。

### 424 第 7 章 数组与列表

### 图 7-15 作为参数传递的数组

![](img/8a88e1d8c69a687988c05f162ce32cac_424_0.png)

### 图 7-16 people 和 strArray 变量引用同一个数组

![](img/8a88e1d8c69a687988c05f162ce32cac_424_1.png)

由于数组总是通过引用传递的，因此接收数组作为参数的方法可以访问实际数组（而不是数组的副本）。例如，在学生示例程序的`Chap07`文件夹中，你会找到一个名为`Array Argument`的项目。图 7-17 显示了用户点击 Go 按钮后的应用程序表单。

### 图 7-17 Array Argument 应用程序

![](img/8a88e1d8c69a687988c05f162ce32cac_424_2.png)

## 7.4 将数组作为参数传递给方法

Go 按钮。以下代码显示了 Go 按钮的 Click 事件处理程序以及一个名为`SetToZero`的方法：

```csharp
// goButton 控制的 Click 事件处理程序。
private void goButton_Click(object sender, EventArgs e)
{
    // 创建一个 int 数组。
    int[] numbers = { 1, 2, 3 };
    // 在列表框中显示数组。
    outputListBox.Items.Add("The array's original contents:");
    foreach (int number in numbers)
        outputListBox.Items.Add(number);
    // 将数组传递给 SetToZero 方法。
    SetToZero(numbers);
    // 再次在列表框中显示数组。
    outputListBox.Items.Add("");
    outputListBox.Items.Add("After calling SetToZero:");
    foreach (int number in numbers)
        outputListBox.Items.Add(number);
}
```

```csharp
// SetToZero 方法接收 int 数组作为参数并将其元素设置为 0。
private void SetToZero(int[] iArray)
{
    for (int index = 0; index < iArray.Length; index++)
        iArray[index] = 0;
}
```

让我们仔细观察`goButton_Click`事件处理程序：

- 第 5 行创建了一个名为`numbers`的`int`数组，并初始化值为 1、2 和 3。
- 第 8 行在`outputListBox`中显示“The array's original contents”。
- 第 9-12 行的循环在`outputListBox`中显示数组的内容。查看图 7-17，注意数组的值为 1、2 和 3。
- 第 15 行调用了`SetToZero`方法，并将数组作为参数传递。。
- 第 18 行在`outputListBox`控件中显示一个空行，第 19 行显示字符串“After calling SetToZero:”：
- 第 20-22 行的循环在`outputListBox`中显示数组的内容。查看图 7-17，注意数组的值为 0、0 和 0。

正如你从图 7-17 中所示，`SetToZero`方法更改了存储在`numbers`数组中的值。让我们来看看`SetToZero`方法：

- 注意第 28 行，该方法接收一个`int`数组作为参数。参数变量名为`iArray`。

### 426 第 7 章 数组与列表

- 第 30 行是`for`循环的开始，该循环遍历数组。循环迭代时，`index`变量被赋予 0、1、2 等值。只要`index`小于`iArray.Length`，循环就会继续执行。
- 第 32 行的语句将 0 赋值给数组元素`iArray[index]`。

由于`iArray`参数是所作为参数传递的数组的引用，因此第 32 行的语句将 0 赋值给`numbers`数组的一个元素。

## 在数组参数中使用 ref 和 out

你在上一个示例中看到数组总是通过引用传递的。。当你将数组作为参数传递给方法时，该方法可以通过其参数变量直接访问该数组。然而，该方法无法访问用于传递数组的原始引用变量。例如，在示例程序的`Chap7`文件夹中，你会找到一个名为`Change Array 1`的项目。图 7-18 显示了用户点击 Go 按钮后的应用程序表单。以下代码显示了 Go 按钮的 Click 事件处理程序以及名为`ChangeArray`的方法：

### 图 7-18 Change Array 1 应用程序

![](img/8a88e1d8c69a687988c05f162ce32cac_426_0.png)

```csharp
private void goButton_Click(object sender, EventArgs e)
{
    // 创建一个 int 数组。
    int[] numbers = { 1, 2, 3 };
    // 显示 numbers 数组的内容。
    outputListBox.Items.Add("The array's original contents:");
    foreach (int value in numbers)
    {
        outputListBox.Items.Add(value);
    }
    // 将 numbers 数组传递给 ChangeArray。
    ChangeArray(numbers);
    // 显示 numbers 数组的内容。
    outputListBox.Items.Add("After calling SetToZero:");
    foreach (int value in numbers)
    {
        outputListBox.Items.Add(value);
    }
}
```

## 7.4 将数组作为参数传递给方法

```csharp
private void ChangeArray(int[] iArray)
{
    for (int index = 0; index < iArray.Length; index++)
        iArray[index] = 0;
}
```

让我们仔细观察`goButton_Click`事件处理程序：

- 第 3 行创建了一个名为`numbers`的`int`数组，并初始化值为 1、2 和 3。
- 第 6 行在`outputListBox`中显示“The array's original contents”。
- 第 7-10 行的循环在`outputListBox`中显示数组的内容。查看图 7-17，注意数组的值为 1、2 和 3。
- 第 13 行调用了`ChangeArray`方法，并将数组作为参数传递。
- 第 16 行在`outputListBox`控件中显示一个空行，第 17 行显示字符串“After calling SetToZero:”：
- 第 18-20 行的循环在`outputListBox`中显示数组的内容。查看图 7-17，注意数组的值为 0、0 和 0。

正如你从图 7-17 中所示，`SetToZero`方法更改了存储在`numbers`数组中的值。让我们来看看`SetToZero`方法：

- 注意第 28 行，该方法接收一个`int`数组作为参数。参数变量名为`iArray`。

## 在数组参数中使用 ref 和 out

你在上一个示例中看到数组总是通过引用传递的。。当你将数组作为参数传递给方法时，该方法可以通过其参数变量直接访问该数组。然而，该方法无法访问用于传递数组的原始引用变量。例如，在示例程序的`Chap7`文件夹中，你会找到一个名为`Change Array 1`的项目。图 7-18 显示了用户点击 Go 按钮后的应用程序表单。以下代码显示了 Go 按钮的 Click 事件处理程序以及名为`ChangeArray`的方法：

```csharp
private void goButton_Click(object sender, EventArgs e)
{
    // 创建一个 int 数组。
    int[] numbers = { 1, 2, 3 };
    // 显示 numbers 数组的内容。
    outputListBox.Items.Add("The array's original contents:");
    foreach (int value in numbers)
    {
        outputListBox.Items.Add(value);
    }
    // 将 numbers 数组传递给 ChangeArray。
    ChangeArray(numbers);
    // 显示 numbers 数组的内容。
    outputListBox.Items.Add("After calling SetToZero:");
    foreach (int value in numbers)
    {
        outputListBox.Items.Add(value);
    }
}
```

### 图 7-18 Change Array 1 应用程序

![](img/8a88e1d8c69a687988c05f162ce32cac_426_0.png)

## 7.4 将数组作为参数传递给方法

```csharp
private void ChangeArray(int[] iArray)
{
    for (int index = 0; index < iArray.Length; index)
        iArray[index] = 0;
}
```
