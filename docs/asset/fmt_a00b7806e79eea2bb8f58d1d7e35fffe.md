
# PROC STATEMENTS – 创建报告（第 19 章）

```
DEFINE BRAND/GROUP;
DEFINE CITYMP/ANALYSIS MEAN=6.1;
DEFINE HWYMP/ANALYSIS MEAN=6.1;
DEFINE SUV/ACROSS 'BY';
FORMAT SUV FMTTS.;
RUN;
```

```
DATA_NULL; SET GRADES END=EOF;
TABLEHEAD="SUMMARY OF GRADES";nFILE PRINT;
IF N_=1 then Do; * 输出标题;
L=(60-LENGTH(TABLEHEAD))/2; * 居中;
PUT @5 TABLEHEAD='
PUT @5 "NAME" @20 | TEST 1 @30 | TEST 2
@40 | TEST 3 @50 | AVERAGE";
PUT @5 60*'-';
END;
```

```
PUT @5 NAME @20 | G1 5.1 @30 | G2 5.1
@40 | G3 5.1 @50 | AVE 5.1;
IF EOF =1 then Do; * 输出表格底部;
PUT @5 60*'-';
PUT @5 "CLASS AVERAGE " @; * 保留行用于下次输出;
PUT @5 |TRIM(CLASSMEAN)" ;
PUT @5 60*'-';
END;
```

## 500 附录 D：快速参考

格式性别 `$fmtender.` 版本 `$fmtversion.` SATISFIED MARRIED FMTNY.;

```sas
****** 通过计算创建一个变量;
IF SATISFA GT 80 then SATISFIED=1; ELSE SATISFIED=0;
****** 使用 IN 语句创建一个新变量
IF ARRIVE IN("BUS","CAR") then HOW="Arrive by Vehicle"; else
HOW="Arrived by Walking";
****** 定义标签;
LABEL GENDER="Gender"
MARRIED="Married"
SATISFIED="Satisfied with Service"
HOW="How Arrived at Clinic?"
SCHOOLING="How Much School"
AGE="Age in 2016";
****** 设置缺失值;
IF TEMP GT 110 then TEMP=;
IF GENDER="X" then GENDER="";
****** 使用子集 IF 限制数据集中的记录;
IF STAYMINUTES GE 20;
****** 使用 SELECT 进行值编码;
SELECT
WHEN (EDU LT 12 and EDU GT 5) SCHOOLING="Less than 12";
WHEN (EDU EQ 12) SCHOOLING="High School";
OTHERWISE SCHOOLING="Some College";
END;
****** 删除（或保留）某些变量;
DROP SATISFA EDU;
PROC PRINT LABEL DATA=NEW;
VAR GENDER MARRIED HOW SATISFIED SCHOOLING;
RUN;
PROC MEANS MAXDEC=2 DATA=NEW;
CLASS SCHOOLING;
VAR TEMP STAYMINUTES;
RUN;
PROC FREQ DATA=NEW;
TABLE SCHOOLING*HOW;
RUN;
```

## 附录 E：使用 SAS 大学版

SAS University Edition (`SUE`) 是一个功能完整的 SAS 软件版本，包含了以下组件：SAS Studio、Base SAS、SAS/STAT 和 SAS/ACCESS。这些模块足以执行本书中的大多数示例。特殊情况将在后续的“局限性”章节中指出。虽然界面与本地安装版本不同，但该程序提供相同的分析功能。此外，`SUE` 可以在 PC (`Windows`)、`Mac` 或 `Linux` 上运行。关键区别在于，运行 `SUE` 必须连接活跃的互联网。当你使用 `SUE` 提交（运行）SAS 程序时，代码将通过互联网发送到服务器，在服务器处理后返回到你的工作站。附录展示了如何使用 `SUE` 运行示例。主要区别在于用户界面和访问文件的方式。本简报将介绍如何为 SAS Essentials 访问文件。

### E.1 安装 SAS 大学版

按照 SAS 提供的说明安装 `SUE`。安装方法根据计算机类型而异。以下是说明摘要（适用于 `Windows` 安装）。

**第 1 步：下载虚拟化软件** 要安装 `SUE`，请访问 `http://www.sas.com/en_us/university-edition/download-software.html`，并按照 SAS 的说明为你的电脑安装虚拟化程序（免费）。在本示例中，我们将在 `Windows` 平台上使用 Oracle VirtualBox。该网页上有多个虚拟应用程序供选择，请选择与你的电脑操作系统匹配的一个。

建议：
- 在安装 Virtual Box 时接受默认设置。
- 我们建议你下载并打印《快速指南》，以获取关于在电脑上运行 `SUE` 的特定说明。注意：你必须有一个 SAS 配置文件（免费设置）。如果你还没有，在安装过程中会提示你使用配置文件。
- 取决于你的电脑和网络速度，此过程可能需要 30 分钟或更久。

**第 2 步：将 SAS 添加到 VirtualBox（重要）**：我们建议在设置 `SUE` 之前下载书书中使用的示例文件。访问 `http://www.analyticseliot.com/sas` 网站并按照说明下载这些示例文件。这将创建一个名为 `C:\SASDATA` 的文件夹，其中包含 SAS Essentials 使用的示例文件。

作为 `SUE` 设置的一部分，你被要求创建一个 `C:\UniversityEdition` 文件夹。将 `C:\SASDATA` 文件夹中所有用于 SAS Essentials 的文件复制到 `C:\UniversityEdition`。

**第 3 步：启动 SAS**：一旦安装好虚拟机，按照以下步骤操作：
1. 启动 VirtualBox 虚拟机。
2. 虚拟机启动后，打开浏览器，在地址栏中输入 `http://localhost:8080` 并按回车。
3. 此时会出现 SAS Studio 界面。

**第 4 步：使用 SAS Essentials**：要测试 UE，请执行以下步骤：
A. 在列表中选择 `FIRST.SAS`。
B. 点击代码窗口顶部的“运行”（Running）图标。
C. 输入以下代码：
```sas
PROC MEANS DATA="folders/myfolders/SASDATA";
RUN;
```
输入代码后，点击运行图标，结果将出现在 RESULTS 标签中。这验证了你可以访问 SASDATA 文件夹中的 SAS 文件。如果出现错误，请检查日志（Log）。返回 CODE 标签，纠正代码并重新提交。

506 附录 E：使用 SAS® UNIVERSITY EDITION 配合 SAS ESSENTIALS

```
PROC MEANS DATA="folders/myfolders/SASDATA/SOMEDATA";
```

而不是使用

```
DATA "C:\SASDATA\NEWDATA";
```

你应该使用

```
DATA "/folders/myfolders/SASDATA/NEWDATA";
```

依此类推。

## E.2 创建持久性 SAS 库

在 `SUE` 中，要创建一个与书中提到的类似的持久性 SAS 库，请执行以下操作：

- 1. 点击屏幕左侧的 Libraries（库）选项卡。
- 2. 点击左侧的 New Library（新建库）图标。出现如图 E.6 所示的对话框。在对话框中输入以创建库 `mysaslib`。确保 `/folders/myfolders/` 与你创建的文件夹一致。
- 3. 勾选“Re-create this library at start-up（启动时重新创建此库）”。
- 4. 点击 OK 创建文件夹。

为了测试你的库，点击 CODE 并输入：

```
PROC MEANS data=mysaslib;
RUN;
```
