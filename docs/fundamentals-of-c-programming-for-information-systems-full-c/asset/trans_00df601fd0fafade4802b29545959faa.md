

## 第12章

11.2 隐藏表单会将表单及其属性和设置保留在内存中。你不会在运行时丢失控件中输入/显示的数据。
关闭表单会将表单从内存中移除。因此，你会丢失所有当前设置和数据。

11.3 Show 方法打开表单并让 C# 继续处理该语句之后的代码。然而，使用 ShowDialog 方法时，C# 会打开表单并停止处理该语句之后的代码，直到对话框窗口关闭。

11.4 在类中创建一个 Public 方法并从不同的表单调用它。

11.5 静态方法与包含该方法的类的特定实例（对象）无关。它仅与类相关联。因此，使用类名调用它。
要调用非静态方法，你必须创建类的对象并使用对象名代替类名。

11.6 上下文菜单与控件相关联，通过右键单击该控件显示。

11.7 选项 3：从上下文菜单中选择一项

12.1 数据表是保存在内存中的临时表。每个数据表可能包含来自一个或多个通常存储在磁盘上的数据库表的数据。

12.2 表适配器将数据表连接到数据库，并从数据库检索数据并将数据保存到数据库。

12.3 绑定源将表单上的用户界面控件链接到数据表。

12.4 表适配器的 Fill 方法将数据从数据库表复制到数据表。

12.5 表适配器的 Update 方法将数据从数据表保存到数据库表

12.6 数据绑定控件是链接到数据源的用户界面控件

12.7 数据绑定控件中的数据链接到绑定源，而绑定源链接到数据表。

12.8 将所有 DataBindings 设置为 None。
将 DataSource 设置为 CustomerBindingSource
将 DisplayMember 设置为 CustomerId

12.9 用户将只能看到 CountryId 为 22 的员工记录。
这不会影响数据表中的记录。数据表仍然会有来自 Employee 表的所有记录。

12.10 Employee 数据表将只有来自 DeptNo 11 的员工记录。

12.11 连接字符串，SQL

12.12 使用代码在运行时创建数据访问对象使代码更灵活、高效且可重用。

12.13 键入的数据表包含与数据库表中的字段类型相同的字段，通常在设计时创建。未键入的数据表不包含其字段的信息。它们在运行时创建。

12.14 数据绑定控件通过绑定源绑定到数据表中的特定字段。因此，表单上的数据与数据表中的字段紧密关联。当前行会自动显示在控件中。非绑定控件未直接绑定到任何字段。

12.15 表适配器的 Update 方法。

12.16 将绑定源的 DataSource 属性设置为数据表。

12.17 使用其 Filter 属性在行之间移动、获取行的位置/计数并选择行。

12.18 将当前行存储在 DataRowView 对象中，并将数据从 DataRowView 复制到表单上的控件。

12.19 两种代码都允许用户查看 IS 学生记录。代码段 #1 将只加载 IS 学生记录到数据表。代码段 #2 将加载所有学生记录到数据表，但只允许用户查看 IS 学生记录。

12.20 EndEdit 方法将绑定源行中的更改应用到其链接的数据表。

12.21 False

12.22 数据适配器的 Update 方法将数据表中的更改保存到数据库表。

12.23 DataReader 提供了一种高效的方式来顺序访问由 SQL 语句从数据库检索的数据

12.24 False

12.25 False

12.26 ExecuteScalar

12.27 ExecuteReader

12.28 ExecuteNonQuery

12.29 使 DataReader 前进到下一行

Flowchart, 4
for Loop, 135, 216, 223
for vs. foreach, 219
foreach Loop, 142, 219, 287
Form
  Accessing from another form, 331
  Creating multiple instances, 333
  FormClosing event, 255
  Hiding vs. Closing, 333
  Load event, 254
  Login form, 342
  Sharing methods between forms, 335
  Show vs. ShowDialog, 334
Graphical User Interface, 3
High-level languages, 6
if else if Statement, 96
if else Statement, 87
Implicit cast, 64
Infinite Loop, 131
Initializing a variable, 31
Input, 3
int type, 27, 56
Integer, 26
Integer literals, 61
Integrated Development Environment (IDE), 6
Intermediate language, 6
Interpreter, 6
KeyValuePair collection, 294
Label, 16
  Autosize property, 16
Lifetime of a variable, 30
List<T> Collection, 281
ListBox, 198
  Items collection, 47
ListView, 302, 307, 316, 321
ListViewItem, 303, 317
Literals, 59
Local variables, 49, 62
Locals Window, 62
Logic error, 4
Logical operators, 93
Low-level, 5
Machine language, 6
Machine Language, 5
Menus, 345
  Context Menu, 348
MessageBox, 52
Method, 22, 144, 264
  access identifier, 145
  cohesive methods, 155
  passing values to methods, 148
  public, 145
  static methods, 338
  void method, 146
Methods that Return a Value, 168
Microsoft Intermediate Language (IL) Assembly, 6
Multiplication with large integers, 66
Namespace, 21
Nested if Statements, 98
Non-integer (real) types, 28
Output, 2
parameter
  out parameter, 159
Parameter, 149, 338
parameter query, 381
Parse, 35
PositionChanged event, 390
Precedence of Operators, 37
Prefixes for controls, 16
Pre-test loops, 132
Process, 3
Project, 8
Properties window, 10
Pseudo code, 4
RadioButtons, 182
Real number, 26
Reference types, 68
Relational operator, 87
Replace (string, string) method, 71
Runtime error, 4
SaveFileDialog control, 260
Scope of Variables, 49
Scroll Bars, 176
SelectCommand, 398
SelectedIndexChanged event, 195
Sequential Access Files, 230
Solution, 8
Solution Explorer, 10
SortedDictionary, 279
SortedList, 279
SQL Server, 432
SqlCommand, 413
SqlCommandBuilder, 403
Startup form, 15
StreamReader class, 231
StreamWriter class, 253
string Type, 28
  Concatenating strings, 71

String operations, 69
String.Format method, 47
Substring method, 70
ToLower method, 70
Trim method, 70
String vs. Character, 72
Structure chart, 148
switch Statement, 102
Syntax error, 4
Tab Pages, 312, 326
Table adapter, 353, 380, 381
TextBox, 16
ToolStrip, 350
ToolTip, 13
Top-down design, 144, 161
Trim() method, 70
Try-catch, 51
TryParse method, 106
typed dataset, 384
unbound control, 384
untyped dataset, 384
Using directive, 21
Validating Input, 184
validating event, 111
Value types, 68
Value Types vs. Reference Types, 209
while Loop, 121
Widening conversion, 64

