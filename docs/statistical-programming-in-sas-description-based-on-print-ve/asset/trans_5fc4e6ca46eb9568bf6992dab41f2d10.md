

宏程序通过对 %PROG-NAME 的引用来调用。分号不是必需的。%PROG-NAME 是与宏处理器对话，而不是与其他 SAS 组件对话。

参数可以传递给宏程序。 （“参数”一词对统计学界有技术含义，对编程界有不同的含义。这里，“参数”是宏的参数，其值可能会影响宏的行为。）在此宏程序示例中，探索了复杂的宏变量构造。请考虑显示 10.8 中的示例。需要解析两个宏变量来定义第三个宏变量。变量具有权重（weight1 和 weight2）的假设值，分别在两个不同的时间点（week1 和 week2）测量。两个宏参数（variable 和 obs）标识感兴趣的变量和时间点。此宏设计为回显日志中的输入并打印感兴趣变量的值。

## 显示 10.8 解析复杂的宏变量

```
%let var1=week;
%let var2=weight;
%let time1=1;
%let time2=2;
%let var1time1 = week1;
%let var1time2 = week2;
%let var2time1 = weight1;
%let var2time2 = weight2;

data tester;
  input week1 weight1 week2 weight2;
  datalines;
15 70 25 74
;
run;

%macro showvalue(variable, obs); * positional parameter;
  %put Value of '&variable' = &variable;
  %put Value of '&obs' = &obs;
  %put Value of '&&&variable.&obs' = &&&variable.&obs;
  proc print;
    var &&&variable.&obs;
  run;
%mend showvalue;

%showvalue(var1, time1)

%showvalue(var2, time2)
```

此程序中一个有趣的构造是 &&&variable.&obs。宏变量名称从左到右解析。&& 由宏处理器解析为 &。在此示例中，当 &variable=var1 (=week) 且 &obs=time1 (=1) 时，&&&variable.&obs 的值为 var1time1 (=week1)。调用此宏的 SAS 日志显示在显示 10.9 中。

## 显示 10.9 调用宏的输出

```
%showvalue(variable=var1, obs=time1)
Value of '&variable' = var1
Value of '&obs' = time1
Value of '&&&variable.&obs' = week1
```

在显示 10.10 中定义的宏 trap_area_Z 中，梯形法则面积估计代码周围放置了一个宏包装器。为此宏定义了参数：LOW、HIGH、npts_lo、npts_hi、npts_by、fout、print_est、print_pts、display_graph 和 ODS_on。trap_area_Z 的宏声明包括这些参数及其默认值。

```
%macro trap_area_Z
(LOW=-1.645,HIGH=1.645,npts_lo=10,npts_hi=10,npts_by=2,
fout=C:\Users\baileraj.IT\Desktop\est3.out,
print_est=FALSE, print_pts=FALSE, display_graph=FALSE,
ODS_on=FALSE);
```

与显示 10.8 中的位置参数相反，trap_area_Z 宏定义中使用了关键字参数。参数可以通过位置、关键字或两种策略的混合传递。 （如果使用混合，则必须在关键字参数之前指定位置参数。）如果您定义了关键字参数，则必须使用关键字在参数列表中调用宏。宏定义中使用的样式必须与调用宏时使用的样式相匹配。出于编写自文档化代码的精神，关键字参数是首选。

trap_area_Z 宏的构造明确解决了两个问题：

- 1. 你能设置一个开关，仅在请求时才生成图形吗？
- 2. 是否可以将此估计器打包为可调用程序、子例程或函数？

让我们从此宏的名称及其输入参数开始。输入参数在宏中分配默认值。宏注释描述输入参数。这些注释以 %* 开头，以分号结束。如果您使用标准注释（例如，以星号开头，以分号结束），则注释会显示在日志中。但是，注释要到设置适当选项后才会显示。注意：宏内部使用最安全和首选的注释形式为 /* comment ... */。

在显示 10.5 中，您将硬编码值转换为宏变量。宏变量使用 %LET 语句分配值。在以下宏中，打印、生成图形和使用 ODS RTF 均基于宏的参数。%IF 和 %THEN 语句检查是否请求图形。例如，提交以下代码块：

```
%if %upcase(&display_graph)=TRUE %then %do;
    ods graphics on;
    proc sgplot data=trapper2;
    title "Plot of function values vs. x-values";
    scatter x=xout y=yout;
    run;
    ods graphics off;
%end;
```

当宏参数 display_graph=true 时，此代码会导致以下行被包含在处理输入堆栈中。

```
ods graphics on;
proc sgplot data=trapper2;
title "Plot of function values vs. x-values";
scatter x=xout y=yout;
run;
ods graphics off;
```

%upcase 函数保证 &display_graph 值为 TRUE、True 或 true 在与条件比较之前转换为 TRUE。然后由宏处理器评估 %IF 和 %THEN 语句。如果为真，则 %DO 和 %END 语句之间的代码作为输入堆栈的一部分进行处理。宏可以根据一系列值评估积分。此选项使用带有 %end 语句的 %do、%to 和 %by 设置。例如：

```
%do npts=&npts_lo %to &npts_hi %by &npts_by; *loop over npts values;
```

如果将所有这些想法放在一起，您将得到显示 10.10 中所示的宏。

## 显示 10.10 构建标准正态密度曲线下面积的梯形法则估计

```
```sas
%macro trap_area_z(LOW=-1.645, HIGH=1.645, npts_lo=10, npts_hi=10, npts_by=2,
    fout=C:\Users\baileraj.IT\Desktop\test3.out,
    print_set=FALSE, print_pts=FALSE, display_graph=FALSE, ODS_on=FALSE);

/* -------------------------------------------------------------------------
Purpose: Estimate P(LOW<Z< HIGH) using the trapezoidal rule
Macro variables:
LOW, HIGH: interval of interest
NPTS_LO, NPTS_HI, NPTS_BY: # function values evaluated in area calc.
FOUT: output data file containing area estimate for each NPTS value
PRINT_EST: print area estimate
PRINT_PTS: print points/nodes {x1-xn} + function values {f(x1)-f(xn)}
DISPLAY_GRAPH: generate PROC GPLOT with function values
ODS_ON: generate ODS RTF output
------------------------------------------------------------------------- */

%do npts = &npts_lo %to &npts_hi %by &npts_by; *loop over npts values;

data trapper;
    file "&fout" MOD;
    trapsum = 0;
    array x_value(&npts) x1-x&npts;
    array f_value(&npts) y1-y&npts;

    low  = &LOW;
    high = &HIGH;
    incr = (high-low)/(( &npts )-1);
    pi = arccos(-1);
    do i=1 to &npts;
        x_value[i] = low + incr*(i-1);
        f_value[i] = (1/sqrt(2*pi))*exp(-x_value[i]*x_value[i]/2);

        if i=1 or i=&npts then trapsum = trapsum + f_value[i]/2;
        else trapsum = trapsum + f_value[i];
    end;
    area_est = trapsum*incr;
    output;

put "est. P(&LOW < Z < &HIGH) =" area_est "(based on &NPTS points)";
run;

%if %upcase(&ODS_ON)=TRUE %then %do;
    ods rtf bodytitle file = "C:\Users\baileraj.IT\Desktop\trap.rtf";
%end;

%end;
%mend;
```
```

## 显示 10.10 （续）

```
%if %upcase(&print_est)=TRUE %then %do;
proc print data=trapper;
  title "Trapezoidal Rule Area Estimate for P(&LOW<Z<&HIGH)";
  title2 " (based on &NPTS equally spaced points)";
  var low high incr area_est;
run;
%end;

data trapper2;
  set trapper;
  array x_value(&npts) x1-x&npts;
  array f_value(&npts) y1-y&npts;
  do ii=1 to &npts;
    xout = x_value[ii];
    yout = f_value[ii];
    output;
  end;
run;

%if %upcase(&print_pts)=TRUE %then %do;
proc print data=trapper2;
  title "Interpolation Points for Trapezoidal Rule";
  var ii low high incr area_est xout yout;
run;
%end;

%if %upcase(&display_graph)=TRUE %then %do;
ods graphics on;
proc sgplot data=trapper2;
  title "Plot of function values vs. x-values";
  scatter x=xout y=yout;
run;
ods graphics off;
%end;

%if %upcase(&ODS_ON)=TRUE %then %do;
ods rtf close;
%end;

%end;   * of loop over npts values;
%mend trap_area_2;
```

您可以使用 %GOTO 在执行期间指示宏处理器移动到不同位置。%GOTO 在检查错误时特别方便。在显示 10.11 中的代码和显示 10.12 中的输出中，如果将无效参数作为参数传递，则会生成错误消息。%sysevalf 函数评估 &npts<1 是否成立。如果是，则生成错误消息并执行分支。宏变量 &npts 用单引号括起来。这可以防止宏处理器评估此变量。如果宏变量用双引号括起来，则宏处理器会在表达式中替换宏变量的值。

