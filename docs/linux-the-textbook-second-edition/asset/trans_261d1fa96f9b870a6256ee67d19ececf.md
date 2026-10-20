

## 数组

数组可以在声明时使用以下语法进行初始化

```
array_name=(value1 ... valueN)
```

其中 "value1" 的形式为 [subscript]=string。请注意，下标是可选的，但如果提供，则对应的值将被分配给给定的数组槽；否则，分配给该值的数组槽为上一个分配的槽加一。

你可以使用 ${name[subscript]} 语法引用数组项。此过程称为数组索引。如果 "subscript" 为 @ 或 *，则引用所有数组元素。@ 和 * 之间的区别在于 "${name[*]}" 展开为包含数组 name 所有元素的单个词，而 "${name[@]}" 将数组 name 的每个元素展开为单独的词。

在下面的示例中，数组变量 movies 被分配了三个值；前两个值被分配到位置 0 和 1，第三个被分配到槽号 65。echo 命令用于显示这三个变量的值。

```
$ movies=("Silence of the Lambs" "Malcolm X" [65]="The Birds")
$ echo ${movies[0]}
Silence of the Lambs
$ echo ${movies[1]}
Malcolm X
$ echo ${movies[2]}

$ echo ${movies[65]}
The Birds
$ echo ${movies[*]}
Silence of the Lambs Malcolm X The Birds
$ echo ${movies[@]}
Silence of the Lambs Malcolm X The Birds
$
```

readonly 命令配合 -a 选项可用于声明只读数组变量。在下面的会话中，us_presidents 数组被初始化为三个项目。echo 命令用于显示该数组的第一个、第四十个、第四十四和第四十五个元素。声明 Fibonacci 数组的命令失败，因为 local 命令只能用于在函数范围内声明变量。声明 Fibonacci 的 declare 命令是成功的。

```
$ readonly -a us_presidents=([1]="George Washington" [40]="Ronald Reagan" "Bush" [42]="Bill Clinton" [44]="Barack Obama" "Donald Trump")
$ echo ${us_presidents[1]}
George Washington
$ echo ${us_presidents[40]}
Ronald Reagan
$ echo ${us_presidents[44]}
Barack Obama
$ echo ${us_presidents[45]}
Donald Trump
$ local -a Fibonacci=(0 1 1 2 3 5 8 13 21 34)
-bash: local: can only be used in a function
$ declare -a Fibonacci=(0 1 1 2 3 5 8 13 21 34)
$ echo ${Fibonacci[7]}
13
$
```

数组项的大小（以字节为单位）可以使用 ${#name[subscript]} 语法显示。如果未使用下标，则显示第一个数组元素大小。如果 * 用作下标，则显示数组元素的数量。在下面的会话中，我们显示 movies 数组中各项的大小。两个赋值语句中的第一个用于在槽 16 处向数组插入新项（"Forrest Gump"），第二个赋值语句用于将槽 65 中的当前值（"The Birds"）替换为新值（"Sleepless in Seattle"）。图 13.1 显示了在进行这些更改前后 movies 数组。

|  | Before movies |  | After movies |
|---|---|---|---|
| movies[0]: | Silence of the Lambs | movies[0]: | Silence of the Lambs |
| movies[1]: | Malcolm X | movies[1]: | Malcolm X |
| ... | ... | ... | ... |
| movies[16]: |  | movies[16]: | Forrest Gump |
| ... | ... | ... | ... |
| movies[65]: | The Birds | movies[65]: | Sleepless in Seattle |

FIGURE 13.1 The movies array before and after changing its contents.

```
$ echo ${#movies}
20
$ echo ${#movies[65]}
9
$ echo ${#movies[*]}
3
$ movies[16]="Forrest Gump"
$ movies[65]="Sleepless in Seattle"
$ echo ${#movies[*]}
4
$ echo ${movies[0]}; echo ${movies[1]}; echo ${movies[16]}; echo ${movies[65]}
Silence of the Lambs
Malcolm X
Forrest Gump
Sleepless in Seattle
$
```

到现在应该很明显，任何使用赋值语句被赋予多个值的 shell 变量都将成为数组变量。因此，当变量被赋值为命令的多词输出时，它会成为数组变量，并将输出的每个字段包含在单独的数组槽中。在下面的示例中，files 是一个数组变量，其元素是当前目录中所有文件的名称。numfiles 变量包含当前目录中文件的数量。文件数量也可以使用 echo ${#files[*]} 命令显示，如图所示。echo ${files[*]} 命令显示当前目录中所有文件的名称，而 echo ${files[2]} 命令显示第三个元素（即槽号为 2 的元素）。

```
$ files=`ls` numfiles=`ls | wc -w`
$ echo ${files[*]}
addall canleave countup debug_demo dext dext_functions diff2 exec.demo1 find_sys_const fs heredoc_demo trap_demo
$ echo $numfiles
12
$ echo ${#files[*]}
12
$ echo ${files[2]}
countup
$
```

在下面的示例中，num_array_demo 文件包含一个脚本，该脚本使用名为 Fibonacci 的整数数组，计算数组中整数的和，并在屏幕上显示该和。此示例中的 Fibonacci 数组包含斐波那契数列的前十个数。对于不熟悉斐波那契数列的人来说，前两个数是 0 和 1，之后的数由前两个数相加得到。数学上，该数列表示如下。

F₁ = 0
F₂ = 1
Fₙ = Fₙ₋₁ + Fₙ₋₂, for n ≥ 3

因此，斐波那契数列的前十个数为 0、1、1、2、3、5、8、13、21 和 34。

num_array_demo 文件中的脚本记录良好且相当容易理解。它显示前十个斐波那契数的和。代码后的示例运行如下。

```
$ cat num_array_demo
# File Name:
# Author:
# Date Written:
# Last Modified:
# Purpose:
# Brief Description:
#!/bin/bash -xv
# Initialize Fibonacci array to any number of Fibonacci numbers; first 15
# in this case.
declare -a Fibonacci=(0 1 1 2 3 5 8 13 21 34 55 89 144 233 377)
size=${#Fibonacci[@]}
index=1
sum=0
next=0
while [ $index -le $size ]
do
  next=${Fibonacci[$index]}
  sum=$((sum + next))
  index=$((index + 1))
done
echo "The sum of first ${#Fibonacci[@]} Fibonacci numbers is $((sum))."
exit 0
$ ./num_array_demo
The sum of first 15 Fibonacci numbers is 986.
```

### 练习

- 编写一个 Bash 脚本，包含两个数值数组 array1 和 array2，分别初始化为集合 {1, 2, 3, 4, 5} 和 {1, 4, 9, 16, 25} 中的值。脚本应生成并显示一个数组，其元素为两个数组对应元素的和。因此，结果数组的第一个元素为 1 + 1 = 2，第二个为 2 + 4 = 6，以此类推。
- 在你的系统上复制本节讨论的所有 Bash 会话和脚本，以验证它们是否产生预期结果。

## Here Documents

Bash 的 here document 功能允许你在脚本中将命令的标准输入重定向并将其附加到脚本内的数据中，以特定格式包装，如下所述。显然，此功能适用于从标准输入获取输入的命令。该功能主要用于显示菜单，尽管此功能还有一些其他重要用途。维护数据在脚本内的优势在于消除了如果数据保存在单独文件中所需的额外文件操作，如打开和读取。结果是程序运行速度更快。以下是 here document 的简要描述。

### 语法

```
command << [-] input_marker
... input data ...
input_marker
```

### 目的

以 here document 的数据作为输入来执行 command —— 数据位于输入开始和结束标记 input_marker 之间

input_marker 是你选择的用于包装 command 输入数据的字符串。结束标记必须单独占一行，并且不能被任何空格包围。命令和变量替换在 here document 数据被定向到 command 的 stdin 之前执行。可以使用引号防止这些替换或在 here document 中包含任何引号。input_marker 可以用引号括起来以防止整个文档中的任何替换，如

```
command <<'Marker'
...
Marker
```

<< 后面的连字符 (-) 可用于删除 here document 中各行中的前导制表符（不是空格）以及结束 here document 的标记。此功能允许 here document 和分隔标记符合脚本的缩进。下面的会话说明了这一点：

```
while [ ... ]
do
    grep ... <<- DIRECTORY
        John Doe ...
        ...
        Art Pohm ...
    DIRECTORY
    ...
done
```

最后一个但非常重要的一点：使用 here document 的命令的输出和错误重定向必须在命令行中指定，而不是在结束 here document 的标记之后。同样，将命令的标准输出通过管道与其他命令连接也是如此，如下面的会话所示。请注意，grep ... <<- DIRECTORY 2> errorfile | sort 命令可以用 (grep ... 2> errorfile | sort) <<- DIRECTORY 替换。

```
while [ ... ]
do
    grep ... <<- DIRECTORY 2> errorfile | sort
        John Doe ...
        ...
        Art Pohm ...
    DIRECTORY
    ...
done
```

我们可以用一个简单的将 cat 命令的 stdin 从 here document 重定向的实例来说明 here document 功能的使用。heredoc_demo 文件中的脚本用于向用户显示一条消息，然后向作为命令行参数传递的收件人发送一条消息。在下面的会话中，我们使用了两个 here documents：一个以 << DataTag 开始并以 DataTag 结束；另一个以 << WRAPPER 开始并以 WRAPPER 结束。请注意，在使用此脚本之前必须安装 Linux mail 实用程序。

```
$ cat heredoc_demo
#!/bin/bash

cat << DataTag
This is a simple use of the here document. This data is the
input to the cat command.
```

