

File 类可以表示文件或目录。创建文件有多种方式：

- File(URI uri)
- File(String pathname)
- File(String parent, String child)
- File(File parent, String child)

File 类中的大多数方法都不言自明，既然此时我们只需进行介绍，遍历文件树就是一个很好的示例。参见图 9.1。

![](img/588a4cda8f2acae94a7e1987bf99400d_244_0.png)

图 9.1 目录树。

FilesAndDirectories 示例位于 javagames.filesandres 包中，它会遍历硬盘上的目录并显示每个文件和文件夹的信息。main() 方法调用 runTest() 方法，后者包含遍历文件树的代码。runTest() 方法首先为硬盘上的每个文件夹创建一个新的文件对象，然后调用 displayInfo() 方法，该方法将文件信息打印到控制台，并递归遍历剩余文件。

以下方法用于收集每个文件的信息：

- canExecute()—文件是否可执行
- canRead()—文件是否可读
- canWrite()—文件是否可写
- isHidden()—是否为隐藏文件
- isDirectory()—如果是目录则为 true，如果是文件则为 false
- lastModified()—上次修改的日期和时间
- length()—文件的大小（字节）
- getName()—文件名

还有其他方法可用。有关更多信息，请参阅 Java 文档。

StringBuilder 类用于格式化文件信息。lastModified 值被封装在 Date() 类中，并使用 SimpleDateFormat() 进行格式化。length 被转换为千字节，并使用 DecimalFormat() 类格式化以包含逗号。最后，读、写和执行文件属性被追加到末尾。

在将文件信息打印到屏幕后，listFiles() 方法用于显示任何子文件夹的所有信息。FilesAndDirectories 代码如下：

```java
package javagames.filesandres;

import java.io.File;
import java.text.DecimalFormat;
import java.text.SimpleDateFormat;
import java.util.Date;

public class FilesAndDirectories {
    public FilesAndDirectories() {
    }

    public void runTest() {
        // list files and folders
        String dir = "C:\\temp";
        File file = new File( dir );
        displayInfo( 0, file );
    }

    private void displayInfo( int depth, File file ) {
        // Name, Date, Size, Attr
        boolean executable = file.canExecute();
        boolean readable = file.canRead();
        boolean writable = file.canWrite();
        boolean hidden = file.isHidden();
        boolean directory = file.isDirectory();
        long lastModified = file.lastModified();
        long length = file.length();
        String name = file.getName();
        // create ASCII file structure
        StringBuilder buf = new StringBuilder();
        for (int i = 0; i < depth; ++i) {
            buf.append("    ");
        }
        if (directory) {
            buf.append(" + ");
        }
        if (name.isEmpty()) {
            buf.append(" . ");
        } else {
            buf.append(name);
        }
        // add modification date
        buf.append("\t\t*");
        Date date = new Date(lastModified);
        buf.append(new SimpleDateFormat().format(date));
        buf.append("\t\t");
        // add file size in kilobytes
        long kb = length / 1024;
        DecimalFormat format = new DecimalFormat();
        format.setGroupingUsed(true);
        buf.append(format.format(kb));
        buf.append(" KB");
        // add read, write, execute attribute flags
        buf.append("\t\t*");
        if (hidden) buf.append("-");
        if (readable) buf.append("R");
        if (writable) buf.append("W");
        if (executable) buf.append("X");
        // print everything to the command line
        System.out.println(buf.toString());
        File[] children = file.listFiles();
        if (children != null) {
            for (File child : children) {
                displayInfo(depth + 1, child);
            }
        }
    }
    public static void main(String[] args) {
        new FilesAndDirectories().runTest();
    }
}
```

## 了解输入/输出流

在 Java 的世界中，`InputStream` 是用于处理多种数据源的接口。`InputStream` 可以是文件、数组、网络套接字和外部设备。以下列出了可用于创建不同资源的不同输入源。

- Properties: `InputStream`, `Reader`
- Images: `File`, `InputStream`, `ImageInputStream`, `URL`
- Audio: `InputStream`
- XML: `InputStream`, `Reader`, `File`, `InputSource`

虽然有不同种类的类可用于读取和写入数据，但 `InputStream` 是所有人都可用的唯一类。即使使用 `Class` 和 `ClassLoader` 访问类路径资源也会使用 `InputStream`。

由于所有这些类都依赖于 `InputStream`，使用它应该很容易。但是，由于许多早期 Java API 相关的异常处理模式，使用 `InputStream` 可能会很繁琐且容易出错。

因为流在使用后应始终关闭，即使发生错误也是如此，基本模式如下：

```
InputStream in = null;
try {
  in = [make new stream]
  while ([has more data]) {
    [process data]
  }
} catch (IOException ex) {
  [handle error or rethrow]
} finally {
  try {
    in.close();
  } catch (Exception ex) { }
}
```

不仅创建和读取 `InputStream` 有必须捕获的异常，关闭流也是如此。

`read()` 方法返回一个整数，因此请记住将其强制转换为正确的数据类型。当 `read()` 方法返回 -1 时，表示没有更多数据可用。读取字符串使用 `Reader` 接口，它包装了 `InputStream`。模式相同，区别在于不返回单个字节，而是每个 `readLine()` 方法返回一行文本。

示例代码从 lorem-ipsum.txt 文件读取，该文件包含以下文本：

Lorem ipsum dolor sit amet, consectetuer adipiscing elit,
sed do eiusmod tempor incididunt ut labore et dolore magna
aliqua. Ut enim ad minim veniam, quis nostrud exercitation
ullamco laboris nisi ut aliquip ex ea commodo consequat.
Duis aute irure dolor in reprehenderit in voluptate velit
esse cillum dolore eu fugiat nulla pariatur. Excepteur sint
occaecat cupidatat non proident, sunt in culpa qui officia
deserunt mollit anim id est laborum.

ReadingDataFromFiles 代码位于 javagames.filesandres 包中，是从文件读取字节和字符串的一个小示例。

```java
package javagames.filesandres;

import java.io.*;

public class ReadingDataFromFiles {
    public void runTest() {
        String path = "./res/assets/text/lorem-ipsum.txt";
        File file = new File( path );
        readInBytes( file );
        readInStrings( file );
    }

    public void readInBytes( File file ) {
        System.out.println();
        System.out.println();
        System.out.println( "****************************" );
        System.out.println( "Reading in bytes" );
        System.out.println();
        InputStream in = null;
        try {
            in = new FileInputStream( file );
            int next = -1;
            while ((next = in.read()) != -1) {
                System.out.print( (char)next );
            }
        } catch ( IOException ex ) {
            ex.printStackTrace();
        } finally {
            try {
                in.close();
            } catch ( IOException ex ) { }
        }
    }

    public void readInStrings( File file ) {
        System.out.println();
        System.out.println();
        System.out.println( "**************************" );
        System.out.println( "Reading in strings" );
        System.out.println();
        Reader reader = null;
        try {
            reader = new FileReader( file );
            BufferedReader buf = new BufferedReader( reader );
            String line = null;
            while ( ( line = buf.readLine() ) != null ) {
                System.out.println( line );
            }
        } catch ( IOException ex ) {
            ex.printStackTrace();
        } finally {
            try {
                reader.close();
            } catch ( IOException ex ) { }
        }
    }

    public static void main( String[] args ) {
        new ReadingDataFromFiles().runTest();
    }
}
```

使用 OutputStream 类写入文件与使用 InputStream 类似。模式如下：

```
OutputStream out = null;
try {
out = [open output stream]
[ write data ]
} catch ( FileNotFoundException fex ) {
[ handle error ]
} catch ( IOException ioex ) {
[ handle error ]
} finally {
```

