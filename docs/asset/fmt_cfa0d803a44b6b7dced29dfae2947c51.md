
layout overlay;

  scatterplot X=height Y=weight;

endlayout;

endgraph;

end;

run;

```

`SGENDER` 和 DATA 步都可以用于执行此模板。这两种技巧至少都要求你指定输入数据源和模板名称。在两种情况下，后台都会填充一个 ODS 数据对象并绑定到模板上。然后，数据对象被传递给图渲染器，由渲染器处理数据和图以生成输出图像。

`PROC SGENDER` 的语法非常简单。它使用 `DATA=` 选项指定数据源，使用 `TEMPLATE=` 选项指定用于渲染图的模板：

```sas
proc scatter data=sashelper.class template=mygraphs.scatter;
;
```

DATA 步稍微复杂一些。要执行 GTL 模板，DATA 文件和 PUT 语句提供了特定于 ODS 的语法。你至少必须指定以下内容：

```sas
data _null;
  set sashelper.class;
  file print _ods=(template=mygraphs.scatter*);
  put _ods;
```

- DATA 步使用关键字 `NULL` 作为数据集名称，这样 DATA 步在执行时就不会向输出数据集中写入变量。输入数据源通过 `SET` 语句定义。这种方法可以在当前示例中定义，但输入数据源可以是任何适当的 DATA 语法（带有 `DATELINES` 的 `INPUT`、带有 `INFILE` 的 `INPUT`、`MERGE`、`UPDATE` 等）。
- `FILE PRINT` 将输出重定向到 ODS。`PRINT` 是一个保留的文件引用，在执行 GTL 模板时是必需的。它将任何 `PUT` 语句产生的输出重定向到与 SAS 过程产生的相同文件中。
- `PUT _ods` 语句也是必需的，它在每次执行 DATA 步时都会将必要的变量写入输出对象中。

注意：输出数据对象所需的列是由图模板定义的列（在本例中为 `Height` 和 `Weight`），而不是输入数据源。在其他 DATA 步或过程处理中，如果你确切知道模板使用了哪些列，可以使用 `DROP=` 或 `KEEP=` 数据集选项来限制输入列，以稍微提高处理效率。

## 管理输入数据

### 过滤输入数据

如果不需要输入数据源中的所有变量或所有数据值，可以使用 `WHERE` 语句或输入 SAS 数据集选项（例如 `OBS=` `WHERE=`）来控制被处理的观测值。无论使用 `PROC SGENDER` 还是 DATA 步执行 GTL 模板，都可以使用过滤技巧。

在下面的示例中，第一个 `PROC SGENDER` 使用 `WHERE` 语句仅为图表选择女性观测值。第二个 `PROC SGENDER` 使用 `OBS=` 输入数据集选项来限制使用的观测值数量。

```sas
/* 仅绘制女性观测值 */
proc sgender data=sashelper.class template=mygraphs.scatter;
where sex="F";
run;
```

```sas
/* 测试模板 */
proc sgender data=sashelper.class(obs=5) template=mygraphs.scatter;
run;
```

## 执行数据转换

在使用 `PROC SGENDER` 时，必要的数据转换必须在模板执行之前进行。因此，转换需要中间步骤。例如，以下代码对 `Height` 和 `Weight` 列进行转换，转换结果存储在名为 `class` 的数据集中，并用于 `SGENDER` 语句：

```sas
data class;
set sashelper.class;
height*=24;
weight*=45;
label height="CM" weight="KG";
run;

proc sgender data=class template=mygraphs.scatter;
run;
```

在执行 DATA 步时，构建数据的 DATA 步可以执行任何必要的数据转换或计算。不需要中间步骤。下一个示例产生与之前的示例相同的图：

```sas
data _null_;
set sashelper.class;
height*=24;
weight*=45;
label height="CM" weight="KG";
file print ods=( template="mygraphs.scatter" );
```

## 初始化模板数据动态和宏变量

泛化模板的一种实用技巧是定义在模板执行时解析的动态和宏变量。

你可以创建新的宏变量，也可以使用 SAS 定义的自动宏变量（如 `SYSDATE`）。所有类型的宏变量在引用之前都必须声明。自动宏变量不需要初始化，但你必须初始化创建的宏变量。宏变量的值根据它们所处的符号表（局部或全局）获取。

以下模板声明了动态变量 `XVAR` 和 `YVAR`，以及宏变量 `STUDY` 和 `SYSDATE`：

```sas
proc template;
  define statgraph mygraphs.regfit;
    dynamic XVAR YVAR;
    mvar STUDY SYSDATE;
    begingraph;
      entitle"Regression fit for Model YVAR = XVAR";
      entryfoot align=left STUDY align=right SYSDATE;
    layout overlay;
      scatterplot X=XVAR Y=YVAR;
      regressionplot X=XVAR Y=YVAR;
    endlayout;
  endgraph;
end;
```

- `Dynamic` 语句声明了动态变量 `XVAR` 和 `YVAR`。在执行此模板的语句中，你必须通过分配输入数据源的变量来初始化这些动态，以便它们在运行时有值。
- `entitle` 语句将动态变量 `XVAR` 和 `YVAR` 拼接成字符串，作为图标题显示。在运行时，动态变量将被初始化时赋值的变量名称替换。
- `SCATTERPLOT` 和 `REGRESSIONPLOT` 语句在其 X 和 Y 属性上引用了动态变量。在两个图的运行时，赋值给 `XVAR` 的变量将为图提供 X 值，赋值给 `YVAR` 的变量将提供 Y 值。
- `MVAR` 语句声明了宏变量 `STUDY`。由于 `STUDY` 不是 SAS 自动宏变量，它将为此模板创建。在执行此模板的语句中，你必须为 `STUDY` 初始化一个值。

### 初始化模板动态和宏变量

- `ENTRYFOOTNOTE` 语句同时引用宏变量 `STUDY` 和 `SYSDATE`。你分配给 `STUDY` 的值将作为左对齐脚注显示，而 `SYSDATE` 的运行时值将作为右对齐脚注显示。

与所有 GTL 模板一样，`MYGRAPHS.REGFIT` 模板可以使用 `PROC SGENDER` 语句或 DATA 步执行。无论哪种方式，模板中声明的动态和/或新的宏变量都必须初始化以为它们提供运行时值。以下示例使用 `PROC SGENDER` 执行模板：

```sas
%let study=CLASS dataset;

proc sgender data=sashelp.class template=mygraphs.regfit;
dynamic xvar="height" yvar="weight";
```

- `%LET` 语句将字符串值 "CLASS dataset" 分配给宏变量 `STUDY`。
- `PROC SGENDER` 使用 `DYNAMIC` 语句初始化动态变量 `XVAR` 和 `YVAR`。`XVAR` 被赋值为输入变量 `HEIGHT`，`YVAR` 被赋值为输入变量 `WEIGHT`。

![](img/a9ccb6123dee40d424cb295a3a99c16c_450_0.png)

DATA 步使用 ODS 选项的 `DYNAMIC=` 子选项来初始化动态变量。宏变量可以从现有的符号表初始化。你可以在 DATA 步执行期间通过 `CALL SYMPUT` 或 `CALL SYMPTX` 更新符号表。以下示例使用 DATA 步执行 `MYGRAPHS.REGFIT` 模板：

```sas
data _null_;
if _N_=1 then call symput("study","CLASS dataset");
set sashelp.class;
file print ods=( template="mygraphs.regfit"
dynamic=( xvar="height" yvar="weight" ) );
run;
put _ods_;
```

- `CALL SYMPUT` 使用值 "CLASS dataset" 初始化宏变量。宏变量只需要初始化一次，因此 `IF` 语句将初始化限制在第一个观测值 `[_N_ = 1]`。
- `DYNAMIC=` 子选项初始化动态变量 `XVAR` 和 `YVAR`。`XVAR` 被赋值为输入变量 `HEIGHT`，`YVAR` 被赋值为输入变量 `WEIGHT`。

有关此主题的更完整讨论和更多示例，请参阅第327页第14章“使用动态和宏变量创建灵活模板”。

# 管理输出数据对象

## 设置输出列的标签和格式

默认情况下，输出数据对象的列从输入变量继承变量属性（名称、类型和标签）。然而，使用 `LABEL` 和 `FORMAT` 语句，你可以更改生成的输出对象列的标签和格式。

`LABEL` 和 `FORMAT` 语句适用于 `PROC SGENDER` 和 DATA 步。以下示例为用于 `MYGRAPHS.SCATTER` 模板的 `HEIGHT` 和 `WEIGHT` 变量分配标签，并为 `WEIGHT` 变量分配了格式。

```sas
proc sgender data=sashelp.class template=mygraphs.scatter;
label height="Height in Inches" weight="Weight in Pounds";
run;
```

## 为输出数据对象设置名称和标签

创建输出数据对象时，它会被分配一个名称和一个标签。下表显示了默认名称和标签，取决于相应的 GTL 模板是使用 `PROC SGENDER` 语句还是 DATA 步执行的：

| 选项 | PROC SGENDER 的默认名称 | DATA 步的默认名称 |
|---|---|---|
| OBJECT=name | SGENDER | FilePrint (DATA 步的每次执行都会增加对象名称：FilePrint1, FilePrint2 等以此此类推) |
| OBJECTLABEL="string" | SGENDER Procedure | 与对象名称相同 |

使用 `PROC SGENDER` 或 DATA 步，你都可以使用 `OBJECT=` 选项为输出数据对象设置名称。你可以使用 `OBJECTLABEL=` 选项为数据对象设置描述性标签。以下示例在 `PROC SGENDER` 中设置了名称和标签：

```sas
/* Open ODS LISTING destination */
ods close;
ods listing;

/* set object name and label on PROC SGENDER */
proc sgender data=sashelp.class template=mygraphs.scatter
object=Scatter1
objectlabel="Scatter Plot 1";
run;
```

此示例在 DATA 步中设置了名称和标签：

```sas
/* set object name and label on DATA step */
data _null_;
set sashelp.class;
file print ods=( template="mygraphs.scatter"
object=Scatter2
objectlabel="Scatter Plot 2" );
put _ods_;
run;
```

## 在结果窗口查看数据对象的名称和标签

执行 GTL 模板时，ODS 对象会被填充并绑定到模板。该对象被分配一个名称，可以在各种 ODS 语句（如 `ODS SELECT`、`ODS EXCLUDE` 和 `ODS OUTPUT`）中引用。数据对象还分配了标签。对象名称和标签出现在结果窗口。要查看它们：

1. 如果尚未打开，请打开结果窗口。
2. 右键点击图表并选择属性（Properties）。

下图显示了在“设置数据对象的名称和标签”中创建的对象。结果窗口显示了创建的两个对象，Scatter2 窗口显示了名为 Scatter2 的对象的属性。

![](img/a9ccb6123dee40d424cb295a3a99c16c_)

## 为输出图像文件设置名称

默认情况下，输出图像文件与输出数据对象的名称相同。你可以使用 `ODS GRAPHICS` 语句中的 `IMENAME` 选项为输出图像分配备用名称。例如，以下代码为输出图像分配了 `fit_heightweight`：

```sas
ods graphics imagename="fit_heightweight";

proc sgender data=sashelp.class template=mygraphs.regfit;
dynamic xvar="height" yvar="weight";
```

## 将输出数据对象转换为 SAS 数据集

可以使用 `ODS OUTPUT` 语句将数据对象转换为 SAS 数据集。通常，你需要识别要转换的对象并分配一个名称。当使用 `PROC SGRENDER` 执行 GTL 模板时，输出数据对象始终命名为 `SGRENDER`。因此，你可以通过 `ODS OUTPUT` 语句中的该名称识别数据对象。以下示例将数据对象转换为名为 `fit1` 的 SAS 数据集：

```sas
ods output sgender=fit1;

proc sgrender data=sashelp.class template=mygraphs.regfit;
dynamic xvar="height" yvar="weight";
run;
```

由于 DATA 步的输出对象每次执行都会变化，因此使用 `DATA FILE` 语句上的 `OBJECT=` 选项设置名称以便于识别。以下示例为数据对象分配名称 `DATAOBJ`，并将其转换为名为 `fit2` 的 SAS 数据集：

```sas
ods output dataobj=fit2;

data _null_;
  if _N_=1 then call symput("study","CLASS dataset");
  set sashelp.class;
  file print ods=( template="mygraphs.regfit"
                dynamic=( xvar="height" yvar="weight" )
                object=dataobj );
put _ods_;
run;
```
