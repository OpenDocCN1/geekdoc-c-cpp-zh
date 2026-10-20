

```
6      public static void main( String[] args )
7      {
8          CreateTextFile application = new CreateTextFile();
9
10         application.openFile();
11         application.addRecords();
12         application.closeFile();
13     } // end main
14 } // end class CreateTextFileTest
```

要终止输入，请在提示输入时键入文件结束指示符。
在 UNIX/Linux/Mac OS X 上键入 <ctrl> d 然后按 Enter
在 Windows 上键入 <ctrl> z 然后按 Enter

输入账号号码（> 0）、名字、姓氏和余额。
? 100 Bob Jones 24.98
输入账号号码（> 0）、名字、姓氏和余额。
? 200 Steve Doe -345.67
输入账号号码（> 0）、名字、姓氏和余额。
? 300 Pam White 0.00
输入账号号码（> 0）、名字、姓氏和余额。
? 400 Sam Stone -42.16
输入账号号码（> 0）、名字、姓氏和余额。
? 500 Sue Rich 224.62
输入账号号码（> 0）、名字、姓氏和余额。
? ^Z

图 17.7 | 测试 CreateTextFile 类。（第 2 部分，共 2 部分。）

| 示例数据 |  |  |  |
|---|---|---|---|
| 100 | Bob | Jones | 24.98 |
| 200 | Steve | Doe | -345.67 |
| 300 | Pam | White | 0.00 |
| 400 | Sam | Stone | -42.16 |
| 500 | Sue | Rich | 224.62 |

图 17.8 | 图 17.5–17.7 中程序的示例数据。

## 17.4.2 从顺序访问文本文件读取数据

数据存储在文件中，以便在需要时检索进行处理。第 17.4.1 节演示了如何创建顺序访问文件。本节展示如何从文本文件顺序读取数据。我们演示如何使用类 Scanner 从文件而不是键盘输入数据。

图 17.9 和 17.10 中的应用程序从第 17.4.1 节的应用程序创建的 "clients.txt" 文件中读取记录并显示记录内容。图 17.9 的第 13 行声明了一个 Scanner，将用于从文件检索输入。

// Fig. 17.9: ReadTextFile.java
// 此程序读取文本文件并显示每条记录。
import java.io.File;
import java.io.FileNotFoundException;
import java.lang.IllegalStateException;
import java.util.NoSuchElementException;
import java.util.Scanner;

import com.deitel.ch17.AccountRecord;

public class ReadTextFile
{
    private Scanner input;

    // 允许用户打开文件
    public void openFile()
    {
        try
        {
            input = new Scanner( new File( "clients.txt" ) );
        } // end try
        catch ( FileNotFoundException fileNotFoundException )
        {
            System.err.println( "Error opening file." );
            System.exit( 1 );
        } // end catch
    } // end method openFile

    // 从文件读取记录
    public void readRecords()
    {
        // 将要写入屏幕的对象
        AccountRecord record = new AccountRecord();

        System.out.printf( "% -10s%-12s%-12s%10s\n", "Account",
            "First Name", "Last Name", "Balance" );

        try // 使用 Scanner 对象从文件读取记录
        {
            while ( input.hasNext() )
            {
                record.setAccount( input.nextInt() ); // 读取账号号码
                record.setFirstName( input.next() ); // 读取名字
                record.setLastName( input.next() ); // 读取姓氏
                record.setBalance( input.nextDouble() ); // 读取余额

                // 显示记录内容
                System.out.printf( "% -10d%-12s%-12s%10.2f\n",
                    record.getAccount(), record.getFirstName(),
                    record.getLastName(), record.getBalance() );
            } // end while
        } // end try
```
53      catch ( NoSuchElementException elementException )
54      {
55          System.err.println( "File improperly formed." );
56          input.close();
57          System.exit( 1 );
58      } // end catch
59      catch ( IllegalStateException stateException )
60      {
61          System.err.println( "Error reading from file." );
62          System.exit( 1 );
63      } // end catch
64      } // end method readRecords

      // 关闭文件并终止应用程序
      public void closeFile()
      {
          if ( input != null )
              input.close(); // 关闭文件
      } // end method closeFile
  } // end class ReadTextFile

# 图 17.9 | 使用 Scanner 进行顺序文件读取。（第 2 部分，共 2 部分。）

```
1  // Fig. 17.10: ReadTextFileTest.java
2  // 测试 ReadTextFile 类。
3
4  public class ReadTextFileTest
5  {
6      public static void main( String[] args )
7      {
8          ReadTextFile application = new ReadTextFile();
9
10         application.openFile();
11         application.readRecords();
12         application.closeFile();
13     } // end main
14  } // end class ReadTextFileTest
```

| Account | First Name | Last Name | Balance |
|---|---|---|---|
| 100 | Bob | Jones | 24.98 |
| 200 | Steve | Doe | -345.67 |
| 300 | Pam | White | 0.00 |
| 400 | Sam | Stone | -42.16 |
| 500 | Sue | Rich | 224.62 |

# 图 17.10 | 测试 ReadTextFile 类。

方法 openFile（第 16–27 行）通过在第 20 行实例化一个 Scanner 对象来打开文件以供读取。我们将一个 File 对象传递给构造函数，指定 Scanner 对象将从应用程序执行所在的目录中的 "clients.txt" 文件读取。如果找不到文件，将发生 FileNotFoundException。异常在第 22–26 行处理。

方法 readRecords（第 30–64 行）从文件中读取并显示记录。第 33 行创建 AccountRecord 对象 record 以存储当前记录的信息。第 35–36 行显示应用程序输出中列的标题。第 40–51 行从文件读取数据，直到到达文件结束标记（此时，第 40 行的 hasNext 方法将返回 false）。第 42–45 行使用 Scanner 方法 nextInt、next 和 nextDouble 输入一个 int（账号号码）、两个 Strings（名字和姓氏）和一个 double 值（余额）。文件中的每条记录是一行数据。值存储在对象 record 中。如果文件中的信息格式不正确（例如，在应为余额的位置出现姓氏），在输入记录时将发生 NoSuchElementException。该异常在第 53–58 行处理。如果在输入数据之前关闭了 Scanner，将发生 IllegalStateException（在第 59–63 行处理）。如果没有发生异常，记录的信息将显示在屏幕上（第 48–50 行）。注意第 48 行的格式字符串中，账号号码、名字和姓氏左对齐，而余额右对齐并以两位精度输出。循环的每次迭代从文本文件中输入一行文本，表示一条记录。

第 67–71 行定义方法 closeFile，它关闭 Scanner。main 方法在图 17.10 的第 6–13 行定义。第 8 行创建一个 ReadTextFile 对象，然后用于打开、添加记录到并关闭文件（第 10–12 行）。

## 17.4.3 案例研究：信用查询程序

要从文件中顺序检索数据，程序从文件开头开始并连续读取所有数据，直到找到所需信息。在程序执行期间，可能需要多次（从文件开头）顺序处理文件。类 Scanner 不允许重新定位到文件开头。如果需要再次读取文件，程序必须关闭文件并重新打开它。

图 17.11–17.13 中的程序允许信用经理获取零余额客户列表（即不欠任何钱的客户）、信用余额客户列表（即公司欠钱的客户）和借方余额客户列表（即欠公司钱的客户，用于商品和服务）。信用余额为负数，借方余额为正数。

### MenuOption 枚举

我们首先创建枚举类型（图 17.11）来定义用户将拥有的不同菜单选项。选项及其值在第 7–10 行列出。方法 getValue（第 19–22 行）检索特定枚举常量的值。

```
1  // Fig. 17.11: MenuOption.java
2  // 信用查询程序选项的枚举。
3
4  public enum MenuOption
5  {
6      // 声明枚举类型的内容
7      ZERO_BALANCE( 1 ),
8      CREDIT_BALANCE( 2 ),
9      DEBIT_BALANCE( 3 ),
10     END( 4 );
```

图 17.11 | 信用查询程序菜单选项的枚举。（第 1 部分，共 2 部分。）

