

## 第29章：C# 2010 中的文件处理

现在，让我们创建一个名为 CompressingFile 的应用程序（可在 CD-ROM 上获得），并执行以下步骤来压缩文件：

- 1. 添加一个 Label 控件、两个 Button 控件、一个 TextBox 控件、一个 OpenFileDialog 控件和一个 SaveFileDialog 控件。
- 2. 将 Label 控件的 Text 属性更改为 Path of the file to compress:，并将 Button 控件的 Text 属性分别更改为 Browse 和 Compress File，如图 29:30 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1453_0.png)

3. 打开 CompressingFile 应用程序的 Form1.cs 文件并用清单 29.11 所示的代码替换现有代码：

### 清单 29.11：显示 CompressingFile 应用程序的 Form1.cs 文件的代码

```
```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.IO;
using System.IO.Compression;

namespace CompressingFile
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
    }

    private void button1_Click(object sender, EventArgs e)
    {
        if (openFileDialog1.ShowDialog() == DialogResult.OK)
        {
            textBox1.Text = openFileDialog1.FileName;
        }
    }

    private void button2_Click(object sender, EventArgs e)
    {
        if (saveFileDialog1.ShowDialog() == DialogResult.OK)
        {
            // Note: code in image transcription is incomplete at this point
        }
    }
}
```
```

```
byte[] bufferwrite;
FileStream fsSource;
FileStream fsDest;
GZipStream gzCompressed;
fsSource = new FileStream(textBox1.Text, FileMode.Open, FileAccess.Read, FileShare.Read);
bufferwrite = new byte[fsSource.Length];
fsSource.Read(bufferwrite, 0, bufferwrite.Length);
fsDest = new FileStream(saveFileDialog1.FileName, FileMode.OpenOrCreate, FileAccess.Write);
gzCompressed = new GZipStream(fsDest, CompressionMode.Compress, true);
gzCompressed.Write(bufferwrite, 0, bufferwrite.Length);
fsSource.Close();
gzCompressed.Close();
fsDest.Close();
}
}
```

4. 按 F5 键运行应用程序并单击 Browse 按钮。打开对话框出现，如图 29.31 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1454_0.png)

图 29.31：显示打开对话框

5. 从打开对话框中选择要压缩的文件并单击打开按钮（图 29.31）。在我们的例子中，我们选择了 File.txt 文件。所选文件的路径出现在 Path of the file to compress 文本框中，如图 29.32 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1454_1.png)

图 29.32：显示压缩文件的路径

6. 单击 Compress File 按钮以压缩文件。保存对话框出现，如图 29.33 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1455_0.png)

图 29.33：显示另存为对话框

7. 指定文件的名称和位置，然后单击保存按钮（图 29.33）。

压缩文件后，让我们学习如何解压缩它们。为此，创建一个名为 DecompressingFiles 的应用程序（也可在 CD-ROM 上获得）并执行以下步骤：

- 1. 在 Form1 上添加一个 Label 控件、两个 Button 控件、一个 TextBox 控件、一个 OpenFileDialog 控件和一个 SaveFileDialog 控件。
- 2. 将 Label 控件的 Text 属性更改为 Select file to decompress，并将 Button 控件的 Text 属性分别更改为 Browse 和 Decompress File，如图 29.34 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1455_1.png)

图 29.34：显示 DecompressingFiles 应用程序的设计视图

- 3. 打开 DecompressingFiles 应用程序的 Form1.cs 文件并用清单 29.12 所示的代码替换现有代码：

### 清单 29.12：显示 DecompressingFiles 应用程序的 Form1.cs 文件的代码

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.IO;
using System.IO.Compression;

namespace DecompressingFiles
```

```
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            if (openFileDialog1.ShowDialog() == DialogResult.OK)
            {
                textBox1.Text = openFileDialog1.FileName;
            }
        }

        private void button2_Click(object sender, EventArgs e)
        {
            if (saveFileDialog1.ShowDialog() == DialogResult.OK)
            {
                byte[] bufferwrite;
                FileStream fsSource;
                FileStream fsDest;
                GZipStream gzDecompressed;
                fsSource = new FileStream(textBox1.Text, FileMode.Open, FileAccess.Read, FileShare.Read);
                gzDecompressed = new GZipStream(fsSource, CompressionMode.Decompress, true);
                bufferwrite = new byte[4];
                fsSource.Position = (int)fsSource.Length - 4;
                fsSource.Read(bufferwrite, 0, 4);
                fsSource.Position = 0;
                int bufferLength = BitConverter.ToInt32(bufferwrite, 0);
                byte[] buffer = new byte[bufferLength + 100];
                int readoffset = 0;
                int totalBytes = 0;
                while (true)
                {
                    int bytesRead = gzDecompressed.Read(buffer, readoffset, 100);
                    if (bytesRead == 0)
                        break;
                    readoffset += bytesRead;
                    totalBytes += bytesRead;
                }
                fsDest = new FileStream(saveFileDialog1.FileName, FileMode.Create);
                fsDest.Write(buffer, 0, totalBytes);
                fsSource.Close();
                gzDecompressed.Close();
                fsDest.Close();
            }
        }
    }
}
```

- 4. 按 F5 键运行应用程序并单击 Browse 按钮以打开打开对话框。
- 5. 从打开对话框中选择压缩文件并单击打开按钮，如图 29.35 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1457_0.png)

图 29.35：显示打开对话框

6. 现在，单击 Form1 表单上的 Decompress File 按钮，其结果是另存为对话框出现，如图 29.36 所示：

![](img/e073a4882197be4ab61103cbe0bcb394_1457_1.png)

图 29.36：显示另存为对话框

7. 在另存为对话框的文件名组合框中指定文件的名称，以便您可以在指定位置轻松找到文件的解压缩形式。在本例中，我们指定了 DecompressedFile（图 29.36）。

8. 单击保存按钮以将文件以 DecompressedFile 的名称保存在所需位置。现在，让我们总结本章讨论的主要主题。

## 摘要

在本章中，您学习了 System.IO 命名空间及其类。接下来，您学习了如何处理目录和文件。此外，您还学习了如何检查目录是否存在、创建、重命名和删除目录。您还了解到文件 I/O 操作涉及检查文件属性；并执行其他操作，例如创建、读取、写入、重命名和复制文件。最后，您学习了如何压缩和解压缩文件。

在下一章中，您将学习如何使用可扩展标记语言（XML）和 .NET。

## 30

## 使用 XML 和 .NET 工作

![](img/e073a4882197be4ab61103cbe0bcb394_1458_0.png)

| 如果您需要立即解决以下问题： | 请参见页码： |
|---|---|
| 使用流式 XML | 1425 |
| 在 .NET 中实现 DOM | 1432 |
| 导航和转换数据 | 1435 |
| 转换 ADO.NET 和 XML 数据 | 1438 |
| 使用 XML 实现对象序列化 | 1442 |

