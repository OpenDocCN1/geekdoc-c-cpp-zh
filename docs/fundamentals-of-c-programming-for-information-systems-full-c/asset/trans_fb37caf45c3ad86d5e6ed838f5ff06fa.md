

图 8-11 中的第 93–106 行显示了代码的第二部分，该部分显示成绩百分比高于班级平均分的学生的姓名和分数。第 20–92 行计算班级平均分，与前面讨论的图 8-10 相同。

## 图 8-11：计算平均分并显示高于平均分学生的代码

```
private void btnAboveAvg_Click(object sender, EventArgs e)
{
    //Declare two 1-D arrays
    string[] names = new string[10];
    float[] percentScores = new float[10];
    // percentScores is the array of all percent scores
    int recordCount, index = 0;

    string currentLine;
    string[] fields;
    float percentScore, classTotal = 0, classAvg;
    //percentScore is the percent score for a student;
    StreamReader examsReader = new StreamReader("Exams.txt");

    while (examsReader.EndOfStream == false)
    {
        currentLine = examsReader.ReadLine(); // read current line
        fields = currentLine.Split(','); // split current line
        percentScore = (float.Parse(fields[1]) + float.Parse(fields[2])) / 2;

        names[index] = fields[0]; //Store name into current element of names array
        percentScores[index] = percentScore; // Store percent into percentScores
        index = index + 1;
        classTotal = classTotal + percentScore; // Add current percent to classTotal
    }
    recordCount = index;
    classAvg = classTotal / (float) recordCount;

    string fmtStr = "{0,-15}{1,12:N1}{2,12:N1}";
    lstDisplay.Items.Clear();
    lstDisplay.Items.Add("Above average students");
    lstDisplay.Items.Add(string.Format(fmtStr, "Name", "Percent", "Class Avg"));

    //Find above average students
    for (index = 0; index < recordCount; index++)
    {
        if (percentScores[index] > classAvg)
            lstDisplay.Items.Add(string.Format(fmtStr, names[index],
                percentScores[index], classAvg));
    }
    examsReader.Close();
}
```

## 第 101 行：if (percentScores[index] > classAvg)

由于循环变量的取值范围为 0 到 4，第 101 行等价于
if (percentScores[0] > classAvg)
if (percentScores[1] > classAvg)
if (percentScores[2] > classAvg)
等等。

因此，语句 if (percentScores[index] > classAvg) 将 percentScores 的每个元素与 classAvg 进行比较。

## 第 102 行：lstDisplay.Items.Add(string.Format(fmtStr, names[index], percentScores[...]));

如果 percentScores 的任何元素大于 classAvg，则第 102 行会使用相同的索引值从 names 数组的对应元素中显示姓名。

步骤 1-11：将图 8-11 中第 99–104 行的缺失代码添加到 btnAboveAvg 的 Click 事件处理程序中以显示高于平均分的学生。在第 102 行和第 104 行处设置断点。

步骤 1-12：运行项目。当程序中断时，观察 classAvg 以及 names 和 percentScore 数组的值。

## 是时候练习了！做练习 8-2

## StreamReader 的 ReadBlock 方法

除了使用 ReadLine 方法读取整行之外，您还可以从当前行的指定位置开始读取指定数量的字符到字符数组中。例如，以下语句从索引 0 开始读取 10 个字符到名为 studentArray 的字符数组中：

```
examsReader.ReadBlock(studentArray, 0, 10);
```

## StreamReader 的 ReadToEnd 方法

StreamReader 的 ReadToEnd 方法从当前位置开始读取整个文件并返回一个字符串。以下语句将读取整个文件 Exams.txt 并将其显示在 ListBox lstDisplay 中：

```
lstDisplay.Items.Add(examsReader.ReadToEnd);
```

## 复习问题

8.4 以下是在名为 Orders.txt 的文本文件中存储的订单数据（客户#、订单#、订单数量、单价）的示例。

0155, 76533, 3, 10.95
0140, 75446, 12, 8.50
0150, 75550, 1, 89.95
0145, 75648, 25, 2.50

以下代码旨在从上述文件读取数据并计算并显示每个订单的扩展成本（= 订单数量 x 单价）。计算扩展成本的语句不完整。

```
StreamReader OrdersReader = new StreamReader("Orders.txt");
string[] fields;
float extCost;
while (OrdersReader.EndOfStream == false)
{
    currentLine = OrdersReader.ReadLine();
    fields = currentLine.Split(',');
    // insert code to compute extCost (= Order Qty x Unit Price)
    extCost =
    lstDisplay.Items.Add(extCost);
}
```

插入必要的代码来计算 extCost。

8.5 以下是在名为 Orders.txt 的文本文件中存储的订单数据（客户#、订单#、订单数量、单价）的示例。

0155, 76533, 3, 10.95
0140, 75446, 12, 8.50
0150, 75550, 1, 89.95
0145, 75648, 25, 2.50

以下代码旨在从上述文件读取数据，为每个订单计算扩展成本（= 订单数量 x 单价），并将订单#和扩展成本存储在两个不同的数组（orderNumbers 和 extCosts）中。存储订单#和扩展成本到数组的语句缺失。

```
StreamReader OrdersReader = new StreamReader("Orders.txt");
string[] fields;
float extCost;
int index = 0;
string[] orderNumbers = new string[10];
float[] extCosts = new float[10];
while (OrdersReader.EndOfStream == false)
{
    currentLine = OrdersReader.ReadLine();
    fields = currentLine.Split(',');
    extCost = float.Parse(fields[2])*float.Parse(fields[3]);
    // insert code to store Order# into the array, orderNumbers
    ...
    // insert code to store extended cost into the array, extCosts
    ...
    index = index + 1;
}
```

插入缺失的代码以将订单#存储到数组 orderNumbers 中，并将扩展成本存储到数组 extCosts 中。

代码的一个主要特点是，只要从文件中读取的记录数等于数组的大小，数组的大小就会动态增加。因此，该代码旨在从包含大量记录的文件中读取，并且预计会增长。这里实际使用的文件（Vendor.txt） however 非常小，以便于跟踪代码的执行并测试循环。

读取每行中的七个数据项并将姓名和电话号码添加到两个数组中的代码的第一部分显示在图 8-12 中。

## 图 8-12：使用 Array.Resize 方法的 LargeFiles 表单

```
20  | string[] names, phoneNumbers; //Declare arrays.
21    int recordCount = 0;

23  □ private void LargeFiles_Load(object sender, EventArgs e)
24  {
25      string currentLine;
26      int arrayInitialSize = 10000, arrayIncrement = 5000;
27      string[]fields = new string[7]; // Declare an array named fields
28      StreamReader vendorReader = new StreamReader("Vendor.txt");

30      names = new string[arrayInitialSize];
31      phoneNumbers = new string[arrayInitialSize];

      // Read each line, split it, and store name & phone number into two arrays.
      while (vendorReader.EndOfStream == false)
      {
          // If the names array is full, increase the size of arrays.
          if (recordCount == names.Length)
          {
              Array.Resize(ref names, names.Length + arrayIncrement);
              Array.Resize(ref phoneNumbers, phoneNumbers.Length + arrayIncrement);
          }
          currentLine = vendorReader.ReadLine();
          fields = currentLine.Split(','); // split the line

          names[recordCount] = fields[1]; //Store name into the array, names
          phoneNumbers[recordCount] = fields[6]; //Store phone number in phoneNumbers
          recordCount = recordCount + 1;
      }
      vendorReader.Close();
  }
```

读取每行、将其拆分为不同的数据项并将七个数据项存储在临时数组（第 42 行和第 43 行）中的过程与我们在 ReadTextFiles 表单中早期使用的方法类似。记录存储在临时数组 fields 中后，您将存储供应商名称（第二个元素；索引 1）和电话号码（第七个元素；索引 6）到数组 names 和 phone numbers 中（第 45 行和第 46 行）。

让我们看一下代码的一些关键部分：

