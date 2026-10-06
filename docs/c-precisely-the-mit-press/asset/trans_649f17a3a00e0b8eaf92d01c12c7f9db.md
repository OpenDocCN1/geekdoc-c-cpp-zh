

## 25.7.2 来自字节数组的输入和输出：MemoryStream

MemoryStream 是一种从内存中的字节数组读取或向其写入的流（Stream）。内存流有一个容量（capacity），表示流中的最大字节数，以及一个长度（length），表示流中当前的字节数。容量在创建流时设置，除非流是可调整大小的，否则无法更改。MemoryStream 类具有以下构造函数：

- MemoryStream() 创建一个容量为 0 的可调整大小 MemoryStream，支持读取、写入和寻址。
- MemoryStream(int n) 创建一个容量为 n 的可调整大小 MemoryStream，支持读取、写入和寻址。如果 n<0，则抛出 ArgumentOutOfRangeException。
- MemoryStream(byte b[]) 创建一个容量为 b.Length 的不可调整大小 MemoryStream，支持读取、写入和寻址。如果 b 为空，则抛出 ArgumentNullException。
- MemoryStream(byte b, bool wr) 工作原理类似，但如果 wr 为 true，则支持写入。
- MemoryStream(byte b, int i, int n) 创建基于 b[i..i+n-1] 创建一个容量为 n 的不可调整大小 MemoryStream，支持读取、写入和寻址。如果 i<0 或 n<0，则抛出 ArgumentNullException；如果 i+n>b.Length，则抛出 ArgumentException。
- MemoryStream(byte b, int i, int n, bool wr) 工作原理类似，但如果 wr 为 true，则支持写入。

MemoryStream 与 Stream 类 (25.7) 相同的成员，此外这些成员（其中 ms 是 MemoryStream 类型的变量）：

- SetLength(n)，其中 n 的类型为 length，将 ms 的长度设置为 n。如果 n<ms.Length，流将被截断，且当前位置设置为流中最后一个字节之后。如果 n>ms.Capacity，ms 的容量将增加，流中的新字节将初始化为 0。如果 ms 不可调整大小或 ms 不写入，则抛出 NotSupportedException。如果 n<0，则抛出 ArgumentOutOfRangeException。
- 只读属性 ms.Capacity 类型为 int，表示流的容量。将容量设置为 n，如果 ms 不可扩展或已关闭，则抛出 NotSupportedException；如果 n!=ms.Length，则抛出 ArgumentOutOfRangeException。
- ToArray() 类型为 byte[]，无论流当前位置如何，都会将内容写入新的字节数组。
- WriteTo(st)，其中 st 是 Stream 类型的表达式，将内容写入流 st 或关闭 ms 关闭。如果 st 为空，则抛出 ArgumentNullException；如果 ms 已关闭，则抛出 ObjectDisposedException。

## 25.8 目录

Directory 和 DirectoryInfo 类实现了操作目录的方法。Directory 类提供了静态方法，DirectoryInfo 类提供了类似的方法。每次调用 Directory 方法都会产生安全检查，而 DirectoryInfo 实例可以为 null 以节省某些检查。

- Directory.GetCurrentDirectory() 类型为 String，返回工作目录的字符串表示。
- DirectoryInfo(String path) 创建一个关联路径名称的新 DirectoryInfo 对象。如果目录不存在，则抛出 DirectoryNotFoundException。

假设 d 是 DirectoryInfo 类型的变量：

- d.Name 类型为 String，是 d 的名称。
- d.Parent 类型为 DirectoryInfo，是 d 的父目录，如果 d 是根目录，则为 null。
- d.GetDirectories() 类型为 DirectoryInfo[]，返回 d 的子目录。
- d.GetFiles() 类型为 FileInfo[]，返回 d 中的文件。

## 25.9 文件

FileInfo 对象表示一个文件，即文件系统中的文件名。文件名可能表示一个文件，也可能什么都不表示（如果没有该文件或路径）。即使文件名表示一个文件，给程序也可能有读取或写入该文件的权限，或者读取通往文件路径上的目录。这些是 FileInfo 类中的少数构造函数和方法：

- FileInfo(String name) 创建与路径名对应的文件名，路径可以是相对或绝对的。如果 name 为空字符串或格式无效，抛出 ArgumentException；如果 name 为空，则抛出 ArgumentNullException；如果名称或长度过长，抛出 PathTooLongException；如果调用者没有权限，则抛出 UnauthorizedAccessException 或 SecurityException。
- 只读属性 Ex，如果存在此文件名的文件则为 true；否则为 false。
- 只读属性 Name 和 FullName 类型为 String，是文件名及其完整路径。
- 只读属性 Extension 类型为 String，是文件的扩展名，包括开头的点（.），如果没有扩展名，则为空字符串。
- 只读属性 Length 类型为 long，是文件按字节计算的长度。
- FileStream Create() 创建一个新文件并返回与其关联的 FileStream。
- void Delete() 如果文件存在则删除文件；否则什么都不做。
- FileStream OpenRead() 创建与文件关联的用于读取的 FileStream。
- FileStream OpenWrite() 创建与文件关联的用于写入的 FileStream。
- StreamReader OpenText() 创建与文件关联的用于读取的 StreamReader。
- StreamWriter AppendText() 创建一个用于追加文本的 StreamWriter。
- StreamWriter CreateText() 创建一个新文件并返回一个用于从中写入的 StreamWriter。

## 示例 194 读取并打印目录层次

调用 ShowDir(0, dir) 将打印目录 dir 的名称，递归地调用自己打印 dir 的所有子目录，然后打印 dir 中所有文件的名称。由于每次递归调用都会增加缩进，因此布局反映了目录结构。

```c
using System.IO;
// Directory, DirectoryInfo, FileInfo
public class DirectoryHierarchy {
    public static void ShowDir(int indent, DirectoryInfo dir) {
        Indent(indent); Console.WriteLine(dir.Name);
        DirectoryInfo[] subdirs = dir.GetDirectories();
        foreach (DirectoryInfo d in subdirs) {
            ShowDir(indent + 4, d);
            FileInfo[] files = d.GetFiles();
            foreach (FileInfo file in files) {
                Indent(indent + 4); Console.WriteLine(file.Name);
            }
        }
    }

    public static void Main() {
        DirectoryInfo dir = new DirectoryInfo(Directory.GetCurrentDirectory());
        ShowDir(0, dir);
    }
}
```

## 示例 195 文件名、路径和文件信息

路径可以是相对或绝对形式给出。无论主机操作系统如何，路径都可以以 Windows 式（使用反斜杠）或 Unix 式（使用正斜杠）给出。

```csharp
// Windows
FileInfo file = new FileInfo("example");
```

## 25.10 网络通信

一对不同的进程可以通过套接字（sockets）进行通信。进程可能在同一台机器上，也可能在网络连接的不同机器上。

套接字通常用于客户端/服务器架构，服务器进程创建一个监听连接的服务器套接字。当客户端连接到服务器套接字时，服务器端创建一个新的套接字并连接到客户端。套接字连接用于客户端和服务器之间的双向通信；两端都可以获取一个可写可读的流。

以下是 System.Net.Sockets 命名空间中类的构造函数和方法：

- Socket(AddressFamily af, SocketType st, ProtocolType pt) 创建指定类型的服务器套接字。
- void Listen(int queue) 将套接字转换为监听模式。
- void Accept(EndPoint ep) 监听连接，直到连接建立。建立时创建一个新的 Socket。如果套接字不在监听模式，则抛出 SocketException。
- void Bind(EndPoint ep) 将套接字绑定到给定的端点 ep（网络地址和端口号），可以是 IPPoint 表达式（示例 196）。
- void Close() 关闭套接字。
- 只读属性 RemoteEndPoint 返回套接字连接的远程端点。
- int Send(byte[] b) 和 int Receive(byte[] b) 用于向套接字发送数据和从套接字接收数据。

虽然可以使用使用套接字进行通信，但通常最好是将套接字封装在 NetworkStream 中，并以二进制或字符格式进行通信。

NetworkStream 类（来自 System.Net.Sockets）是抽象类 Stream 的子类；它进一步包含以下构造函数和属性：

- NetworkStream(Socket s) 创建一个与套接字 s 关联的新流。
- 只读属性 DataAvailable 表示流中是否有数据可读。

