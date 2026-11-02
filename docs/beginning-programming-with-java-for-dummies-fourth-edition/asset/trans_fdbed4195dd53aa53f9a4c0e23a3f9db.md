
## 从文件读取
所有 Scanner 方法都可以从现有的磁盘文件读取。例如，要从名为 mySpeech 的文件读取一个单词，可使用如下代码：

```
Scanner diskScanner =
    new Scanner(new File("mySpeech"));

String oneWord = diskScanner.next();
```

要从名为 letters.dat 的文件读取一个字符然后在屏幕上显示该字符，可以这样做：

```
Scanner diskScanner =
    new Scanner(new File("letters.dat"));

System.out.println(
    diskScanner.findWithinHorizon(".",0).charAt(0));
```

![](img/6d9dcff12e52b997f3ad31445b712549_283_0.png)

注意我从名为 mySpeech 的文件读取，而不是 mySpeech.txt 或 mySpeech.doc。放在点号之后的内容称为文件名扩展名，对于包含数字和其他数据的完整文件，文件名扩展名是可选的。当然，Java 程序必须命名为 something.java，但数据文件可以命名为 mySpeech.txt、mySpeech.reallymine.allmine，或仅 mySpeech。只要你在 new File 调用中使用的名称与计算机硬盘上的文件名相同，一切就没问题。

## 向文件写入
print 和 println 方法可以向磁盘文件写入。以下是一些示例：

在 Listing 13-2 代码的运行期间，变量 total 存储数字 99.75。要将 99.75 存入 cookedData.txt 文件，你执行

```
diskWriter.println(total);
```

此 println 调用之所以写入磁盘文件，是因为 Listing 13-2 中的以下行：

```
PrintStream diskWriter =
    new PrintStream("cookedData.txt");
```

在程序的另一个版本中，你可能决定不使用 total 变量。要将 99.75 写入 cookedData.txt 文件，你可以调用

```
diskWriter.println(unitPrice * quantity);
```

✔ 要在屏幕上显示 OK，你可以进行以下方法调用：

```
System.out.print ("OK");
```

要将 OK 写入名为 approval.txt 的文件，可以使用以下代码：

```
PrintStream diskWriter =
    new PrintStream("approval.txt");

diskWriter.print ("OK");
```

✔ 你可能决定将 OK 作为两个独立字符写入。要写入屏幕，可以进行以下调用：

```
System.out.print ('O');
System.out.print ('K');
```

而要将 OK 写入 approval.txt 文件，可以使用以下代码：

```
PrintStream diskWriter =
    new PrintStream("approval.txt");

diskWriter.print ('O');
diskWriter.print ('K');
```

✔ 与 System.out 的对应方法类似，磁盘写入的 print 和 println 方法在换行行为上有所不同。例如，你想在屏幕上显示以下文本：

```
Hankees  Socks
7        3
```

为此，你可以进行以下方法调用：

```
System.out.print ("Hankees  ");
System.out.println ("Socks");
System.out.print (7);
System.out.print ("        ");
System.out.println (3);
```

要将相同文本写入名为 scores.dat 的文件，可以使用以下代码：

```
PrintStream diskWriter =
    new PrintStream("scores.dat");

diskWriter.print ("Hankees  ");
diskWriter.println ("Socks");
diskWriter.print (7);
diskWriter.print ("        ");
diskWriter.println (3);
```

## 为文件命名
如果包含数据的文件不在你的程序项目文件夹中怎么办？如果是这样，当你调用 `new File` 时，文件名必须包含文件夹名称。例如，在 Windows 中，你的 `TallyBudget.java` 程序可能位于你的 `c:\Users\MyUserName\workspace\13-09` 文件夹中，而名为 `totals` 的文件可能位于名为 `c:\advertisements` 的文件夹中。（参见下图。）

![](img/6d9dcff12e52b997f3ad31445b712549_285_0.png)

然后，要引用 `totals` 文件，你需要包含文件夹名称、文件名，以及（为安全起见）驱动器号：

```
Scanner diskScanner = new Scanner
    (new File("c:\\advertisements\\totals"));
```

注意我使用双反斜杠来分隔驱动器号、文件夹名称和文件名。要了解原因，请查看第 12 章中标题为“Escapism”的侧边栏。字符串 `"c:\totals"` 中的单个反斜杠代表一个制表符，后跟 `otals`。但在此示例中，文件名为 `totals`，而不是 `otals`。使用单个反斜杠，名称 `c:\advertisements\totals` 将无法正确工作。

在引号内，你使用双反斜杠来表示通常的单个反斜杠。因此字符串 `"c:\\advertisements\\totals"` 代表 `c:\advertisements\totals`。这很好，因为 `c:\advertisements\totals` 是你在 Windows 中通常引用文件的方式。

如果你想避开所有这些反斜杠的困惑，可以使用正斜杠来指定每个文件的位置。Windows 对 `new File("c:/advertisements/totals")` 和 `new File("c:\\advertisements\\totals")` 的响应完全相同。而如果你使用 UNIX、Linux 或 Macintosh，双反斜杠的胡闹就不适用于你。只需写

```
Scanner diskScanner =
    new Scanner (new File(
    "/Users/me/advertisements/totals"));
```

或类似的内容，反映你的系统目录结构。

## 写入、重写和再重写
考虑到我的顽皮，我做了一个小实验。我问自己如果多次运行同一个写文件程序会发生什么。所以我创建了一个微型程序（Listing 13-5 中的程序），并运行了两次。然后我检查了程序的输出文件。输出文件（如图 13-8 所示）只包含两个字母。

### Listing 13-5：一个小实验
```
import java.io.File;
import java.io.FileNotFoundException;
import java.io.PrintStream;

class WriteOK {
    public static void main(String args[])
    throws FileNotFoundException {
        PrintStream diskWriter =
            new PrintStream(new File("approval.txt"));
        diskWriter.print  ('O');
        diskWriter.println('K');
        diskWriter.close();
    }
}
```

![](img/6d9dcff12e52b997f3ad31445b712549_286_0.png)

以下是实验从开始到结束的事件序列：

- 1. **在运行 Listing 13-5 中的代码之前，我计算机的硬盘上没有 `approval.txt` 文件。**

没关系。每个实验都必须从某个地方开始。

### 2. 我运行 Listing 13-5 中的代码。
Listing 13-5 中对 new PrintStream 的调用创建了一个名为 approval.txt 的文件。最初，新的 approval.txt 文件不包含任何字符。稍后在 Listing 13-5 中，对 print 和 println 的调用将字符放入文件中。因此，运行代码后，approval.txt 文件包含两个字母：字母 OK。

### 3. 我第二次运行 Listing 13-5 中的代码。
此时，我可能会想象 approval.txt 文件中会出现 OKOK。但图 13-8 中显示的并非如此。运行代码两次后，approval.txt 文件只包含一个 OK。原因如下：

- Listing 13-5 中对 new PrintStream 的调用会删除我现有的 approval.txt 文件。该调用创建了一个新的、空的 approval.txt 文件。
- 创建新的 approval.txt 文件后，print 方法调用将字母 O 放入新文件中。
- println 方法调用将字母 K 添加到同一个 approval.txt 文件中。

所以故事就是这样。每次运行程序时，它都会销毁硬盘上已有的 approval.txt 文件。然后程序向新创建的 approval.txt 文件添加数据。

## 第 14 章
### 在循环内创建循环
### 本章内容
- ► 分析循环策略
- ► 诊断循环问题
- ► 创建嵌套循环

如果你是 Wiley Publishing 的编辑，请不要阅读接下来的几段。在接下来的几段中，我泄露了一个重要的商业秘密（这是你真的不希望我做的事）。

我即将描述一个写畅销 For Dummies 书籍的万无一失流程。流程如下：

写几个词组成一个句子。多次重复以创建一段落。

```
Repeat the following to form a paragraph:
    Repeat the following to form a sentence:
        Write a word.
```

多次重复之前的说明以制作一个章节。制作多个章节然后制作多个章节。

```
Repeat the following to form a best-selling book
in the For Dummies series:
    Repeat the following to form a chapter:
        Repeat the following to form a section:
            Repeat the following to form a paragraph:
                Repeat the following to form a sentence:
                    Write a word.
```

这个过程涉及循环套循环套循环套循环套循环。它就像一个语言上的 M.C. Escher 版画。它有用，还是无聊？
