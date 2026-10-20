
// Fig. 17.3: FileDemonstration.java
// File class used to obtain file and directory information.
import java.io.File;
import java.util.Scanner;

public class FileDemonstration
{
    public static void main( String[] args )
    {
        Scanner input = new Scanner( System.in );

        System.out.print( "Enter file or directory name: " );
        analyzePath( input.nextLine() );
    } // end main

    // display information about file user specifies
    public static void analyzePath( String path )
    {
        // create File object based on user input
        File name = new File( path );

        if ( name.exists() ) // if name exists, output information about it
        {
            // display file (or directory) information
            System.out.printf(
                "%s\n%s\n%s\n%s\n%s\n%s\n%s\n%s",
                name.getName(), " exists",
                ( name.isFile() ? "is a file" : "is not a file" ),
                ( name.isDirectory() ? "is a directory" :
                "is not a directory" ),
                ( name.isAbsolute() ? "is absolute path" :
                "is not absolute path" ), "Last modified: ",
                name.lastModified(), "Length: ", name.length(),
                "Path: ", name.getPath(), "Absolute path: ",
                name.getAbsolutePath(), "Parent: ", name.getParent() );

            if ( name.isDirectory() ) // output directory listing
            {
                String[] directory = name.list();
                System.out.println( "\n\nDirectory contents:\n" );

                for ( String directoryName : directory )
                    System.out.println( directoryName );
            } // end if
        } // end outer if
        else // not file or directory, output error message
        {
            System.out.printf( "%s %s", path, "does not exist." );
        } // end else
    } // end method analyzePath
} // end class FileDemonstration

Enter file or directory name: E:\Program Files\Java\jdk1.6.0_11\demo\jfc
jfc exists
is not a file
is a directory
is absolute path
Last modified: 1228404395024
Length: 4096
Path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc
Absolute path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc
Parent: E:\Program Files\Java\jdk1.6.0_11\demo\jfc

Directory contents:
CodePointIM
FileChooserDemo
Font2DTest
Java2D
Laffy
Metalworks
Notepad
SampleTree
Stylepad
SwingApplet
SwingSet
SwingSet2
SwingSet3

Enter file or directory name: C:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D\README.txt
README.txt exists
is not a directory
is not a file
is absolute path
Last modified: 1228404384270
Length: 7518
Path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D\README.txt
Absolute path: E:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D\README.txt
Parent: E:\Program Files\Java\jdk1.6.0_11\demo\jfc\Java2D

## 图 17.3 | 用于获取文件和目录信息的 File 类。（第 2 部分，共 2 部分。）

（作为文件或作为目录）在磁盘上。如果名称不存在，控制流转到第 46–49 行并向屏幕显示一条消息，其中包含用户键入的名称，后跟“does not exist.”。否则，if 语句（第 22–45 行）执行。程序输出文件或目录的名称（第 27 行），随后是使用 isFile（第 28 行）、isDirectory（第 29 行）和 isAbsolute（第 31 行）测试 File 对象的结果。接下来，程序显示 lastModified（第 33 行）、length（第 33 行）、getPath（第 34 行）、getAbsolutePath（第 35 行）和 getParent（第 35 行）返回的值。如果 File 对象表示一个目录（第 37 行），程序通过使用 File 方法 list（第 39 行）以字符串数组的形式获取目录的内容列表，并在屏幕上显示该列表。

该程序的第一个输出演示了与 JDK 中的 jfc 目录关联的 File 对象。第二个输出演示了与随 JDK 提供的 Java 2D 示例中的 README.txt 文件关联的 File 对象。在这两种情况下，我们都在计算机上指定了绝对路径。

分隔符字符用于在路径中分隔目录和文件。在 Windows 计算机上，分隔符字符是反斜杠（\）。在 UNIX 系统上，它是正斜杠（/）。Java 在路径名中对这两个字符进行相同的处理。例如，如果我们使用路径

```
c:\Program Files\Java\jdk1.6.0_11\demo\jfc
```

它采用每种分隔符字符，Java 仍会正确处理该路径。在构建表示路径信息的字符串时，使用 File.separator 来获取本地计算机的正确分隔符字符，而不是显式使用 / 或 \。该常量返回一个字符串，由一个字符组成——系统的正确分隔符。

## 17.1 编程常见错误

在字符串字面量中使用 \ 作为目录分隔符而不是 \\ 是逻辑错误。单个 \ 表示 \ 后跟下一个字符表示转义序列。使用 \\ 在字符串字面量中插入 \。

## 17.4 顺序访问文本文件

接下来，我们创建和操作顺序访问文件，其中记录按记录键字段的顺序存储。我们从文本文件开始，使读者能够快速创建和编辑人类可读的文件。我们讨论创建顺序访问文本文件、向其写入数据、从中读取数据以及更新数据。我们还包括一个信用查询程序，该程序从文件中检索特定数据。

### 17.4.1 创建顺序访问文本文件

Java 对文件不施加任何结构——诸如记录之类的概念并不存在于 Java 语言中。因此，您必须根据应用程序的要求对文件进行结构化。在下面的示例中，我们看到如何对文件施加键控记录结构。

图 17.4、17.5 和 17.8 中的程序创建了一个简单的顺序访问文件，该文件可能用于应收账款系统中，以跟踪公司应收其信用客户的金额。对于每个客户，程序从用户那里获取账号、客户姓名和余额（即客户欠公司的商品和服务金额）。每个客户的数据构成该客户的“记录”。该应用程序使用账号作为记录键——文件将按账号顺序创建和维护。程序假定用户按账号顺序输入记录。在基于顺序访问文件的综合应收账款系统中，将提供排序功能，以便用户可以按任意顺序输入记录。然后对记录进行排序并写入文件。

### 类 AccountRecord

类 AccountRecord（图 17.4）封装了本章示例中使用的客户记录信息。AccountRecord 声明在包 com.deitel.ch17（第 3 行）中，以便可以导入到本章的多个示例中以便重用。（第 8.14 节提供了有关编译和使用您自己的包的信息。）类 AccountRecord 包含私有实例变量 account、firstName、lastName 和 balance（第 7–10 行）以及用于访问这些字段的 set 和 get 方法。尽管在本示例中 set 方法不验证数据，但在“工业级”系统中应执行验证。

// Fig. 17.4: AccountRecord.java
// AccountRecord class maintains information for one account.
package com.deitel.ch17; // packaged for reuse

public class AccountRecord
{
    private int account;
    private String firstName;
    private String lastName;
    private double balance;

    // no-argument constructor calls other constructor with default values
    public AccountRecord()
    {
        this( 0, "", "", 0.0 ); // call four-argument constructor
    } // end no-argument AccountRecord constructor

    // initialize a record
    public AccountRecord( int acct, String first, String last, double bal )
    {
        setAccount( acct );
        setFirstName( first );
        setLastName( last );
        setBalance( bal );
    } // end four-argument AccountRecord constructor

    // set account number
    public void setAccount( int acct )
    {
        account = acct;
    } // end method setAccount

    // get account number
    public int getAccount()
    {
        return account;
    } // end method getAccount

    // set first name
    public void setFirstName( String first )
    {
        firstName = first;
    } // end method setFirstName

    // get first name
    public String getFirstName()
    {
        return firstName;
    } // end method getFirstName

