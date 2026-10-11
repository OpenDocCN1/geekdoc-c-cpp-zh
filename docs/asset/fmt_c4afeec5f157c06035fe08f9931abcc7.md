
| A7758 | Dahlia | Associate Professor | Notre Dame | dbahlia@college.edu |

| A1021 | Henry | Associate Professor | Ohio State | jhenry@college.edu |

| A7896 | Johnston | Distinguished Professor | Harvard | sjohnston@college.edu |

| B911 | King | Professor | East Florida University | jking@college.edu |

| B8650 | Johnson | Associate Professor | Germany | johnson@college.edu |

| B7888 | Bai | Associate Professor | | ybai@college.edu |

![](img/d59a47501d0a20fc0460a49c469c6fb7_61.png)

FIGURE 2.30 faculty 表。

FIGURE 2.31 faculty 表。

# 使用 C# 进行 SQL 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_62_0.png)

图 2.31 完成的表。

你完成的 Faculty 表应该与图 2.31 所示的表匹配。现在转到“文件”菜单并选择“保存所有”，以保存此完成的 Faculty 数据表。你完成的 Faculty 数据表将以名为 `dbo.Faculty` 的表形式显示，并已添加到“对象管理器”窗口中“表”下的新数据库 `CSE_DEPT` 中。此时，保持图像列为 NULL，我们稍后将使用 Visual Studio.NET 和 DevExpress 控件添加实际的教师图像。

## 2.9.3 创建表

以类似的方法，创建其余三个表：Course、Student 和 StudentCourse。选择 `course_id`、`student_id` 和 `s_course_id` 为这些表的主键。这些表的详细数据请参考图 2.32–2.34。数据类型选择，请遵循以下说明：

Course 表的数据类型选择：

- `course_id` - varchar(50) (主键)
- `credit` - int
- `enrollment` - int
- `faculty_id` - varchar(50)
- 其他所有列 – 使用 varchar(50) 或 text

Student 表的数据类型选择：

- `student_id` - varchar(50) (主键)
- `student_name` - varchar(50)
- `gpa` - float
- `credits` - int
- `simage` - image
- 其他所有列 – 使用 varchar(50) 或 text

## 数据库简介

| 课程 ID | 课程名称 | 学分 | 教室 | 时间表 | 选人数 | 教师 |
|---|---|---|---|---|---|---|
| CSE-131A | 社会中的计算机 | 3 | MCI-109 | 周一三周五: 9:00-9:55 AM | 28 | A52990 |
| CSE-131B | 社会中的计算机 | 3 | MCI-114 | 周一三周五: 9:00-9:55 AM | 20 | B66750 |
| CSE-131C | 社会中的计算机 | 3 | MCI-109 | 周二周四: 11:00-12:25 PM | 25 | A52990 |
| CSE-131D | 社会中的计算机 | 3 | MCI-109 | 周一三周五: 9:00-9:55 AM | 30 | B66590 |
| CSE-131E | 社会中的计算机 | 3 | MCI-301 | 周一三周五: 1:00-1:55 PM | 25 | B66750 |
| CSE-131I | 社会中的计算机 | 3 | MCI-308 | 周二周四: 1:00-2:25 PM | 32 | A52990 |
| CSE-132A | 编程入门 | 3 | MCI-303 | 周一三周五: 9:00-9:55 AM | 21 | J33486 |
| CSE-132B | 编程入门 | 3 | MCI-302 | 周二周四: 11:00-12:25 PM | 21 | B77880 |
| CSE-230 | 算法与结构 | 3 | MCI-305 | 周二周四: 11:00-12:25 PM | 28 | B66750 |
| CSE-232A | 数据结构 | 3 | MCI-301 | 周一三周五: 1:00-1:55 PM | 20 | A77587 |
| CSE-232B | 编程 II | 3 | MCI-303 | 周二周四: 11:00-12:25 PM | 17 | A77587 |
| CSE-233A | 算法入门 | 3 | MCI-302 | 周一三周五: 9:00-9:55 AM | 19 | K69918 |
| CSE-233B | 算法入门 | 3 | MCI-301 | 周二周四: 11:00-12:25 AM | 19 | K69918 |
| CSE-234A | 数据结构 | 3 | MCI-302 | 周一三周五: 9:00-9:55 AM | 25 | B77880 |
| CSE-234B | 数据结构 | 3 | MCI-114 | 周二周四: 11:00-12:25 PM | 15 | J33486 |
| CSE-242 | 编程 II | 3 | MCI-303 | 周二周四: 1:00-2:25 PM | 18 | A52990 |
| CSE-320 | 面对象编程 | 3 | MCI-301 | 周二周四: 1:00-2:25 PM | 22 | B66750 |
| CSE-331 | 应用编程 | 3 | MCI-109 | 周二周四: 11:00-12:25 PM | 28 | R99118 |
| CSE-333A | 计算机体系 | 3 | MCI-301 | 周一三周五: 10:00-10:55 AM | 22 | A77587 |
| CSE-333B | 体系 | 3 | MCI-302 | 周二周四: 11:00-12:25 PM | 15 | A77587 |
| CSE-335 | 网页编程 | 3 | MCI-303 | 周一三周五: 1:00-1:55 PM | 25 | B66750 |
| CSE-432 | 离散算法 | 3 | MCI-206 | 周四: 9:30-11:00 AM | 20 | B66590 |
| CSE-439 | 数据库系统 | 3 | MCI-206 | 周一三周五: 1:00-1:55 PM | 18 | B66590 |
| CSE-138A | 操作系统 | 3 | MCI-301 | 周二周四: 1:00-2:25 PM | 15 | A52990 |
| CSE-138B | 操作系统 | 3 | MCI-109 | 周一三周五: 9:00-9:55 AM | 35 | J33486 |
| CSE-330 | 数字数逻辑 | 3 | MCI-305 | 周一三周五: 9:00-9:55 AM | 26 | K69918 |
| CSE-332 | 半导体基础 | 3 | MCI-305 | 周二周四: 1:00-2:25 PM | 24 | K69984 |
| CSE-334 | 电测设计 | 3 | MCI-212 | 周二周四: 11:00-12:25 PM | 25 | H99118 |
| CSE-430 | 生物信息学 | 3 | MCI-206 | 周四: 9:30-11:00 AM | 16 | B66590 |
| CSE-432 | 模拟电路设计 | 3 | MCI-309 | 周一三周五: 2:00-2:55 PM | 18 | K69918 |
| CSE-433 | 数字信号处理 | 3 | MCI-206 | 周二周四: 2:00-2:25 PM | 28 | H99118 |
| CSE-434 | 进阶电子学 | 3 | MCI-213 | 周一三周五: 1:00-1:55 PM | 26 | B77880 |
| CSE-436 | 自动控制与设计 | 3 | MCI-305 | 周一三周五: 10:00-10:55 AM | 29 | J33486 |
| CSE-437 | 操作系统 | 3 | MCI-303 | 周二周四: 1:00-2:25 PM | 17 | A77587 |
| CSE-438 | 进阶逻辑与处理器 | 3 | MCI-213 | 周一三周五: 11:00-11:55 AM | 35 | B77880 |
| CSE-439 | CSE 特色主题 | 3 | MCI-206 | 周一三周五: 10:00-10:55 AM | 22 | J33486 |

| 学生 ID | 姓名 | GPA | 学分 | 年级 | 邮箱 |
|---|---|---|---|---|---|
| A78835 | Andrew Woods | 3.26 | 108 | 大四 | aerosols@college.edu |
| A97850 | Ashley Jade | 3.57 | 116 | 大三 | ajade@college.edu |
| B92996 | Blue Valley | 3.52 | 102 | 大四 | bvalley@college.edu |
| H10210 | Holes Smart | 3.87 | 78 | 大二 | smith@college.edu |
| T77896 | Tom Erica | 3.95 | 127 | 大四 | terica@college.edu |

## 36 SQL Server 数据库编程

| ID | 学生 ID | 课程 ID | 学分 | 专业 |
|---|---|---|---|---|
| 1000 | H10210 | CSC-131D | 3 | CE |
| 1001 | B92996 | CSE-132A | 3 | CS/IS |
| 1002 | T77896 | CSC-335 | 3 | CS/IS |
| 1003 | A78835 | CSC-331 | 3 | CE |
| 1004 | H10210 | CSE-234B | 3 | CE |
| 1005 | T77896 | CSE-234A | 3 | CS/IS |
| 1006 | B92996 | CSE-233A | 3 | CS/IS |
| 1007 | A78835 | CSE-132A | 3 | CE |
| 1008 | A78835 | CSE-432 | 3 | CE |
| 1009 | A78835 | CSE-439 | 3 | CE |
| 1010 | T77896 | CSC-439 | 3 | CS/IS |
| 1011 | H10210 | CSE-132A | 3 | CE |
| 1012 | H10210 | CSC-331 | 2 | CE |
| 1013 | A78835 | CSC-335 | 3 | CE |
| 1014 | A78835 | CSE-438 | 3 | CE |
| 1015 | T77896 | CSE-432 | 3 | CS/IS |
| 1016 | A97850 | CSE-132B | 3 | ISE |
| 1017 | A97850 | CSC-234A | 3 | ISE |
| 1018 | A97850 | CSC-331 | 3 | ISE |
| 1019 | A97850 | CSC-335 | 3 | IS |
| 1020 | T77896 | CSE-439 | 3 | CS/IS |
| 1021 | B92996 | CSC-230 | 3 | CE |
| 1022 | A78835 | CSE-332 | 3 | CE |
| 1023 | B92996 | CSE-430 | 3 | CE |
| 1024 | T77896 | CSE-333A | 3 | CS/IS |
| 1025 | H10210 | CSE-433 | 3 | CE |
| 1026 | H10210 | CSE-334 | 3 | CE |
| 1027 | B92996 | CSC-131C | 3 | CS/IS |
| 1028 | B92996 | CSE-439 | 3 | CS/IS |

## 2.9.4 创建表之间的关系

接下来，我们需要使用主键和外键在这些五个表之间建立关系。在 Microsoft SQL Server 2019 数据库环境中，表之间的关系

# 使用 C# 进行 SQL 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_66_0.png)

图 2.37 通过使用对象资源管理器窗口中每个数据表下的“键”（Keys）来完成。

可以使用 Microsoft SQL Server Management Studio 18 建立 Login 表和 Faculty 表之间的关系。

### 2.9.4.1 创建 Login 表和 Faculty 表之间的关系

Faculty 表和 Login 表之间的关系是一一多多的关系，这意味着 `faculty_id` 是 Faculty 表中的主键，它可以被映射到 Login 表中作为外键的 `faculty_id`。

要建立此关系，在打开的 Microsoft SQL Server Management Studio 18 中，展开 Login 表以及 Login 表下的“键”文件夹。目前，在“键”下只存在一个主键 `PK_Login`。

要添加新的外键，点击“键”文件夹，并从弹出菜单中选择“新建外键”（New Foreign Key）项以打开关系对话框，如图 2.38 所示。

默认关系为 `FK_Login_Login`，显示在“已选关系”（Selected Relationship）框中。现在我们要在 Login 表和 Faculty 表之间创建外键关系，通过修改“标识”（Identify）面板下（名称）框中的名称，将此外键关系的名称更改为 `FK_Login_Faculty`。

然后，通过展开“常规”（General）面板下的“表和列规格”（Tables and Columns Specification）项来选择两个表。点击“表和列规格”项右侧的展开按钮，如图 2.39 所示。

点击“主键表”组合框的下拉箭头，从列表中选择 Faculty 表，然后点击紧邻“主键表”组合框的下方的行，并选择 `faculty_id` 列。你可以看到 Login 表已自动选择并显示在“外键表”组合框中。点击“外键表”组合框正下方框的下拉箭头，并选择 `faculty_id`

作为 Login 表的外键。完成后的“表和列”对话框应与图 2.40 所示的匹配。点击 OK 按钮关闭此对话框。

在我们关闭此对话框之前，还需要做一件事，即在父表 Faculty 中的主键（`faculty_id`）与子表 Login 中的外键（`faculty_id`）之间建立级联关系。我们需要这样做是因为我们希望简化如 CSE DEPT 等关系型数据库中这些表之间的数据更新和删除操作。在第 7 章学习如何对关系型数据库进行更新和删除数据时，你将对这种级联有更好的理解。

# 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_68_0.png)

**图 2.40** 完成的“表和列”对话框。

要执行此级联，向下滚动此“外键关系”对话框并展开**表设计器**(Table Designer）项，在其中你可以找到**插入和更新规格**(INSERT And UPDATE Specifications）项。展开此项后会显示两个子项，分别是：

- **删除规则**(Delete Rule）
- **更新规则**(Update Rule）

这两个项的默认值均为**无操作**（No Action）。点击“删除规则”项的**无操作**框并点击下拉箭头，从列表中选择**级联**（Cascade）。对“更新规则”项执行相同的操作。你完成后的“外键关系”对话框应与图 2.41 所示的匹配。

通过这种方式，我们建立了父表主键与子表外键之间的级联关系。此后，当你更新或删除父表中的任何主键时，子表中的相关外键也将随之更新或删除，无需任何额外操作。非常方便！

点击**关闭**(Close）按钮关闭此对话框。

转到**文件 | 保存**（File | Save）菜单打开**保存**对话框，并点击**是**(Yes）按钮保存此关系。当“保存更改脚本”（Save Change Script）对话框出现时，你可以选择**是**或**否**。在对象资源管理器中，右键点击 Login 表下的“键”文件夹，并从弹出菜单中选择“刷新”（Refresh）以显示此关系。你可以看到新创建的外键 `FK_Login_Faculty` 出现在“键”下。这是在 Login 表和 Faculty 表之间建立的新外键。你可以通过右键点击 Faculty 表下的“键”文件夹来确认并找到新创建的外键。

### 2.9.4.2 创建 Login 表和 Student 表之间的关系

通过这种方式，我们为 Login 表创建外键，并与 Student 表建立一一多关系。

## 数据库简介

![](img/d59a47501d0a20fc0460a49c469c6fb7_69_0.png)

图 2.41 完成的外键关系对话框。
