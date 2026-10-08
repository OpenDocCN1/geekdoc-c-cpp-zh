
```vb
// 记录。这需要几行代码。
// 继续操作是清除文本框并
// 从 ArrayList 中移除
// 项目，另一方面，
如果用户
// 点击“取消”，只需要一条命令。
// 退出子程序（Sub），你稍后就会看到这个。
//
// 从 ArrayList 和 ListBox 中移除项目。
ListBox1.Items.RemoveAt(intSelectedIndex)
myArray.RemoveAt(intSelectedIndex)
// 清空文本框。
//
tboxMfg.Text = "" // #1
tboxModel.Text = "" // #2
tboxStyle.Text = "" // #3
tboxEngine.Text = "" // #4
tboxColor.Text = "" // #5
tboxFinancer.Text = "" // #6
tboxOwner.Text = "" // #7
tboxCost.Text = "" // #8
// 现在，重新创建一个仅包含
// “保留”
// 项目的文件。
ReCreateFile() // 这调用了一个外部
// 子程序来
// 写入文件。
// Else // 意味着用户没有点击
"OK”。
Exit Sub // 如果 . . . 用户点击了
"Cancel"，则中止
// 删除操作！！！！
End If // End Sub // btnDeleteSelected Click
//
// 就这样！！要么我们删除了记录，要么取消了
尝试。接下来，我将向你展示 Re-Create()
// 子程序。
```

简易编程 C# 和 Visual Basic...

# 7793 PS... 所有的注释和解释

7794 包含在此处的实际上并不在实际代码

7795 块中。此子程序（Sub）是从

7796 btnDeleteSelectedRecord_Click 事件中调用的。它对用户

7797 可见，甚至不可知。

7798 //

7799 Public Sub RecreateFile()

7800 // 这个子程序是从

7801 // btnDeleteSelectedRecord_Click 事件调用的

7802 // 在此时，目标项目已经

7803 // 从 ArrayList 和 listBox

7804 // 中移除

7805 // 剩下的都是我们想要

7805 // 保留的记录 . . .

7807 //

7808 Dim myFile As Boolean = False

7809 // Boolean 是一个“逻辑变量”，True 表示

7810 条件

7811 // 测试是否存在。

7812 //

7813 // 检查文件，存在则删除旧文件

7814 myFile =

7815 My.Computer.FileSystem.Exists("C:\App Target

7816 Files\AutomobileStructSpecs.txt") // 如果文件存在，评估

7817 // 为 True。

7818 ("C:\App Target

7819 Files\AutomobileStructSpecs.txt")

7820 //

7821 // 这是比较两个

7822 // 字符串的好方法 . . .

7823 // 将一个放在另一个的注释中

7824 // 并寻找

7825 // 任何差异

7826 //

7827 // 检查文件，存在则删除旧文件

7828 If (myFile = True) Then

7829 My.Computer.FileSystem.DeleteFile("C:\App

7830 Target Files\AutomobileStructSpecs.txt")

7831 End If

7822 // 创建我们需要重写的信息
224 John Queen
