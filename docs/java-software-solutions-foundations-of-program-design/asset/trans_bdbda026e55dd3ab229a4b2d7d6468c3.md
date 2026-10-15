
## 清单8.2（续）

```text
Enter number 5: 72.404
Enter number 6: 34.8
Enter number 7: 63.41
Enter number 8: 45.55
Enter number 9: 69.0
Enter number 10: 99.18
The numbers in reverse order:
99.18  69.0  45.55  63.41  34.8  72.404  29.06  53.5  48.9  18.36
```

清单8.3中展示的LetterCount示例使用了两个数组和一个字符串对象。名为upper的数组用于存储字符串中每个大写字母出现的次数。名为lower的数组对小写字母也起同样的作用。

由于英语字母表中有26个字母，upper和lower数组都声明为26个元素。每个元素包含一个整数，默认初始为零。for循环逐个字符地扫描字符串。字符串中每出现一个字符，相应数组中相应的计数器就会加1。

## 清单8.3

```java
//****************************************************************
//  LetterCount.java      Author: Lewis/Loftus
//
//  Demonstrates the relationship between arrays and strings.
//****************************************************************

import java.util.Scanner;

public class LetterCount
{
    //---------------------------------------------------------------
    //  Reads a sentence from the user and counts the number of
    //  uppercase and lowercase letters contained in it.
    //---------------------------------------------------------------
    public static void main (String[] args)
    {
        final int NUMCHARS = 26;

        Scanner scan = new Scanner (System.in);

        int[] upper = new int[NUMCHARS];
        int[] lower = new int[NUMCHARS];

        char current;  // the current character being processed
        int other = 0;  // counter for non-alphabetics

        System.out.println ("Enter a sentence:");
        String line = scan.nextLine();

        // Count the number of each letter occurrence
        for (int ch = 0; ch < line.length(); ch++)
        {
            current = line.charAt(ch);
            if (current >= 'A' && current <= 'Z')
                upper[current-'A']++;
            else
                if (current >= 'a' && current <= 'z')
                    lower[current-'a']++;
                else
                    other++;
        }

        // Print the results
        System.out.println ();
        for (int letter=0; letter < upper.length; letter++)
        {
            System.out.print ( (char) (letter + 'A') );
            System.out.print (":" + upper[letter]);
            System.out.print ("\t\t" + (char) (letter + 'a') );
            System.out.println (":" + lower[letter]);
        }

        System.out.println ();
        System.out.println ("Non-alphabetic characters: " + other);
    }
}
```

### 输出

```text
Enter a sentence:
In Casablanca, Humphrey Bogart never says "Play it again, Sam."
```

| 大写字母 | 大写字母计数 | 小写字母 | 小写字母计数 |
|------------------|-----------------|------------------|-----------------|
| A | 0 | a | 10 |
| B | 1 | b | 1 |
| C | 1 | c | 1 |
| D | 0 | d | 0 |
| E | 0 | e | 3 |
| F | 0 | f | 0 |
| G | 0 | g | 2 |
| H | 1 | h | 1 |
| I | 1 | i | 2 |
| J | 0 | j | 0 |
| K | 0 | k | 0 |
| L | 0 | l | 2 |
| M | 0 | m | 2 |
| N | 0 | n | 4 |
| O | 0 | o | 1 |
| P | 1 | p | 1 |
| Q | 0 | q | 0 |
| R | 0 | r | 3 |
| S | 1 | s | 3 |
| T | 0 | t | 2 |
| U | 0 | u | 1 |
| V | 0 | v | 1 |
| W | 0 | w | 0 |
| X | 0 | x | 0 |
| Y | 0 | y | 3 |
| Z | 0 | z | 0 |

非字母字符：14

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_415_0.png)

视频注释  
关于LetterCount示例的讨论。

两个计数器数组的索引范围都是0到25。我们必须将每个字符映射到一个计数器。一种合乎逻辑的做法是使用upper[0]统计找到的'A'字符数，使用upper[1]统计找到的'B'字符数，依此类推。同样，lower[0]用于计数字符'a'，lower[1]用于计数字符'b'，依此类推。另一个名为other的变量用于统计遇到的所有非字母字符。

注意，为了判断一个字符是否为大写字母，我们使用了布尔表达式(current >= 'A' && current <= 'Z')。判断小写字母时也使用了类似的表达式。我们本可以使用Character类中的静态方法isUpperCase和isLowerCase来进行这些判断，但在这个示例中我们没有使用，以便强调这样一个要点：由于字符基于Unicode字符集，它们具有特定的数值和顺序，我们可以在编程中使用这些数值和顺序。

我们使用当前字符来计算要引用的数组索引。在计算索引时，我们必须小心，确保它保持在数组边界内并与正确的元素匹配。请记住，在Unicode字符集中，大写和小写字母都是连续的，并按顺序排列（参见附录C）。因此，取一个大写字母（如'E'，其数值为69）的数值，然后减去字符'A'的数值（65），得到4，这正是字符'E'的计数器所对应的正确索引。注意，在程序中我们实际上不需要知道每个字母的具体数值。

## 另一种数组语法

从语法上讲，在Java中声明数组引用有两种方式。第一种方式（在前面的示例和本书中一直使用）是将方括号与数组中存储的值的类型关联起来。第二种方式是将方括号与数组名关联起来。因此，下面两种声明是等价的：

```java
int[] grades;
int grades[];
```

尽管就编译器而言，这两种声明方式没有区别，但第一种方式与其他类型的声明保持一致。如果将数组方括号与元素类型关联，则声明的类型是明确的，尤其是在同一行声明多个变量时。因此，在本书中我们始终将方括号与元素类型关联。

## 初始化列表

**关键概念：** 可以使用初始化列表来实例化数组对象，而不必使用new运算符。

可以使用*初始化列表*来实例化数组，并为数组元素提供初始值。本质上，这与在声明中初始化基本数据类型的变量是相同的思路，只是数组需要多个值。

初始化列表中的各项用逗号分隔，并用花括号{}括起来。使用初始化列表时，不使用new运算符。数组的大小由初始化列表中的项数决定。例如，下面的声明将数组scores实例化为一个包含八个整数的数组，索引从0到7，并具有指定的初始值：

```java
int[] scores = {87, 98, 69, 87, 65, 76, 99, 83};
```

初始化列表只能在数组首次声明时使用。

初始化列表中每个值的类型必须与数组元素的类型匹配。让我们看另一个例子：

```java
char[] vowels = {'A', 'E', 'I', 'O', 'U'};
```

在这种情况下，变量vowels被声明为包含五个字符的数组，初始化列表包含字符字面量。

清单8.4中显示的程序演示了如何使用初始化列表来实例化数组。

## 数组作为参数

**关键概念：** 整个数组可以作为参数传递，使形式参数成为原始数组的别名。

整个数组可以作为参数传递给方法。因为数组是对象，所以当整个数组作为参数传递时，传递的是原始数组引用的副本。我们在第7章讨论过这个问题，它适用于所有对象。

接收数组作为参数的方法可以永久性地更改数组中的某个元素，因为它引用的是原始元素值。但该方法不能永久性地更改对数组本身的引用，因为发送给方法的是原始引用的副本。这些规则与适用于任何对象类型的规则一致。

数组元素也可以传递给方法。如果元素类型是基本类型，则传递的是值的副本。如果元素是对对象的引用，则传递的是对象引用的副本。与往常一样，方法内部对参数所做的更改产生的影响取决于参数的类型。我们将在下一节进一步讨论对象数组。

