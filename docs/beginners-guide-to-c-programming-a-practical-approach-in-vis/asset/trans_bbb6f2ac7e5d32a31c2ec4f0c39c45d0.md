
variable_type[] newArray = new variable_type[number_of_elements]

代码 10.2

例如，以下代码行创建了一个具有整数类型元素的三元素数组：

```
int[] myIntArray = new int[3];
```

代码 10.2

我们也可以在声明时初始化数组。例如，让我们创建一个包含元素 4、55、102 的整数数组：

```
int[] myNewArray = {4, 55, 102};
```

代码 10.3

由于我们在此代码中初始化了数组，因此无需显式指定其元素数量。

让我们在一个项目中声明一个数组并在 ListBox 中显示其元素。

- 1. 创建一个新的 C# 项目。
- 2. 在窗体上添加一个 Button 和一个 ListBox。
- 3. 分别将 Button 的 Name 和 Text 设置为 showButton 和 Show。
- 4. 将 ListBox 的 Name 设置为 showListBox。窗体将如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_255_0.png)

图 10.1. 窗体的布局

- 5. 双击 Button 以创建其事件处理程序 `showButton_Click(...)`。我们所有的代码都将进入此方法。
- 6. 让我们按如下方式声明并初始化一个名为 myIntArray 的数组：

```csharp
int[] myIntArray = { 3, 5, 7, 8, 10 };
```

代码 10.4

这是一个包含 5 个元素的整数数组，如下所示：

| 索引 | 元素 |
|---:|---:|
| 0 | 3 |
| 1 | 5 |
| 2 | 7 |
| 3 | 8 |
| 4 | 10 |

表 10.1. 已声明数组元素的索引

- 7. 我们将在 showListBox 中显示此数组的元素。我们需要遍历数组中的所有元素。一种方法是获取数组的元素数量，然后构造一个 **for** 循环进行遍历。然而，**foreach** 循环一次完成所有这些操作。以下 foreach 循环遍历数组中的所有元素并将它们插入到 ListBox 中：

```csharp
foreach (int item in myIntArray)
{
    showListBox.Items.Add(item);
}
```

代码 10.5

在此代码中，整数变量 item 在循环中一次持有数组元素的数值。然后，在每次循环中，此值被插入到 ListBox 中。Click 事件处理程序方法的完整代码如下：

```csharp
private void showButton_Click(object sender, EventArgs e)
{
    int[] myIntArray = { 3, 5, 7, 8, 10 };
    foreach (int item in myIntArray)
    {
        showListBox.Items.Add(item);
    }
}
```

代码 10.6（续）

8. 构建并运行代码。当单击 Show 按钮时，我们的数组元素将显示在 ListBox 中，如图 10.2 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_257_0.png)

图 10.2. 使用 foreach 循环将数组元素插入到 ListBox 中

9. 我们可以修改数组以保存字符串元素，并相应地修改 foreach 循环的变量类型，如下所示：

```csharp
private void showButton_Click(object sender, EventArgs e)
{
    string[] myStringArray = { "John", "James", "Joseph" };
    foreach (string item in myStringArray)
    {
        showListBox.Items.Add(item);
    }
}
```

代码 10.7

构建项目并单击 Show 按钮后，字符串数组的元素现在将显示在 ListBox 中：

相关联的数组元素 myStringArray[i, jj] 由代码行 arrayListBox.Items.Add(myStringArray[i, jj]); 添加到 ListBox 中。

8. 构建并运行项目。程序窗口将如 图 10.5 所示。当单击 List elements 按钮时，数组的元素将写入 ListBox，如 图 10.6 所示。

![](img/41d82527c4e41cdb7e56259564306ddc_261_0.png)

图 10.5. 程序窗口

![](img/41d82527c4e41cdb7e56259564306ddc_261_1.png)

图 10.6. 数组元素列在 ListBox 中

注意 ListBox 中元素的顺序。它们类似于 [0, 0]、[0, 1]、[0, 2]、[1, 0]、...、[1, 2]。从此顺序可以看出，i) 第一个循环

3. 分别将 Button 的 Name 和 Text 属性设置为 **resizeButton** 和 **Resize**。

4. 将 ListBox 的 Name 设置为 **elementsListBox**。窗体可能如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_263_0.png)

图 3.10. 窗体布局

5. 双击 Button 以创建其 Click 事件处理程序方法，然后在此方法中插入代码行 10.13、10.14 和 10.15。让我们也使用 foreach 循环来在 ListBox 上显示数组的元素。添加这些内容后，事件处理程序方法将如下所示：

```csharp
string[] myArray = {"Water", "Soda water", "Orange juice",
"Lemonade" };
private void resizeButton_Click(object sender, EventArgs e)
{
    Array.Resize(ref myArray, 5);
    myArray[4] = "Tea";
    foreach (string item in myArray)
    {
        elementsListBox.Items.Add(item);
    }
}
```

代码 10.15

请注意，我们在事件处理程序之前声明并初始化了数组，即全局区域，这样我们就可以在其他事件处理程序中也使用此数组。

6. 构建并运行项目。当单击 Resize 按钮时，数组将被调整大小，并且元素 "Tea" 将被追加并显示在 ListBox 上：

![](img/41d82527c4e41cdb7e56259564306ddc_264_0.png)

图 10.8. 调整大小后的数组元素

## 10.1.3.2. Copy() 方法

此方法用于从一个数组复制单个元素到另一个数组。

Copy() 方法的使用方式如下：

```
Copy(original_array, index, destination_array, index, number_of_elements_to_be_copied);
```

代码 10.16

如果我们将 number_of_elements_to_be_copied 指定为 1，则只复制一个元素，否则我们可以在单行代码中复制多个元素。让我们在最近为 Resize() 方法开发的项目中使用此方法：

- 1. 在窗体上 Resize 按钮下方添加一个 Button。
- 2. 将 Button 的 Name 和 Text 属性分别设置为 copyButton 和 Copy。窗体将如下所示：

![](img/41d82527c4e41cdb7e56259564306ddc_267_0.png)

图 10.11. 窗体的布局

- 3. 双击 **Set and Get** 按钮并创建其事件处理程序方法。我们将在此方法中使用 `setValue()` 和 `getValue()` 方法。
- 4. 让我们首先使用 `setValue()` 方法将 myArray 的第二个元素设置为 "Coffee"，如下所示：

```
myArray.SetValue("Coffee", 1);
```

代码 10.21

- 5. 我们可以使用 for 循环在 ListBox 上显示数组元素：

```csharp
for (int i = 0; i < myArray.Length; i++)
{
    elementsListBox.Items.Add(myArray.GetValue(i));
}
```

代码 10.22

在此代码中，我们使用 `getValue()` 方法按 `myArray.GetValue(i)` 读取索引 `i` 处的值。整个事件处理程序方法将如下所示：

```csharp
private void setGetButton_Click(object sender, EventArgs e)
{
    myArray.SetValue("Coffee", 1);
    for (int i = 0; i < myArray.Length; i++)
```

```
newHt.Add("Physics", 10);
newHt.Add("Maths", 9);
newHt.Add("Literature", 9);
newHt.Add("History", 7);
```

代码 10.25

9. 我们将在 ListBox 中显示键值对。为此，让我们首先获取 Hashtable 的键：

```
ICollection keys = newHt.Keys;
```

代码 10.26

10. 我们现在可以使用 foreach 循环遍历这些键：

```
foreach (string key in keys)
{
    displayListBox.Items.Add(key + "->" + newHt[key]);
}
```

代码 10.27

正如您从此代码中看到的，Hashtable newHt 的值是通过表达式 newHt[key] 访问的，类似于访问数组元素。从这个角度来看，我们可以将数组视为具有固定键 0、1、2 等的 Hashtable。键值对将作为 key -> value 写入 ListBox，这得益于表达式 key + "->" + newHt[key] 设置的字符串连接。

整个事件处理程序方法将由以下这些代码行填充：

```csharp
private void keyValueButton_Click(object sender, EventArgs e)
{
    Hashtable newHt = new Hashtable();
    newHt.Add("Physics", 10);
    newHt.Add("Maths", 9);
    newHt.Add("Literature", 9);
    newHt.Add("History", 7);
    
    ICollection keys = newHt.Keys;
    foreach (string key in keys)
    {
        displayListBox.Items.Add(key + "->" + newHt[key]);
    }
}
```
