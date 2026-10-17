


function name, and then a scalar. The interpreter processes the combination without problems. Still, the readability of the code is questionable.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_82_0.png)

**Figure 4.2**
你可以对函数使用不同形式的语法，并达到相同的结果。

# Changing the Cases of Strings

如前一节中 `uc()` 函数的使用所示，Perl 为你提供了允许更改字符串中字符大小写的函数。有些函数仅影响字符串的起始字符。其他函数允许你更改字符串中所有字符。本节对这些函数进行了回顾。

# Case with First Characters

如果你想将字符串的第一个字符更改为大写或小写，可以通过 `ucfirst()` 和 `lcfirst()` 函数来实现。请参考 Listing04_02：

```perl
#Listing04_02
#Changing the cases of first letters in strings
#The first letter of the writer's name remains lowercase
$NameToChange = "herman Melville";
print "\nPrior to capitalization: " . $NameToChange;

#Assign the scalar back to itself
$NameToChange = ucfirst($NameToChange);
print "\nAfter capitalization: " . $NameToChange;

#Change the first letter back to lowercase
$NameToChange = lcfirst($NameToChange);
print "\nRestored to original: " . $NameToChange;
```

# CHAPTER 4 Print Functions

在 Listing04_03 中，你首先将诗人的名字赋给标量 $NameToChange。然后，你将标量作为参数传递给 `uc()` 函数，该函数将包含诗人名字的字符串转换为大写。请注意，与之前一样，为了使转换生效，你必须将字符串重新赋给自身。`lc()` 函数将字符串转换为小写。同样，你必须将字符串重新赋给自身才能使转换生效。Figure 4.4 说明了 Listing04_03 的输出。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_84_0.png)

# Obtaining the Length of a String

要获取字符串的长度，你使用 Perl 的 `length()` 函数。与 `uc()` 和 `print()` 函数一样，`length()` 函数需要一个字符串作为参数。与这些函数不同的是，它返回的值本身不是字符串。它返回的值是一个整数，指示字符串中的字符数。Listing04_04 说明了 `length()` 函数的一些用法：

```perl
#Listing04_04
#Use the length() function

#1 Basic string
#characters in the first line: 22
#characters in the second line: 40
#white spaces are counted as characters
($PreludeLines = <<WORDW);
I should learn to love
The end of life and everything we know.
WORDW

#2.Print the lines
print("\n". "$PreludeLines" . "\n");
```

64
TEAM LinG

```perl
#3.Obtain the length and store the value in a scalar
$CharLength = length($PreludeLines);
#Then show the results
print "\nThe number of characters in the lines,".
      "\nincluding blank spaces ".
      "(from Wordsworth's \"Prelude\")is $CharLength.";

#4.You can also just print the return value
print "\nAgain, the length: ". length($PreludeLines);
```

Listing04_04 中与注释 #1 相关的行创建了一个由 William Wordsworth 的《The Prelude》中的两行组成的块。在创建块之前，注释显示了每行包含的字符数（包括空格）。你将这些行存储在标量 $PreludeLines 中。与注释 #2 相关的代码打印这些行。

在注释 #3 之后的行中，你调用 length() 函数并将 $PreludeLines 作为其参数提供给它。该函数获取行中的字符数（包括空格），并将此值返回给标量 $CharLength。在获取行的字符长度后，你打印一个插值了存储在 $CharLength 中的值的连接字符串。

在注释 #4 处，你调用 print() 函数来打印 length() 的返回值。Figure 4.5 显示了 Listing04_04 的输出。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_85_0.png)

**Figure 4.5**
使用 `length()` 函数获取包含空格的字符串长度。

# Hidden Characters and Strings

在处理字符串时，换行符常常会结束字符串。此类字符不可见，如果你想相互比较字符串，可能会产生问题。例如，eq 运算符不会将包含换行符的字符串视为与缺少换行符的另一个字符串相等，即使两个字符串中除换行符外的所有字符都相同。

# Hidden Characters in Strings

Figure 4.6 说明了 W. H. Auden 诗歌中的两行。第一组行包含隐藏字符。第二组行不包含此类字符。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_86_0.png)

**Figure 4.6**
W. H. Auden 的《Fish in the Unruffled Lakes》中的行显示了额外字符。

如果你仅根据看到的两组文本是否相等来检查 Figure 4.6 中说明的两行，则比较结果会出错。请考虑 Listing04_05：

```text
#Listing04_05
#1 Set up lines with and without hidden newline characters
$CoupleALineA= "Sighs for folly said and done\n";
$CoupleALineB= "Twist our narrow days\n";
#without
$CoupleBLineA= "Sighs for folly said and done";
$CoupleBLineB= "Twist our narrow days";

#2 Print to show visual equality but different lengths
print("\nA--A: " . $CoupleALineA . "\n");
print("\nA--B: " . $CoupleALineB . "\n");
print length($CoupleALineA);
```

```perl
print("\nA-A: ". $CoupletBLineA . "\n");
print("\nA-B: ". $CoupletBLineB . "\n");
print length($CoupletBLineA);
```

```perl
#3 Compare the lines to show the interpreter
#considers them to be different
if($CoupletALineA eq $CoupletBLineA)
{
	#Does not print since equal operator returns false
	print "\nLines are the same."
}
if($CoupletALineA ne $CoupletBLineA)
{
	#Prints since the not equal operator returns true
	print "\nLines are not the same."
}
```

在 Listing04_05 的注释 #1 中，你建立两组字符串。你在第一组中附加换行符，但在第二组中不附加。然后，你将两组字符串赋给标量。在与注释 #2 相关的行中，你打印两个对句以显示它们的视觉相似性，但你也使用 length() 函数来评估它们的长度。外观表明这些行彼此相等，但从 length() 函数的返回值中，你可以看到隐藏字符使它们不相等。在注释 #3 标识的行中，你使用选择语句和 eq 及 ne 运算符进行测试。Figure 4.7 显示了结果。选择语句表明解释器认为字符串不相等。

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_87_0.png)

**Figure 4.7**
不可见字符使字符串不相等。

# Eliminating Characters

Perl 提供了 chomp() 和 chop() 函数来消除字符串末尾的字符。chomp() 函数使用最广泛，因为它消除换行符且不删除除换行符以外的任何字符。

# Using the chomp() Function

chomp() 函数直接解决了 Figure 4.7 中说明的问题，即解释器发现两个看起来具有相同字符的字符串不相等。不相等是由于行末尾附加的隐藏字符造成的。Listing04_06 说明了 chomp() 函数的用法：

```perl
#Listing04_06

#1 Set up lines with and without hidden end-of-line characters
$CoupletALineA= "Sighs for folly said and done\n";
$CoupletALineB= "Twist our narrow days\n";

#Use Chomp to remove the hidden end-of-line characters
print "\nWith hidden EOL:" . chomp($CoupletALineA);
print "\nWith hidden EOL:" . chomp($CoupletALineB);

#without
$CoupletBLineA= "Sighs for folly said and done";
$CoupletBLineB= "Twist our narrow days";

print "\nWithout hidden EOL:" . chomp($CoupletBLineA);
print "\nWithout hidden EOL:" . chomp($CoupletBLineB);

#2 Print to show visual equality but different lengths
print "\nA-A: " . $CoupletALineA . "\n";
print "\nA-B: " . $CoupletALineB . "\n";
print length($CoupletALineA);

print "\nA-A: " . $CoupletBLineA . "\n";
print "\nA-B: " . $CoupletBLineB . "\n";
print length($CoupletBLineA);

#3 Compare the lines to show the interpreter
#considers them to be different
```


