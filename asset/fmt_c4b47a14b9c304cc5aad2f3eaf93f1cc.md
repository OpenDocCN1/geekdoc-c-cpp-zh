
```csharp
-------------------- //
// ---------- 此类和命名空间的库的开始 --------------------
using System;
using System.Collections;
using System.IO;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Forms;
// ---- 命名空间的开始 ----
//
namespace VS_CS_Struct_with_File
{ // 用于此方法的大括号
    public partial class StructWithFileIO:Form // 开始部分类
    { // 用于此方法的大括号
        // 如果在全局变量之前声明
        public int myObjIdx;
        public int intSelected;
        public int intCountOfRecords;
        public int StartObject;
        public int intSelectedIdx=999; // 用于 btnDelete_Click
        public int YY = 999; // 用于 btnDelete_Click，传递给 CreateFile(YY)
        public int XX = 999; // 用于 btnDelete_Click，传递给 CreateFile(XX)
        public int XYZEdit = 999; // 用于 btnDelete_Click
        public int intEditIdx;
        public ArrayList mylist = new ArrayList(40);

        // 初始化表单
        public StructWithFileIO() // 初始化表单
        {
            InitializeComponent();
        }

        // 定义自动结构体
        public struct AutoStruct
        {
            // #################################
            // 声明字段 #1) CarMaker
            public string CarMfg;
            public string CarBuilder;
            // 定义一个构造函数
            public string CarMaker(string myCarBuilder)
            {
                CarBuilder = myCarBuilder;
                return CarBuilder;
            } // 结束 #1) CarMaker
            // #################################
            public string CarMod; // 开始 #2) CarMod
            public string CarModel;
            // 定义构造函数
            public string CarMods(string CarMod)
            {
                CarModel = CarMod;
                return CarModel;
            } // 结束 #2) CarMod
            // #################################
            public string CarsStyle; // 开始 #3) CarStyle
            public string myCarStyle;
            // 定义构造函数
            public string CarsStyles(string myStylePut)
            {
                myCarStyle = myStylePut;
                return myCarStyle;
            } // 结束 Style #3 CarStyle
            // #################################
            public string CarsEngine; // 开始 #4) CarEngine
            public string myCarEng;
            // 定义构造函数
            public string CarsEngine(string myCarHP)
            {
                myCarEng = myCarHP;
                return myCarEng;
            } // 结束 Engine #4 CarEngine
            // #################################
            public string CarsColor; // 开始 #5) CarColor
            public string myCarsColor;
            // 定义构造函数
            //
            public string CarsColors(string Paint)
            {
                myCarsColor = Paint;
                return myCarsColor;
            } // 结束 Engine #5) CarColor
            // #################################
            public string CarsFinancer; // 开始 #6) CarFinancer
            public string CarsBanker;
            public string CarsLien;
            // 定义构造函数
            public string CarsFinancer(string Finance)
            {
                CarsLien = Finance;
                CarsFinancer = Finance;
                CarsBanker = Finance;
                return CarsLien;
            } // 结束 Financer #6) CarFinancer
            // #################################
        } // 结束 --------------------Struct
        // // 结束 AutoStruct 结构定义
        大括号 -- OK 到这里!!
        private void btnExit_Click(object sender, EventArgs e)
        {
            Application.Exit();
        } // -----大括号 ----- OK 到这里!!
        // ################# 开始 显示记录
        records
    }
}
```

408

John Queen

```csharp
public void btnDisplay_Click(object sender, EventArgs e)
{
    list1.Items.Clear();
    myArray1.Clear();
    AutoStruct newStruct = new AutoStruct();
    StreamReader myRdr;
    myRdr = new StreamReader("C:\\App Target Files\\AutomobileStructSpecs.txt");
    // 定义字符串变量并读取文件并设置字符串属性
    string myStrFromFileMaker = ". "; // # 1
    string myStrFromFileMod = ". "; // # 2
    string myStrFromFileStyle = ". "; // # 3
    string myStrFromFileEng = ". "; // # 4
    string myStrFromFileColor = ". "; // # 5
    string myStrFromFileFinance = ". ";
    string myStrFromFileOwner = ". "; // # 7
    string myStrFromFileCost = ". "; // # 8
    string myStrFromFile = ". ..";
    // 读取文件并计数读取的记录数。
    while (myStrFromFile != null && myStrFromFile != null) // 开始读取文件
    { own        /* 清除字符串，因为开始读取新的 8 项记录 */
        --------------------
        myStrFromFileMaker = ". "; // # 1
        myStrFromFileMod = ". "; // # 2
        myStrFromFileStyle = ". "; // # 3
        myStrFromFileEng = ". "; // # 4
        myStrFromFileColor = ". "; // # 5
        myStrFromFileFinance = ". "; // # 6
        myStrFromFileOwner = ". "; // # 7
        myStrFromFileCost = ". "; // # 8
    */
```

## 简单地编写 C# 和 Visual Basic...

```csharp
14541 int intCountOfRecords = 0; // 保留
14542 读取的记录数。
14543 //
14544 // 读取文件中 "Every string" 里的
14545 第一条或下一条记录的第一个字符串 --
14546 --读取的字符串将
14547 // 进行测试，以防部分
14548 记录被找到。将字符串赋值，例如
14549 "myCarBuilder" 等赋值给
14550 // new newStruct()."CarMaker" 属性，
14551 struct。我知道制造商是第一个，因为
14552 这是
14553 // 我们向文件中写入信息的
14554 顺序。因此，我们将每个字符串读取赋值给
14555 正确的
14556 // Struct 属性
14557 //
14558 myStrFromFileMaker =
14559 myRdr.ReadLine(); // #1
14560 //MessageBox.Show("#1-Line 160 Go
14561 1 Line Mfg " + myStrFromFileMaker,btnDisplay_
14562 Click");
14563 if (myStrFromFileMaker == "" ||
14564 myStrFromFileMaker==null)
14565 {
14566 intCountOfRecords =
14567 myArylst.Count;
14568 l1blDisplayedRecords.Text = "";
14569 l1blDisplayedRecords.Text =
14570 "There are "+Convert.ToString(intCountOfRecords)+"
14571 records;
14572 myRdr.Close();
14573 myRdr.Dispose();
14574 return;
}
14575 {
14576 if (myStrFromFileMaker!=null &&
14577 myStrFromFileMaker!=null) //1
14578 {
14579
14580 newStruct.CarMaker(myStrFromFileMaker);
}
```

## 410 John Queen

```csharp
14582 // 如果第一个字符串是有效的，
14583 该记录还有另外 7 个
14584 // 除非是一个损坏的局部
14585 记录。
14586 {
14587 // ------------------------------------Start #2
14588 myStrFromFileMod =
14589 myRdr.ReadLine(); // #2)
14590 if (myStrFromFileMod == "" ||
14591 myStrFromFileMod == null
14592 {
14593 myRdr.Close();
14594 myRdr.Dispose();
14595 MessageBox.Show(" Line 185 . . .
14596 文件中发现部分记录，中止显示！",
14597 "Partial record found!");
14598 return;
}
14599 if (myStrFromFileMod!= null &&
14600 myStrFromFileMod!= ""
14601 {
14602 newStruct.CarMods
14603 (myStrFromFileMod);
14604 }
14605 // -------------------------------- Start #3
14606 myStrFromStyle =
14607 myRdr.ReadLine(); // #3
14608 if (myStrFromStyle == "" ||
14609 myStrFromStyle == null
14610 {
14611 myRdr.Close();
14612 myRdr.Dispose();
14613 MessageBox.Show("Line 185 . . .
14614 文件中发现部分记录，中止显示！",
14615 "Partial record found!");
14616 return;
14617 if (myStrFromStyle != "" &&
14618 myStrFromStyle!= null)
14619 {
14620 newStruct.CarStyles
14621 (myStrFromStyle);
## 简单地编写 C# 和 Visual Basic...

```csharp

14624 //MessageBox.Show("Line

14625 206 . . 文件中发现部分记录，中止

14626 display", "Partial record found!");

14627 }

14628 // ------------------------ Start #4

14629 myStrFromFileEng =

14630 myRdr.ReadLine(); // #4

14631 if (myStrFromFileEng == "" ||

14632 myStrFromFileEng == null

14633 {

14634 myRdr.Close();

14635 myRdr.Dispose();

14636 MessageBox.Show("Line 214 . . .

14637 文件中发现部分记录，中止显示",

14638 "Partial record found!");

14639 return;

14640 if (myStrFromFileEng != "" &&

14641 myStrFromFileEng!= null)

14642 {

14643 newStruct.CarsEngine

14644 (myStrFromFileEng);

14645 // ------------------------ Start #5

14646 myStrFromFileColor =

14647 myRdr.ReadLine(); // #5

14648 if (myStrFromFileColor == ""

14649 myStrFromFileColor==null

14650 {

14651 myRdr.Close();

14652 myRdr.Dispose();

14653 MessageBox.Show("Line 228 . . .

14654 文件中发现部分记录，中止显示！",

14655 "Partial record found!");

14656 return;

14657 if (myStrFromFileColor != "" &&
