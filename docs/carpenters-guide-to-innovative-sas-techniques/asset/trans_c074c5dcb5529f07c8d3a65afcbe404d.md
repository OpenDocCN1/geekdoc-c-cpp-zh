
由于没有一种信息格式能有效结合 ANYDTDTM. 信息格式的灵活性与解释 AM/PM 的能力，可以使用以下调整。❷

```sas
dt_plus = input(datetime, anydtdtm.) ❶
        + (43200 ❸
        * (index(upcase(datetime), 'PM') > 0) ❹);
```

## 12.6 ANYDTDTM 信息格式

### 转换混合 DATETIME 值

| 观测 | datetime | dt_plus |
|---:|---|---|
| 1 | 10/13/2011:15:45:12 | 13OCT2011:15:45:12 |
| 2 | 2011-03-01T15:20:45 | 01MAR2011:15:20:45 |
| 3 | 9/13/2011 11:52:54 AM | 13SEP2011:11:52:54 |
| 4 | 9/13/2011 11:52:54 PM | 13SEP2011:23:52:54 |
| 5 | 11/09/2011 11:52:54 PM | 09NOV2011:23:52:54 |
| 6 | 9/13/12 11:52:54 AM | 13SEP2012:11:52:54 |
| 7 | 2011/09/12 11:52:54 PM | 12SEP2011:23:52:54 |

ANYDTDTM. 信息格式用于转换日期时间字符串。INPUT 函数以秒为单位返回日期时间值。如果存在“PM”，我们需要向日期时间值加上 12 小时对应的秒数（43,200 = 12*60*60）。❸ INDEX 函数搜索“PM”的出现位置，并将该位置转换为二进制 0/1 值，再乘以要添加的秒数。❹

## 12.7 从数据集构建格式

VALUE、INVALUE 和 PICTURE 语句通常用于创建用户定义的格式或信息格式。随着值对数量变大，编写这些语句变得不方便（对我来说，所谓的大可能还不到一打）。幸运的是，你也可以使用数据集定义格式和信息格式。

PROC FORMAT 接受一个数据集来控制格式或信息格式的定义。该过程期望特定的变量，并使用数据集的观测值来形成值对。至少，用于控制格式形成的数据集必须包含变量 FMTNAME、START 和 LABEL ❶。它还可以包含二十多个其他变量，用于定义格式。

在此示例中，数据集 CNTLRFMT 将用于创建字符格式（$CL_REG.），该格式会将诊所编号（CLINNUM）映射到区域（REGION）。

```sas
data cntrlfmt (keep=fmtname start label) ❶;
    set advrpt.clinicalnames(rename=(clinnum=start ❷
                                     region=label));
    retain fmtname '$cl_reg'; ❸
run;
proc format cntlin=cntrlfmt; ❹
run;
```

❶ 你可以保留不会被 PROC FORMAT 使用的变量。无关变量将被忽略。

❷ 变量 START 包含要映射的数据值（值对的左侧），而 LABEL 是映射结果中将出现的值。

❸ 字符变量 FMTNAME 包含要创建的格式的名称。

❹ CNTLIN= 选项用于指定包含格式定义的数据集。

控制数据集可以定义多个格式定义；但是，如果这样做，数据集必须按格式名称排序（或至少按格式名称分组）。在以下示例中

```sas
data cntrlfmt(keep=fmtname start label);
   set advrpt.clinicalnames(rename=(clinnum=start));
   length fmtname $8 label $40;
   fmtname = '$cl_reg';
   label = region;
   output cntrlfmt;
   fmtname = '$cl_name';
   label = clinname;
   output cntrlfmt;
run;
proc sort data=cntrlfmt;
   by fmtname start;
run;
proc format cntlin=cntrlfmt;
run;
```

每个传入观测用于构建两个格式（$CL_REG 和 $CL_NAME）。请注意，在将控制数据集传递给 FORMAT 过程之前，已按格式名称对其排序。

控制数据集中可供 PROC FORMAT 使用的潜在变量列表相当广泛；虽然它们有详细文档，但你可以使用 PROC FORMAT 和 CNTLOUT= 选项，通过将格式定义写入数据集来呈现它。这将揭示格式定义中可以使用的变量名，并能让你很好地了解它们的用法。

```sas
proc format cntlout=control(where=(fmtname='CL_NAME'));
run;
proc print data=control;
run;
```

| 观测 | FMTNAME | START | END | LABEL | MIN | MAX | DEFAULT | LENGTH | FUZZ | PREFIX | FILL | TYPE | NOEDIT | SEXCL |
|---:|---|---|---|---|---:|---:|---:|---:|---:|---:|---:|---|---|---|
| 1 | CL_NAME | 011234 | 011234 | 波士顿国家医疗 | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |
| 2 | CL_NAME | 014321 | 014321 | 佛蒙特治疗中心 | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |
| 3 | CL_NAME | 023910 | 023910 | 纽约都会医疗中心 | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |
| 4 | CL_NAME | 024477 | 024477 | 纽约综合医院 | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |
| 5 | CL_NAME | 026789 | 026789 | 日内瓦纪念医院 | 1 | 40 | 27 | 27 | 0 | 0 | 0 | C | N | N |

```sas
libname oldfmt 'c:\temp1';
libname newfmt 'c:\temp2';
libname allfmt (newfmt oldfmt);

proc format library=oldfmt;
  value yesno 1 = 'Yes'
              0 = 'No';
  value generation
    low - <1950 = 'Greatest'
    1950 - high = 'Boomer';
run;

proc format library=newfmt;
  value gender 1 = 'Female'
               0 = 'Male';
  value yesno 1 = 'No'
              0 = 'Yes';
run;

title1 '12.9.3 Display Format names';
proc catalog cat=allfmt.formats;
  contents;
quit;

options fmtsearch=(allfmt work);
```

- 1. 对*库引用* ALLFMT 的任何引用都将指向另外两个位置。
- 2. YESNO. 格式同时出现在两个格式库中。请注意，这两个定义*不*相同。
- 3. 此处使用 PROC CATALOG 来显示格式的位置。LEVEL 列指包含该格式的目录所在的库。
- 4. 在使用 ALLFMT 库中的任何格式之前，必须将该库包含在搜索路径中。ALLFMT 中的格式将先于 WORK 库中任何同名格式被找到。在 ALLFMT 内部，目录从左到右搜索。将使用 NEWFMT 库中 YESNO. 格式的版本。

CATALOG 过程生成的输出显示，各种格式可以在串联库 ALLFMT 中找到。它还显示，在 OLDFMT 和 NEWFMT 目录中都定义的 YESNO. 格式，正从列表中的第一个目录（NEWFMT – LEVEL=1）中选取。

### 12.9.3 显示格式名称

| # | 名称 | 类型 | 级别 | 创建日期 | 修改日期 | 描述 |
|---:|---|---|---:|---|---|---|
| 1 | GENDER | FORMAT | 1 | 11Dec11:14:40:49 | 11Dec11:14:40:49 | |
| 2 | GENERATION | FORMAT | 2 | 11Dec11:14:40:49 | 11Dec11:14:40:49 | |
| 3 | YESNO | FORMAT | 1 | 11Dec11:14:40:49 | 11Dec11:14:40:49 | |

![](img/4b16455363806a3241267bf9f49ba5d1_425_0.png)

## 第 13 章：与宏语言交互

- 13.1 避免宏变量冲突——让你的宏变量成为 %Local 398
- 13.2 使用 SYMPUTX 例程 400
  - 13.2.1 与 CALL SYMPUT 比较 401
  - 13.2.2 使用 SYMPUTX 保存选项值 402
  - 13.2.3 使用 SYMPUTX 构建宏变量列表 402
- 13.3 通用程序——主题变奏 403
  - 13.3.1 程序泛化的步骤 403
  - 13.3.2 泛化层次与宏语言理解层次 405
- 13.4 使用宏库 406
  - 13.4.1 建立自动调用库 406
  - 13.4.2 跟踪自动调用宏位置 408
  - 13.4.3 使用存储的已编译宏库 408
  - 13.4.4 宏库搜索顺序 409
- 13.5 元数据驱动程序 409
  - 13.5.1 跨数据集处理 409
  - 13.5.2 控制数据验证 410
- 13.6 硬编码——不要这样做 415
- 13.7 编写宏函数 417
- 13.8 宏信息来源 420
  - 13.8.1 使用 SASHELP 和 Dictionary 表
  - 13.8.2 检索系统选项和设置 422
  - 13.8.3 访问 SAS 数据集的元数据 424
