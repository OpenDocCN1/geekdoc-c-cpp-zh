
```csharp
private void btnSaveRecord_Click(object sender, EventArgs e)
{
    AutoStruct newStruct = new AutoStruct();
    //
    string myMfg = "";// #1 制造商
    myMfg = txtBoxMfg.Text;
    newStruct.CarBuilder = myMfg;
    //
    string myAutoModel = "";// #2 型
    myAutoModel = txtBoxModel.Text;
    newStruct.CarModel = myAutoModel;
    //
    string myAutoStyle = "";// #3 样式
    myAutoStyle = txtBoxStyle.Text;
    newStruct.CarStyle = myAutoStyle;
    //
    string myAutoEngine = ""; // #4 引擎
    myAutoEngine = txtBoxEngine.Text;
    newStruct.CarEng = myAutoEngine;
    //
    string myAutoColor = ""; // #5 
    myAutoColor = txtBoxColor.Text;
    newStruct.CarColor = myAutoColor;
    //
    string myAutoOwner = "";// #6 所有者
    myAutoOwner = txtBoxOwner.Text;
    newStruct.CarRealOwner = txtBoxOwner.Text;
    //
    string myAutoFinancier = ""; // #7 资助者
    myAutoFinancier = txtBoxFinancer.Text;
    newStruct.myCarBanker = myAutoFinancier;
    //
    string myAutoCost = "";
    myAutoCost = txtCost.Text; // #8 成本
    newStruct.myCarPrice = myAutoCost;
    //
    // 调用 "writeToFile" 方法执行
    // 实际的“保存到文件功能”
    // “调用”必须包含项目
    // 需要的所有信息。
    //
    // 这是另一个容易
    // 遗漏的地方，请耐心操作！！！
    // 难道不庆幸我们对项目进行了“编号”吗
    //
    writeToFile(myMfg, myAutoModel, myAutoStyle, audioEngine, myAutoColor, myAutoOwner, myAutoFinancier, myAutoCost);
    //
    // 现在信息已保存到硬盘。我们仍然
    // 需要将项目在 listBox1 中列出
    // 并放入 myArray 中。
    //
    // 将列表添加到 listBox1 和 myList...
    //
    string myListing = "";
    myListing = myMfg + " " + myAutoModel + " " + myAutoStyle;
    listBox1.Items.Add(myListing);
    myArrList.Add(newStruct);
    //
    // 通知用户文件中记录的
    // 状态。
    //
    int CountOfRecords = myArrList.Count;
    lblDisplayedRecords.Text = "There are " + Convert.ToString(CountOfRecords) + " records";
} // 结束保存记录 --- 使用 btnSave_click 调用 WriteToFile OK！！！

// "ToFile" 与 btnSave_Click 配合工作。
// 现在记录已经建立，我们需要添加日常记录操作函数。
// 在此之前，从显示记录开始。双击... 进入事件处理代码，如下；

// 开始记录
public void btnDisplay_Click(object sender, EventArgs e)
{
    // 清空 ListBox1 和 myList
    listBox1.Items.Clear();
    myArrList.Clear();
    // 实例化“结构体”
    AutoStruct newStruct = new AutoStruct();
    // 实例化一个 StreamReader 完整文件名
    StreamReader myRdr = new StreamReader(@"C:\Target\Files\AutomobileStruct.txt");
    // 定义字符串变量并读取文件，设置结构体属性
    // 在复杂程序中，使用注释对所有关键项目进行编号，
    // 以帮助定位和纠正错误（调试）
    string myStrFromFileMaker = ""; // #1
    string myStrFromFileMod = ""; // #2
    string myStrFromFileStyle = ""; // #3
    string myStrFromFileEng = ""; // #4
    string myStrFromFileColor = ""; // #5
    string myStrFromFileFinance = ""; // #6
    string myStrFromFileOwner = ""; // #7
    string myStrFromFileCost = ""; // #8
    // 从文件中读取记录。
    while ((myStrFromFileMaker = myRdr.ReadLine()) != null)
        // 现在信息已保存到硬盘。我们仍然
        // 需要将项目在 listBox1 中列出
        // 并放入 myArray 中。
        //
        // 将列表添加到 listBox1 和 myList...
        //
        string myListing = "";
        myListing = myMfg + " " + myAutoModel + " " + myAutoStyle;
        listBox1.Items.Add(myListing);
        myArrList.Add(newStruct);
        //
        // 通知用户文件中记录的
        // 状态。
        //
        int CountOfRecords = myArrList.Count;
        lblDisplayedRecords.Text = "There are " + Convert.ToString(CountOfRecords) + " records";
    } // 结束保存记录 --- 使用 btnSave_click 调用 WriteToFile OK！！！

// "ToFile" 与 btnSave_Click 配合工作。
// 现在记录已经建立，我们需要添加日常记录操作函数。
// 在此之前，从显示记录开始。双击... 进入事件处理代码，如下；

// 开始记录
public void btnDisplay_Click(object sender, EventArgs e)
{
    // 清空 ListBox1 和 myList
    listBox1.Items.Clear();
    myArrList.Clear();
    // 实例化“结构体”
    AutoStruct newStruct = new AutoStruct();
    // 实例化一个 StreamReader 完整文件名
    StreamReader myRdr = new StreamReader(@"C:\Target\Files\AutomobileStruct.txt");
    // 定义字符串变量并读取文件，设置结构体属性
    // 在复杂程序中，使用注释对所有关键项目进行编号，
    // 以帮助定位和纠正错误（调试）
    string myStrFromFileMaker = ""; // #1
    string myStrFromFileMod = ""; // #2
    string myStrFromFileStyle = ""; // #3
    string myStrFromFileEng = ""; // #4
    string myStrFromFileColor = ""; // #5
    string myStrFromFileFinance = ""; // #6
    string myStrFromFileOwner = ""; // #7
    string myStrFromFileCost = ""; // #8
    // 从文件中读取记录。
    while ((myStrFromFileMaker = myRdr.ReadLine()) != null)
    {
        // 现在信息已保存到硬盘。我们仍然
        // 需要将项目在 listBox1 中列出
        // 并放入 myArray 中。
        //
        // 将列表添加到 listBox1 和 myList...
        //
        string myListing = "";
        myListing = myMfg + " " + myAutoModel + " " + myAutoStyle;
        listBox1.Items.Add(myListing);
        myArrList.Add(newStruct);
        //
        // 通知用户文件中记录的
        // 状态。
        //
        int CountOfRecords = myArrList.Count;
        lblDisplayedRecords.Text = "There are " + Convert.ToString(CountOfRecords) + " records";
    }
}
```

8798      //------------------------------------ Start #6

8799      myStrFromFileFinance = myRdr.ReadLine();// #6

8800  if (myStrFromFileFinance == "" ||

8801  myStrFromFileFinance == null)

8802      {

8803          myRdr.Close();

8804          myRdr.Dispose();

8805      MessageBox.Show("Line 242 . . . Partial

8806  record found in file

8840 MessageBox.Show("Line 270 . . . Partial

8841  record found in file, aborted display!", "Partial

8842  record found!");

8843  return;

8844  }

8845 // 如果记录是正确的，我们将对其进行进一步处理

8846  further.

8847 //

8848  if (myStrFromFileCost != "" &&

8849  myStrFromFileCost != null)

8850  {

8851      newStruct.CarsCost(myStrFromFileCost);

8852      intCountOfRecords += 1;

8853      1bDisplayedRecords.Text = "";

8854      Convert.ToString(intCountOfRecords);

8855  }

8856 // --- 8行 --- 完整读取1条记录

8857 // --- 创建列表并添加到 listBox1 ---

8858  string myListing = "";

8859  myStrFromFileMod + " " + myStrFromStyle + " "

8860  + myStrFromFileOwner;

8861  listBox1.Items.Add(myListing);

8862  /* --- 添加到 listBox 和数组中 ------- */

8863  intSelectedIdx = listBox1.SelectedIndex;

8864  myArrayList1.Add(newStruct); /*

8865  /* - 项目已添加到 listBox 和数组中 --- */

8866  } //.. 与 "!=", null" 匹配

8867 //.. - 结束 While 循环 --- 重新开始循环

8868 //.. 结束 btnDisplay_Click -- //

```

这是一段相当长的代码。我同意警告不要直接从文本中复制粘贴。请从示例文件中复制。

到目前，你可能已经想象出完成这项工作的其他方法。太棒了！选择这种方法是为了使用我们目前为止学到的简单、直接的方法。你以后将会学习更多更复杂、更高效的方法来实现相同的功能。

和之前的 Visual Basic 一样，我们将尽早处理从文件中删除不需要的记录。这相当于（清除）listBox1 和 myArrayList 中的旧列表，然后重写文件。但用户可能会自然的操作是点击 listBox1 中的某项，因此接下来我们将处理该事件，然后执行删除。

```csharp

//

public void listBox1_SelectedIndexChanged(object sender, EventArgs e)

// 好！！！ . . . 我在这里写这个注释是为了检查

// 匹配的大括号对，我在编写逻辑块之前

// 先执行这一步，以避免混淆。

XX = listBox1.SelectedIndex;

// MessageBox.Show(myStrSender);

// 为了填充文本框，我们需要实例化结构体

// 以获取我们想要为用户选择的特定项目显示的属性。

int selectedIdx = listBox1.SelectedIndex;

if (selectedIdx == -1) {selectedIdx = 0};

int intArrayCount = 0;

intArrayCount = myArrayList.Count; //

/**-

Object myObj; // 不能直接从

// ArrayList 创建结构体。

// --- 这是此事件处理块中的第一个结构体。

```

```csharp

// 在我们需要定义它之前，

// 不知道结构体是什么，或者结构体

// 是否已创建或使用。

// 所以，我们先 new一个新 对象。

myObj = new Object();

//

// 第 2 步

// "Object 是基类" . . 无法直接将

// Object 转换为结构体，需要一个中间步骤。

AutoStruct newStruct = new AutoStruct();

myObj = myArrayList[intSelectedIdx];

newStruct = (AutoStruct)Convert.ChangeType(myObj, typeof(AutoStruct));

//

// 从创建的结构体中提取属性

string myNewCarMaker = newStruct.CarBuilder; // #1

string myNewCarMod = newStruct.CarModel; // #2

string myNewCarStyle = newStruct.BarStyle; // #3

string myNewCarEng = newStruct.myEng; // #4

string myNewCarColor = newStruct.CarsColor; // #5

string myNewCarFinancer = newStruct.Lien; // #6

string myNewCarOwner = newStruct.myOwner; // #7

string myNewCarCost = newStruct.CarCost; // #8

// 将字符串放入文本框中

txtBoxMfg.Text = myNewCarMaker; // #1

txtBoxModel.Text = myNewCarMod; // #2

txtBoxStyle.Text = myNewCarStyle; // #3

txtBoxEngine.Text = myNewCarEng; // #4

txtBoxColor.Text = myNewCarColor; // #5

txtBoxFinancer.Text = myNewCarFinancer; // #6

txtBoxOwner.Text = myNewCarOwner; // #7

txtBoxCost.Text = myNewCarCost; // #8
```
