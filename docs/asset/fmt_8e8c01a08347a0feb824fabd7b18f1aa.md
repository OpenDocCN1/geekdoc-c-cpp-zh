
```
  do Duration=1 to 5 by 4;

    Total=5000;

    interest(Total,Rate,Duration);

    output;

end;

end;

```
图 4.1 显示了使用 `interest` 方法计算在 `crs.banks` 数据集中每家银行存款 5,000 美元在期为一年和五年的最终结果。使用了用户定义的 `interest` 方法，根据数据集中每家银行存储的利率进行计算。

### 图 4.1：使用用户定义利率方法的结果
每家银行的结果 - 初始 $5,000 存款

| 总计 (Total) | 期限 (Duration) | 银行 (Bank) | 利率 (Rate) |
|---|---|---|---|
| $5,159.00 | 1 | Carolina Bank and Trust | 0.0318 |
| $5,847.20 | 5 | Carolina Bank and Trust | 0.0318 |
| $5,160.50 | 1 | Big Federal Credit Union | 0.0321 |
| $5,855.70 | 5 | Big Federal Credit Union | 0.0321 |
| $5,164.00 | 1 | National Savings and Trust | 0.0328 |
| $5,875.59 | 5 | National Savings and Trust | 0.0328 |

如果我们希望方法像函数一样返回一个值，而不是修改其参数之一，我们会有何不同？这个版本将没有 `IN_OUT` 参数，并且在被调用时，必须在能够处理返回结果的表达式中调用。让我们创建一个返回值并从赋值语句中调用的版本。

```
proc ds2;

title '每家银行的结果 - 初始 $5,000 存款';ntitle2 '方法像函数一样返回一个值';ndata;

dcl double Total having format dollar10.2;

dcl int Duration;

keep total duration bank rate;

```

## 精通 SAS DS2 过程：高级数据处理技术

```
method interest(double Amount, double Rate, int Years)

  returns double;

  dcl int i;

  do i=1 to Years

    Amount=SUM(Amount,Amount*Rate);

  end;

  return Amount;

end;

method run();

  set crs.banks;

  do Duration=1 to 5 by 4

    Total=interest(5000,Rate,Duration);

    output;

  end

enddata;

run;

quit;

title:

```

图 4.2 显示了使用修改后的用户定义 `interest` 方法计算在 `crs.banks` 数据集中每家银行存款 5,000 美元在期为一年和五年的最终结果。结果与之前版本产生的结果相同。这是预料之中的，因为我们没有更改用于计算利率的算法，只更改了将结果返回给调用过程的方法。

### 图 4.2：使用修改后定义的利率方法的结果

每家银行的结果 - 初始 $5,000 存款
方法像函数一样返回一个值

| 期限 (Duration) | 银行 (Bank) | 利率 (Rate) |
|---|---|---|
| $5,159.00 | 1 | Carolina Bank and Trust | 0.0318 |
| $5,847.20 | 5 | Carolina Bank and Trust | 0.0318 |
| $5,160.50 | 1 | Big Federal Credit Union | 0.0321 |
| $5,855.70 | 5 | Big Federal Credit Union | 0.0321 |
| $5,164.00 | 1 | National Savings and Trust | 0.0328 |
| $5,875.59 | 5 | National Savings and Trust | 0.0328 |

### 4.2.2.3 利率方法 – V1.1

现在公司里的每个人都在使用我们的新方法进行利率计算，我们发现了一个缺陷：利息可以按年复利。如果我们需要按季度、每周甚至每天复利怎么办？让我们创建 `interest` 的 1.1 版本，它在每年用户指定的周期数内复利后返回总额。新的利率计算算法如下：

```
do i=1 to Years;

  do j=1 to Periods;

Amount=SUM(Amount,Amount*(Rate/periods));

end;

end;

```

我们需要添加一个周期数量的参数。

```
proc ds2;

title '每家银行的结果 - 初始 $5,000 存款';

title2 '变量复利周期';

data;

dcl double Total having format dollar10.2;

dcl int Years Periods;

keep total Years periods bank rate;

method interest(double Amount, double Rate, int Years

, int Periods) returns double;

dcl int i, j;

do i=1 to Years;

do j=1 to Periods;

Amount=SUM(Amount,Amount*(Rate/periods));

end;

end;

```

# 掌握 SAS DS2 过程：高级数据处理技术

DS2 程序包没有内置机制来确定包中包含哪些方法。此外，要修改单个方法，需要重新创建整个包。如果你在使用 DS2 程序包——我强烈建议你这样做——你将需要一些管理措施来使它们更容易使用和管理。我建议采取一些可以提高易用性并简化管理的实践：

- 在你创建的每个包中，都包含一个用户定义的 `CONTENTS` 方法。`CONTENTS` 方法不应接受参数。当调用此方法时，它应该在 SAS 日志中记录该包的文档。至少，它应该提供包中包含的方法列表以及源代码的位置。在对包进行任何维护时，你都需要整个包的源代码，因为每次进行更改都必须重新创建整个包。
- 包中的每个方法都应该通过重载一个不接受参数的方法版本，该版本的作用仅是在 SAS 日志中记录该方法。

让我们创建一个简单的包，其中包含我们感兴趣的两个版本的两个方法，还包含了上述讨论的自文档功能：

```
proc ds2;

package crs.MyMethods;

 contents();

  put 'This package contains the following methods:';

put '  - contents();';

put '  - interest();';

put;

  put 'Package source:';

put %tslit(&path);

put;

end;

method interest();

  put 'Syntax: interest(Amount,Rate,Years,Periods)>';

put '  Amount (double) - original amount';

put '  Rate (double) - interest rate';

put '  Years (int) - number of years for interest'

put '  yield();';

put '  Periods (int) - number of compounding periods';

put '  per year (optional)';

put;

  put 'If Periods are not specified, interest compounds annually;

  Returns total amount after compounding (double)'

put;

end;

method interest(double Amount, double Rate, int Years)

  returns double;

dcl int i;

do i=1 to Years;

  Amount=SUM(Amount,Amount*Rate);

end;

  return Amount;

end;

method interest(double Amount, double Rate, int Years

  , int Periods) returns double;

dcl int j;

do i=1 to Years;

do j=1 to Periods;

Amount=SUM(Amount, Amount*Rate/periods);

end;

return Amount;

endpackage;

run;

quit;

title:;

```

# SAS 日志：

> NOTE: Created package mysymethods in data set cr.mysymethods.
NOTE: Execution succeeded. No rows affected.

如果你和我一样好奇，你会想查看数据集 `cr.mysymethods` 看看包是什么样子的。去看看吧！如图 4 所示，你会发现一个小小的纯文本头，后面跟着一堆神奇的源代码。很酷，但没什么可读性。

### 图 4.4：CRS.MyMethods 包的内容

![](img/ef05c3db88dda150abd07414dd206d3f_75_0.png)

| SAS_ROWID_ | SAS_CHECKSUM | SAS_TEXTPACKAGE_ |
|---|---|---|
| 1 | 18122651414 | DATA_STEP_2_PROGRAM |
| 2 | 6098780327 | 1568 |
| 3 | 6687380327 | |
| 4 | 3029824840 | |
| 5 | 7189461221 | FTMTOEDANEVPE65EIA603MTPINGPESTVGQ4GOLLEINWR4LEJWT65 |
| 6 | 6450382472 | |
| 7 | 9017327308 | VALUHYGTEDK31FTGUE55CAKS55RP.INJDOTGGUOMSTHLQ |
| 8 | 42215452817 | KMWSKWMQDBLLQUIFSHYTYORZBHFTYROWCZNASMMCC |
| 9 | 2693584753 | MKDXQRAVUON6JVAHYODTSYXO5FBR32ZXHWNR36OFA2I |
| 10 | 7120110423 | HFEUEIBVNF63CAET33IN3OAS57K33INOAS57K33 |
| 11 | 2456580629 | GZJYTFT2WKYGJ32ZTDOVE7JHPDTUTXL4 |

## 4.3.2 使用包中的方法

要使用包中的方法，你需要声明并实例化包的实例。当你声明包时，会给实例指定一个标识符。要使用包中的方法，只需使用点语法 `instance.method()` 来调用它们。

包通过 `DCL PACKAGE` 语句声明，并可以在编译时实例化——即同时声明和实例化。或者，也可以在运行时实例化——即先声明，然后在单独的可执行语句中实例化。这并不复杂。但如果包构造方法需要直到程序开始执行才能获得的信息，我们需要运行时实例化包，因为我们构建的包没有使用参数。稍后我们将看到一个示例。

这是一个使用我们在上一节中创建的包中的 `CONTENTS` 方法的程序：

```
proc ds2;

data _null;

  /* Declare and instantiate the package */

  /* This instance's identifier is mm */

  dcl package crs.MyMethods mm();

  method init();

    /* Execute contents method from instance mm */

    mm.contents();

  end;

run;

```

此包包含以下方法：
- contents()
- interest()

源代码：

接下来，我们将使用不带参数的 `interest` 方法版本来检索其语法：

```
proc ds2;

data _null;

  dcl package crs.MyMethods mm();

  method init();

    mm.interest();

  end;

run;

quit;

```

SAS 日志：

Syntax: interest(Amount,Rate,Years,Periods)>
Amount (double) - 原金
Rate (double) - 利率
Years (int) - 年数
Periods (int) -每年复利周期（可选）

当未指定周期时，利息按年计算；返回复利后的总金额 (double)

现在我们知道了语法，让我们使用 `interest` 方法来执行一些工作：

```
proc ds2;

title 'Results for each bank - initial $5000 deposit';

title 'compounding annually and daily ';data;

dcl package cr.MyMethods mm();

dcl double Total;

dcl int Periods;

keep Total Years bank;

method run();

Years=5;

Periods=1;

Total=mm.interest(5000,Rate,Years);

output;

Periods=365;

Total=mm.interest(5000,Rate,Years,Periods);

output;

enddata;

run;

quit;

title;

```

### 图 4.5：使用包方法的 DS2 程序输出
每个银行的结果——初始 $5,000 存款按每年和每日复利

| | 年 | 银行 | |
|---|---|---|---|
| $5,847.20 | 5 | 1 | Carolina Bank and Trust | 0.318 |
| $5,861.65 | 5 | 365 | Carolina Bank and Trust | 0.318 |
| $5,855.70 | 5 | 1 | Big Federal Credit Union | 0.321 |
| $5,870.45 | 5 | 365 | Big Federal Credit Union | 0.321 |
| $5,875.59 | 5 | 1 | National Savings and Trust | 0.328 |
| $5,891.03 | 5 | 365 | National Savings and Trust | 0.328 |

### 4.3.3 使用 DS2 包进行面向对象编程

DS2 包的最终威力在于利用它来实现面向对象的应用程序设计。在面向对象编程中，软件对象可以用于对现实世界对象建模，然后可以将现有对象组合起来建模其他更复杂的对象，而无需重写或重新测试现有对象的功能。这可以显著加快开发周期。对于那些想在 DS2 程序包上“更上一层楼”的人，我们将简要查看如何在 DS2 程序中使用包作为对象使用。

你可以将包认为是一个“类”：包作为创建对象实例的模板，并包含了创建和销毁该实例所需的的方法、提供对象的行为（方法）以及跟踪对象的当前状态（私有全局变量）。例如，一个家用灯。灯有功能（方法），例如操作开关和它的状态——开启或关闭。在创建模拟灯的 DS2 包中，我们将编写方法来提供灯的功能，并创建包变量来跟踪灯的状态。

虽然包不能包含自动执行的系统方法 INIT、RUN 和 TERM，但每个包都包含两个特殊方法：构造方法和析构方法。构造方法和析构方法不返回类型且不能返回值。

析构方法始终是 `DELETE`，由 DS2 包程序自动生成。当包终止（销毁）时，它会执行清理并将包释放回系统。你可以编写自己的 `DELETE` 方法来添加自定义例程。当包实例离开范围并销毁时，`DELETE` 方法会自动执行。

## 第 4 章：用户定义方法与包 63

```
method lamp(varchar(15) name);

    put *** 正在实例化一个灯 ***;

    lampName=name;

    put lampName 'lamp status not set. It is off (default).';

    put;

end;

method lamp(varchar(15) name, varchar(3) state);

    put *** 正在实例化一个灯 ***;

    lampName=name;

    state=lowercase(state);

    if state='on' then do;

        lampIsOn=1;

        put lampName 'lamp is on.';

    end;

    else if state='off' then do;

        lampIsOn=0;

        put lampName 'lamp is off.';

    end;

    else do;

        lampIsOn=0;

        put 'The specified state must be ''off'' or ''on''.';
