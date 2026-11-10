
- `[drive:][path]filename` 指定要删除的文件。使用通配符可指定多个文件。
- `/P` 在删除每个文件之前提示确认

### 示例

- 1. `del test.tmp` 如果文件存在，则删除用户当前所在目录中的 test.tmp 文件。
- 2. `del c:\windows\test.tmp` 如果文件存在，则删除 windows 目录中的 test.tmp 文件。
- 3. `del c:\windows\temp\?est.tmp` ? 是代表单个字母的单个通配字符。此命令将删除子目录 'temp' 中任何以 est.tmp 结尾的文件，例如 pest.tmp 或 zest.tmp。

## 删除目录

RD 命令用于删除 MSDOS 中的空目录。要删除包含文件或目录的目录，用户必须使用 deltree 命令；或者，如果用户运行的是 Microsoft Windows 2000 或 Windows XP，则必须使用 /S 选项。

此命令的语法为：

```text
RMDIR [drive:]path\directory name
RD [drive:]path\directory name
```

Windows 2000 和 Windows XP 中删除目录命令的语法：

```text
RMDIR [/S] [/Q] [drive:]path\directory name
RD [/S] [/Q] [drive:]path\directory name
```

- `/S` 除目录本身外，还删除指定目录中的所有目录和文件。用于删除目录树。
- `/Q` 安静模式；使用 /S 删除目录树时不再询问是否确认。

### 示例

- 1. `rmdir c:\test` 如果 test 目录为空，则删除该目录。如果用户希望删除非空目录，则必须使用 deltree 命令。
- 2. `rmdir c:\test /s` Windows 2000 和 Windows XP 用户可以使用此选项，在提示确认后永久删除 test 目录、所有子目录和文件。

## 重命名文件

REN 命令用于重命名文件和目录。

在较早版本的 MSDOS 中，不使用 ren 或 rename，而是使用 move 命令来重命名 MSDOS 目录或文件。重命名文件/目录或多个文件/目录的语法如下：

```text
RENAME [drive:]\[path]\[directoryname1] filename1 filename2
REN [drive:]\[path]\[directoryname1] filename1 filename2
```

请注意，用户不能为目标指定新的驱动器或路径。

### 示例

要将目录 chope 重命名为 hope，语法如下：

```text
rename c:\chope hope
```

## 移动文件

此命令允许用户将文件或目录从一个文件夹移动到另一个文件夹，或从一个驱动器移动到另一个驱动器。

用于移动文件以及重命名文件和目录的命令语法如下：

- (a) 移动一个或多个文件：

    ```text
    MOVE [/Y | /-Y] [drive:][path]\filename1 destination
    ```

- (b) 重命名目录：

    ```text
    MOVE [/Y | /-Y] [drive:][path]\dirname1 dirname2
    ```

- `[drive:][path]\filename1` 指定用户要移动的文件的位置和名称
- `destination` 指定文件的新位置。destination 可以由驱动器号和冒号、目录名或它们的组合组成。如果用户只移动一个文件，并希望在移动时重命名该文件，则还可以包含文件名
- `[drive:][path]\dirname1` 指定用户要重命名的目录
- `dirname2` 指定目录的新名称
- `/Y` 取消确认是否覆盖现有目标文件的提示
- `/-Y` 提示确认用户是否要覆盖现有目标文件

开关 /Y 可能存在于 COPYCMD 环境变量中。可以在命令行中使用 /-Y 覆盖它。默认情况下，在覆盖时会提示，除非 MOVE 命令是从批处理脚本中执行的。

### 示例

`move c:\windows\temp\*.* c:\temp` 这将把 c:\windows\temp 中的文件移动到根目录下的 temp 目录中，当然，前提是该目录存在。

## PROMPT 命令

此命令用于更改计算机的命令提示符。

```text
C:\> PROMPT <new prompt>
```

```text
ONE | TWO
```

一个管道中可以根据用户需要包含任意多个命令。例如，考虑

```text
ONE | TWO | THREE | FOUR | FIVE
```

管道开头、中间和结尾的命令之间存在明显差异。除非出现异常情况，管道中的第一个命令通常会生成数据。中间的命令会处理数据并将其传递下去。这类命令称为过滤器。管道中的最后一个命令可以是数据消费者和过滤器。如果是这样，它会将最终结果传递给 DOS 的标准设备，结果会显示在屏幕上。

### 示例

```text
TREE | MORE
DIR | SORT
TYPE A.TXT | SORT
```

## ATTRIB 命令

在 DOS 文件中，通常有三个属性用于保护文件免受非法用户或命令的影响。此命令可以控制文件的只读、存档和隐藏属性设置。

```text
ATTRIB settings filename
```

这些设置可以是 +H 或 -H、+A 或 -A、+R 或 -R，用于打开或关闭隐藏、存档和只读属性。如果未指定任何设置，此命令将列出文件并显示当前属性设置情况。

## PATH 命令

path 这个术语已经介绍过。它表示特定文件或目录的位置。要搜索特定文件，必须指明该文件的确切路径。但对于程序来说，path 还描述了一个路径列表，DOS 应在其中搜索命令程序文件。

通常，搜索总是从当前目录开始。如果在那里找不到程序文件，就会显示错误消息。因此，path 是一个设置扩展程序搜索路径的命令。也就是说，如果在当前目录中找不到程序文件，搜索会按照 PATH 命令指定的位置继续。当输入以下命令时

```text
C:\> PATH
```

将显示当前路径设置。如果要更改路径设置，则使用以下命令：

```text
C:\> PATH = C:\; C:\DOS; C:\FPD26
```

也就是说，该命令行给出了程序文件或可执行文件所在的所有目录名。每个目录名之间用分号 (;) 分隔。以下命令会停用并终止扩展程序搜索：

```text
C:\> PATH;
```

## TREE 命令

磁盘可以从根目录分出许多子目录。TREE 命令显示任意磁盘目录树的所有分支列表，也就是说，它显示树中所有分支之间的连接关系。此类命令的写法如下：

```text
C:\> TREE
```

## SORT 命令

此命令用于按列对特定文件进行排序。

```text
C:\> SORT <filename>
```

要按相反顺序对文件排序，请在 SORT 命令后使用 /R，如下所示：

```text
C:\> SORT /R <filename>
```

## FIND 命令

FIND 是一个用于在文件中搜索特定文本的命令。该命令如下：

```text
C:\> FIND "string" <filename> [/C | /I]
```

上述命令显示所有包含双引号内指定单词的行。最常用的选项是 /C 和 /I。

### 示例

- 1. `FIND "dos" sample.txt /C`。此命令报告 sample.txt 中包含字符串 "dos" 的总行数。
- 2. `FIND "rccit" sample.dat /I`。此命令在文件 sample.dat 中搜索字符串 "rccit" 时忽略字母大小写。

## DISKCOPY 命令

此命令用于从一个软盘读取所有格式和数据，并将其复制到另一个软盘，在此过程中生成原盘的完全相同的副本。

```text
C:\> DISKCOPY <source drive> <target drive>
```

DISKCOPY 命令有一些主要缺点。它不允许软盘上存在坏区。如果任一软盘有不可用的坏区，DISKCOPY 将无法正常工作。另一方面，COPY 命令是复制数据的首选方式，在这种情况下可以正常工作。COPY 可以提高软盘空间利用率，而 DISKCOPY 不能。DISKCOPY 会清除目标软盘上的所有内容，而 copy 会将新文件与软盘上的旧文件合并。

## DOSKEY 命令

此命令用于在内存中创建缓冲区，以存储执行该命令后给出的所有命令。此类命令的写法如下：

```text
C:\> DOSKEY
```

执行上述命令后，如果给出以下命令：

```text
C:\> CD 1YEAR\XYZ
C:\> TYPE ABC.TXT
```

计算机会按顺序将所有命令存储在缓冲区中。要检索之前给出的命令，只需连续按向上箭头键，直到找到目标命令。
