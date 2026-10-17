

## 第12章 函数

在程序定义部分，带有尾部注释 #5 的函数定义中，你使用了参数数组的隐式形式来访问 @GreenhouseGasses 数组中的元素。这种用法出现在 foreach 重复语句后面的参数中。它允许你以表格行的形式打印数组中的元素。代码如下：

```perl
foreach $Gas (@_) { #lines left out
```

在这种情形下，你不需要数组的标量形式，因为你无需具体访问各个元素，正如在 makeTableHeading() 函数中处理列标题和表格标题时那样。在这里，通过遍历数组并依次打印每个元素，你满足了函数设定的要求。

在任何给定的函数定义中，你可以同时或单独使用参数数组的标量形式和隐式形式。图 12.10 展示了使用这两种方式传递参数数组所生成的表格。

**图 12.10** 你可以直接使用参数数组，而无需在本地复制它。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_336_0.png)

### 将哈希作为参数传递

当你向函数传递哈希时，参数数组会将哈希转换为数组。要在函数定义中处理该哈希，你必须将参数数组提供的元素重新转换回哈希。你可以通过将参数数组赋值给一个哈希来实现这一点。Listing12_04 处理的数据显示了在过去几个世纪中大气中 CO₂（以百万分率 PPM 计）的增加情况。该程序涉及向函数传递包含大气数据的哈希。函数从参数数组中检索数据，将其重新转换回哈希，然后使用哈希查找操作按年份以表格形式打印数据。

```perl
#Listing12_04
#Passing a hash to a function

#1 Set up data on CO2 in the atmosphere
%CO2Changes = ("1750", "180",
		"1970", "320",
		"1980", "330",
		"2000", "360",
		"2025", "450");

#2 Pass arguments for the table heading
makeTableHeading("Year",
		"CO2 Parts Per Million",
		"Rise In Atmospheric Carbon Dioxide");

#4 Pass the hash to a function
makeTable(%CO2Changes);

#==============================================================
#3
#-------- Definition of makeTableHeading() --------
#makeTableHeading(col head 1, col head 2, table title)
sub makeTableHeading{
	#4 Formatting elements for the table
	$NL = "\n ";
	$DC = sprintf("%c", 247); #cast using sprintf to make a special character
	$TW = 50; #Table width
	$DL = sprintf( "%50s", $NL . $DC x $TW); #top and bottom lines
	$COLAHEAD = $_[0];
	$COLBHEAD = $_[1];
	print "$NL $_[2] $NL";
	printf("$DL $NL");
	printf("$NL %-15s %-40s $NL ", $COLAHEAD , $COLBHEAD);
	printf("$DL $NL" );
}

#5-------- Definition of makeTable() --------
#makeTable(hash for table)
sub makeTable{
	$NL = "\n ";
	%LocalCO2 = @_;               #Assign argument array to hash
	@CO2Years = keys(%LocalCO2);  #extract keys for sorting
	@CO2Years = sort {$a<=>$b}(@CO2Years);  #perform the sort
	#Use the sorted years (array) to extract the values (hash)
	foreach $Year (@CO2Years){                       #access the argument array here
	    printf("$NL %-15s %-40s $NL", $Year, $LocalCO2{$Year});
	}
}
```

在 Listing12_04 中由注释 #1 标识的行中，你建立了一个哈希（%CO2Changes），其中列出了过去几个世纪的日期和 CO₂ 浓度。在定义哈希之后，在注释 #2 处，你调用了 makeTableHeading() 函数并向其提供了三个参数。如图 12.11 所示，这些参数用于命名表格，并提供 Year 和 CO₂ 百万分率作为列标题。

在与注释 #4 相关的行中，你将 %CO2Changes 传递给 makeTable() 函数。你以隐式形式向函数提供哈希。在程序的下半部分，在注释 #5 处，你通过将参数数组赋值给本地哈希标识符 %LocalCO2 来从参数数组中检索哈希。赋值操作会自动将哈希中的元素转换为键值对。

在定义了本地哈希之后，你使用 keys() 函数将本地哈希中的年份（键）赋给一个本地数组（@CO2Years）。在定义该数组的下一行，你使用 Perl sort() 函数的数值形式对年份进行排序。然后进入一个 foreach 重复语句，在其中使用 @CO2Years 中已排序的年份来访问 %LocalCO2 哈希中的元素。为此，你使用了哈希查找操作。当你使用排序后的数组从哈希中检索值（CO₂ 浓度）时，年份会按升序在表格中排列。如图 12.11 所示，CO₂ 浓度也随年份推移而增长。请注意，2025 年的数据是预测值。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_338_0.png)

### 返回值的函数

你可以通过两种方式从函数返回值。一种方式是使用关键字 `return`，后跟要返回的参数。另一种方法是让函数返回其最后一个活动语句的结果。Listing12_05 处理英亩到公顷的转换。生态学家以支持消费水平所需的公顷数来衡量人口的生态足迹。Listing12_05 生成一个表格，其中一列显示英亩数，另一列显示公顷数。定义并调用一个将英亩转换为公顷的函数，演示了 `return` 关键字的使用。另一方面，对这样一个函数的定义和调用——该函数返回一个字符串，用于标识函数所包含信息的来源——则演示了如何隐式返回函数中最后一条语句的结果。

```perl
#Listing12_05
#Passing and returning a value
#1 Footprints for US in acres
   %Footprints = ("Fossil/Nuclear Power",  14.5,
      "Built-up Areas",     0.9,
      "Growing Crops",      3.7,
      "Grazing Animals",    0.8,
      "Harvesting Fish and Sea Food", 0.8);
#Source of information
@FPInfoSource = ("Source: M. Wackernagel, C. Monfreda, D. Deumling",
   "\"Ecological Footprint of Nations.\" November, 2002.",
   "Redefining Progress www.redefiningprogress.org.");
#2 Pass arguments for the table heading
makeTableHeading("Footprint Type",
   "Acres",
   "Hectares",
   "Ecological Footprints for the US");
#4 Pass the hash to a function
makeTable(%Footprints);
#8 Cascading functions: print calls to printTableNote
# See #9 - printTableNote returns implicitly
print(formatTableNote(@FPInfoSource));

###############################################################################
#3 --------- Definition of makeTableHeading() ------------
#makeTableHeading(col head 1, col head 2, col head 3, table title)
sub makeTableHeading(){
	#4 Formatting elements for the table
	$NL = "\n ";
	$DC = sprintf("%c", 254); #cast using sprintf to make a special character
	$TW = 52; #Table width
	$DL = sprintf( "%52s", $NL . $DC x $TW); #top and bottom lines
	$COLAHEAD = $_[0];
	$COLBHEAD = $_[1];
	$COLCHEAD = $_[2];
	print "$NL $_[3] $NL";
	printf("$DL $NL");
	printf("$NL %-30s %-10s %-10s $NL ", $COLAHEAD , $COLBHEAD, $COLCHEAD );
	printf("$DL $NL" );
}

#5 --------- Definition of makeTable() ------------
#makeTable(hash for table)
sub makeTable(){
	$NL = "\n ";
	%LocalFP = @_; #Assign argument array to hash
	@FPAcres = keys(%LocalFP); #extract keys for sorting
	#Use the sorted years (array) to extract the values (hash)
	foreach $Acres (@FPAcres){ #access the argument array here
		printf("$NL %-30s %-10.2f %-10.4f $NL ",
			$Acres,
			$LocalFP{$Acres},
			convertAcreToHectare($LocalFP{$Acres})
		);
	}#end foreach
}#end makeTable

#7 --------- Definition of convertAcreToHectare() ------------
#convertAcreToHectare(hash for table)
```

