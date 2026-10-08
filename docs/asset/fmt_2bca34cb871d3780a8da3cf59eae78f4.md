
14658 `myStrFromFileColor` != null)

14659 {

14660 `newStruct.CarsEngine`

14661 (`myStrFromFileColor`);

14662 }

```
```csharp
14666 // #### --- Start #6 // Reversed
14667 with Banker
14668 `myStrFromFileFinance` =
14669 `myRdr.ReadLine()`; // #6
14670 if (`myStrFromFileFinance` == "") ||
14671 `myStrFromFileFinance` == null
14672 {
14673 `myRdr.Close()`;
14674 `myRdr.Dispose()`;
14675 `MessageBox.Show`("Line 242 . . .
14676 文件中发现部分记录，中止显示！",
14677 "Partial record found!");
14678 return;
14679 if (`myStrFromFileFinance`!= " " &&
14680 `myStrFromFileFinance`!= null
14681 {
14682 `newStruct.myCarsFinancer`
14683 (`myStrFromFileFinance`);
14684 }
14685 // ---------------------- Start #7
14686 string `myStrFromFileCarOwner` =
14687 `myRdr.ReadLine()`; // #7
14688 `newStruct.CarsRealOwner`
14689 (`myStrFromFileCarOwner`)
14690 if (`myStrFromFileCarOwner` == "")
14691 `myStrFromFileCarOwner` == null
14692 {
14693 `myRdr.Close()`;
14694 `myRdr.Dispose()`;
14695 `MessageBox.Show`("Line 257 . . .
14696 文件中发现部分记录，中止显示！",
14697 "Partial record found!");
14698 return;
14699 if (`myStrFromFileCarOwner`!= " " &&
14700 `myStrFromFileCarOwner`!= null
14701 {
14702 `newStruct.CarsRealOwner`
14703 (`myStrFromFileCarOwner`);
14704 }
```

## 简单地编写 C# 和 Visual Basic ...

```csharp
14707 `myStrFromFileCost` =
14708 `myRdr.ReadLine()`; // #8
14709 if (`myStrFromFileCost` == ""
14710 `myStrFromFileCost` == null
14711 {
14712 `myRdr.Close()`;
14713 `myRdr.Dispose()`;
14714 `MessageBox.Show`("Line 270 . . .
14715 文件中发现部分记录，中止显示！",
14716 "Partial record found!");
14717 return;
}
14718 {
14719 if (`myStrFromFileCost` != "" &&
14720 `myStrFromFileCost` != null)
11721 {
14722 `newStruct.CarsCost`
14723 (`myStrFromFileCost`);
14724 `intCountOfRecords` += 1;
14725 `lblDisplayedRecords.Text` = "";
14726 `lblDisplayedRecords.Text` =
14727 `Convert.ToString`(`intCountOfRecords`);
14728 }
14729 // -- 8 记录完成
14731 // 创建要添加的列表
14732 string `myList` = "";
14733 `myList` = `myStrFromFileMaker` + " " + `myStrFromFileMod` + " " + `myStrFromFileStyle` + " " + `myStrFromFileOwner`;
14734 `listBox1.Items.Add`(`myList`);
14735 // 添加到数组
14736 `listBox1.Add`(`newStruct`);
```

414
John Queen

```csharp
private void `btnDelete_Click`(object sender, EventArgs e)
{
    // 获取我们需要标识的
    // 要从删除删除的行
    // 如果没有选择项目，则告知用户
    int `selectedIdx` = `listBox1.SelectedIndex`;
    int `selectedIdx` = `selectedIdx`; // ---- 作为整数传递给 CreateFile
    if (`selectedIdx` == -1)
    {
        `MessageBox.Show`("未选择要删除的项目，请选择一个项目进行删除...", "未选择项目");
    }
    // ---- 现在知道从 listBox1 中删除哪个项目了
    // 如果选择了项目，继续获取所需的属性
    Object `myObj`;
    `myObj` = new Object();
    AutoStruct `newStruct` = new AutoStruct();
    `myObj` = `myList`[`selectedIdx`];
    // ---- 现在知道是哪个项目
    // "结构体/对象" -- 转换为 "newStruct"
    `newStruct` = (AutoStruct)`Convert.ChangeType`(`myObj`, typeof(AutoStruct));
    // 在删除前确认决定
    string `myStrMfg` = `listBox1.SelectedItem.ToString`();
    if (`MessageBox.Show`(`myStrMfg` + " 位于索引 " + `Convert.ToString`(`selectedIdx`) + ". 点击确定移除此项，取消则保留此项。", "确认") == DialogResult.OK)
    {
        // 删除逻辑将在此处
    }
}
```

仅仅是编程 C# 和 Visual Basic...

```csharp
14791              {
14792              // 如果 . . . 用户点击 "确定" 删除记录
14793  record.             // 清空 textBox 项
14794  ArrayList
14795              // --- 使用 "textBox.text" 属性!!!!
14796              //
14798              string `txtBoxMfgInfo`= `txtBoxMfgInfo.Text`; // #1
14799              string `txtBoxModelInfo` = `txtBoxModel.Text`; // #2
14800              string `txtBoxStyleInfo` = `txtBoxModel.Text`; // #3
14801              string `txtBoxEngineInfo` = `txtBoxEngine.Text`; // #4
14802              string `txtBoxColorInfo` = `txtBoxColor.Text`; // #5
14803              string `txtBoxFinancerInfo` = `txtBoxFinancer.Text`; // #6
14804              string `txtBoxOwnerInfo` = `txtBoxOwner.Text`; // #7
14805              string `txtBoxCostInfo` = `txtBoxCost.Text`; // #8
14806              // 清空 textBox --- 清空 textBox --- 清空 textBox
14807              `txtBoxMfg.Text` = "";// #1--- 清空 textBox
14808              `txtBoxModel.Text` = ""; // #2--- 清空 textBox
14809              `txtBoxStyle.Text` = ""; // #3--- 清空 textBox
14810              `txtBoxEngine.Text` = ""; // #4--- 清空 textBox
14811              `txtColor.Text` = ""; // #5--- 清空 textBox
14812              `txtBoxFinancer.Text` = "";// #6--- 清空 textBox
14813              `txtBoxOwner.Text` = ""; // #7--- 清空 textBox
14814              `txtBoxCost.Text` = ""; // #8--- 清空 textBox
14815              //
```

```csharp
14833               // --- 传递给 ReCreateFile(带字符串的) /
14834                   // ----- textBox 已清空但
14835                   // 对象未从 myArray1 或 listBox1 中移除
14836                   尽管如此!!
14837                   /
14838                   // ---- 字符串传递到 ReCreate 文件函数
14839                   // --- | #1 | #2 | #3 | #4 | #5 | #6 | #7 | #8
14840                   // 字符串在这里-v v v v v v v
14841                   // 整数在这里 |
14842                   // v
14843                   `list1.Items.RemoveAt`(`intSelectedIdx`);
14844                   `myArraylist.RemoveAt`(`intSelectedIdx`);
14845                   `ReCreateFile`();
14846                   `list1.SelectedIndex` = 0;
14847                   } // 点击“确定”消息按钮结束
14848 } // -- btnDeleteSelectedRecord 结束
14849 /
14850                   // 与 btnDelete 文件配合从文件中删除记录 /
14851                   public void `ReCreateFile`()
14852                   // ----- OK /
14853                   int `intmySelectedIdx` = 0;
14854                   /
14855                   // myArray 仅包含我们保留的记录对象列表。“但是”这并没有
14856                   // 实际上“删除”那些属性
14857                   已删除的“对象”已保存在持久性硬盘文件中。
14858                   // 我们通过丢弃旧文件并创建一个“新”文件，且“不包含”
14859                   // 来自 listBox1 和 myArray 的列表和对象!!!!!!!!!!!!
14860                   /
14861                   int `intArrayCount` = `myArray.Count`-1;
```

```csharp
14875
//
// 14876
// 如果“存在”14877AutomobileStructSpecs.txt 文件，则“删除”旧的
//
// 14879	Boolean `myTest1` = `File.Exists`("C:\\App\\Target Files\\AutomobileStructSpecs.txt");
14880
if(`myTest1`==true)
14881
{
14882	`File.Delete`("C:\\App Target Files\\AutomobileStructSpecs.txt");
14883	`MessageBox.Show`("旧文件已删除 ");
14884}
//
14886	int StartObj = 0; // 从索引为 "0" 的对象开始
14887	//----- 继续到 (myArray 计数-1)，记得 . .
14888	//----- "Count" 是对象的实际数量，
14889	//-----“但是”编号从零开始
//
// 检查文件名称!!!!
	StreamWriter `writer` = new StreamWriter("C:\\App Target Files\\AutomobileStructSpecs.txt",true);
14892	// 记住 "true" 表示如果存在则“追加”，如果“不存在”则创建它
14893	// 因为零计数，从对象计数零开始写入新文件或追加文件。
14894	int `ObjectSavedCount` = 0;
14895	`MessageBox.Show`("我已准备好保存 . . + Convert.ToString(intArrayCount) + " 数组计数到");
14896	// 作为 While 循环的起点
int `XYZ` = 0;
```
