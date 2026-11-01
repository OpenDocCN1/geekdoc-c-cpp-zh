

```csharp
using System;
using System.IO;
using System.Windows.Forms;

namespace DriveViewer
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            DriveInfo[] di = DriveInfo.GetDrives();

            foreach (DriveInfo itemDrive in di)
            {
                listBox1.Items.Add(itemDrive.Name);
            }
        }

        private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
        {
            DriveInfo di = new DriveInfo(listBox1.SelectedItem.ToString());

            MessageBox.Show("Available Free Space: " + di.AvailableFreeSpace + "\n" +
                "Drive Format: " + di.DriveFormat + "\n" +
                "Drive Type: " + di.DriveType + "\n" +
                "Is Ready: " + di.IsReady + "\n" +
                "Name: " + di.Name + "\n" +
                "Root Directory: " + di.RootDirectory + "\n" +
                "ToString() Value: " + di + "\n" +
                "Total Free Space: " + di.TotalFreeSpace + "\n" +
                "Total Size: " + di.TotalSize + "\n" +
                "Volume Label: " + di.VolumeLabel, di.Name + " DRIVE INFO");
        }
    }
}
```

代码下载 DriveViewer.sln

第一步是使用 using 关键字引入 System.IO 命名空间。在 Form1_Load 事件中，使用 DriveInfo 类获取系统上所有可用驱动器的列表。具体做法是使用 DriveInfo 对象数组，并通过 DriveInfo.GetDrives() 方法填充该数组。然后使用 foreach 循环，遍历找到的每个驱动器，并将结果显示在列表框中。运行结果类似于图 29-14 所示。

该窗体允许最终用户选择列表中的一个驱动器。选择驱动器后，将出现一个消息框，其中包含有关该驱动器的详细信息。如图 29-14 所示，我当前的计算机上有六个驱动器。选择其中几个驱动器后，将生成图 29-15 中汇总显示的消息框。

![](img/d7d2ffa0a76feaab821930e95daace93_862_0.png)

图 29-14

![](img/d7d2ffa0a76feaab821930e95daace93_863_0.png)

图 29-15

从这里可以看到，这些消息框提供了三种完全不同驱动器的详细信息。第一个驱动器 `C:\` 是我的硬盘，因为消息框显示其驱动器类型为 Fixed（固定）。第二个驱动器 `D:\` 是我的 CD/DVD 驱动器。第三个驱动器 `F:\` 是我的 USB 闪存盘，其驱动器类型为 Removable（可移动）。

## 文件安全性

最初引入 .NET Framework 1.0/1.1 时，它没有提供一种简便的方法来访问和处理文件、目录和注册表键的访问控制列表（ACL）。在当时，要完成此类工作通常需要借助 COM 互操作，因此还需要具备更高级的 ACL 编程知识。

随着 .NET Framework 2.0 的发布，这种情况发生了显著变化。它通过 System.Security.AccessControl 命名空间，使得处理 ACL 的过程变得容易得多。使用该命名空间，现在可以操作文件、注册表键、网络共享、Active Directory 对象等的安全设置。

### 从文件读取 ACL

作为 System.Security.AccessControl 的使用示例，本节将介绍如何操作文件和目录的 ACL。首先介绍如何查看特定文件的 ACL。此示例在控制台应用程序中完成，如下所示：

```csharp
using System;
using System.IO;
using System.Security.AccessControl;
using System.Security.Principal;

namespace ReadingACLs
{
    internal class Program
    {
        private static string myFilePath;

        private static void Main()
        {
            Console.Write("Provide full file path: ");
            myFilePath = Console.ReadLine();

            try
            {
                using (FileStream myFile =
                    new FileStream(myFilePath, FileMode.Open, FileAccess.Read))
                {
                    FileSecurity fileSec = myFile.GetAccessControl();
                    foreach (FileSystemAccessRule fileRule in
                        fileSec.GetAccessRules(true, true,
                            typeof(NTAccount)))
                    {
                        Console.WriteLine("{0} {1} {2} access for {3}",
                            myFilePath,
                            fileRule.AccessControlType ==
                            AccessControlType.Allow
                            ? "provides" : "denies",
                            fileRule.FileSystemRights,
                            fileRule.IdentityReference);
                    }
                }
            }
            catch
            {
                Console.WriteLine("Incorrect file path given!");
            }
            Console.ReadLine();
        }
    }
}
```

代码下载 ReadingACLs.sln

要使此示例正常工作，第一步是引用 System.Security.AccessControl 命名空间。这将使你在后续程序中能够使用 FileSecurity 和 FileSystemAccessRule 类。

在检索到指定文件并将其放入 FileStream 对象后，使用 File 对象上的 GetAccessControl() 方法获取该文件的 ACL。然后，从 GetAccessControl() 方法获取的信息被放入 FileSecurity 类中。该类包含对被引用项的访问权限。每个单独的访问权限随后由 FileSystemAccessRule 对象表示。因此，使用 foreach 循环遍历创建的 FileSecurity 对象中找到的所有访问权限。

使用根目录中的一个简单文本文件运行此示例，将产生类似下面的结果：

```
Provide full file path: C:\Sample.txt
C:\Sample.txt provides FullControl access for BUILTIN\Administrators
C:\Sample.txt provides FullControl access for NT AUTHORITY\SYSTEM
C:\Sample.txt provides ReadAndExecute, Synchronize access for BUILTIN\Users
C:\Sample.txt provides Modify, Synchronize access for
    NT AUTHORITY\Authenticated Users
```

下一节将介绍从目录而不是文件读取 ACL。

### 从目录读取 ACL

读取目录（而不是实际文件）的 ACL 信息与前一个示例差别不大。该示例的代码如下：

```csharp
using System;
using System.IO;
using System.Security.AccessControl;
using System.Security.Principal;

namespace ConsoleApplication1
{
    internal class Program
    {
        private static string mentionedDir;

        private static void Main()
        {
            Console.Write("Provide full directory path: ");
            mentionedDir = Console.ReadLine();

            try
            {
                DirectoryInfo myDir = new DirectoryInfo(mentionedDir);

                if (myDir.Exists)
                {
                    DirectorySecurity myDirSec = myDir.GetAccessControl();

                    foreach (FileSystemAccessRule fileRule in
                        myDirSec.GetAccessRules(true, true,
                            typeof(NTAccount)))
                    {
                        Console.WriteLine("{0} {1} {2} access for {3}",
                            mentionedDir, fileRule.AccessControlType ==
                            AccessControlType.Allow
                            ? "provides" : "denies",
                            fileRule.FileSystemRights,
                            fileRule.IdentityReference);
                    }
                }
            }
            catch
            {
                Console.WriteLine("Incorrect directory provided!");
            }

            Console.ReadLine();
        }
    }
}
```

代码下载 ReadingACLsFromDirectory.sln

此示例的最大区别在于使用了 DirectoryInfo 类，该类现在也包含 GetAccessControl() 方法，用于获取目录的 ACL 信息。在 Windows 7 上运行此示例会得到以下结果：

```
Provide full directory path: C:\Test
C:\Test provides FullControl access for BUILTIN\Administrators
C:\Test provides 268435456 access for BUILTIN\Administrators
C:\Test provides FullControl access for NT AUTHORITY\SYSTEM
C:\Test provides 268435456 access for NT AUTHORITY\SYSTEM
C:\Test provides ReadAndExecute, Synchronize access for BUILTIN\Users
C:\Test provides Modify, Synchronize access for NT AUTHORITY\Authenticated Users
C:\Test provides -536805376 access for NT AUTHORITY\Authenticated Users
```

在使用 ACL 时，你将看到的最后一项内容是使用新的 System.Security.AccessControl 命名空间向文件的 ACL 添加条目或从中删除条目。

