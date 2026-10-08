

# 第 17 章 文件与流

107-119

```cs
catch (SerializationException)
{
    MessageBox.Show("写入文件错误", "错误",
    MessageBoxButtons.OK, MessageBoxIcon.Error);
}
catch (FormatException)
{
    MessageBox.Show("格式无效", "错误",
    MessageBoxButtons.OK, MessageBoxIcon.Error);
}
ClearTextBoxes(); // 清空 TextBox 的值
// exitButtonClick 的处理程序
private void exitButton_Click(object sender, EventArgs e) {
    // 关闭文件
    try {
        output?.Close(); // 关闭 FileStream
    } catch (IOException) {
        MessageBox.Show("无法关闭文件", "错误",
        MessageBoxButtons.OK, MessageBoxIcon.Error);
    }
    Application.Exit();
}
```

图 17.9 使用序列化创建顺序访问文件。（第 3/3 部分）

该程序假设输入的数据是正确的，并且按照记录编号顺序排列的。`enterButton` 方法（第 73–120 行）执行写入操作。第 92–95 行创建并初始化了一个 `RecordSerializable` 对象。第 98 行调用 `Serialize` 将 `RecordSerializable` 对象写入输出流。`Serialize` 方法将 `FileStream` 对象作为第一个参数，以便 `BinaryFormatter` 将其第二个参数写入正确的文件。该程序未指定如何格式化对象以进行输出——因此会发生 `SerializationException`。如果在序列化过程中发生问题，在示例（图 17.9）中，我们输入了五个账户——与图 17.5 相同。程序没有显示数据记录在文件中的形式。请记住，我们现在正在使用二进制文件，这些文件不是人类可读的。为了验证文件是否成功创建，下一节将展示一个读取文件内容的程序。

## 17.8 从二进制文件中读取和反序列化数据

前一节展示了如何使用对象序列化创建顺序访问文件。在本节中，我们将讨论如何从文件中顺序读取反序列化对象。

图 17.10 读取并显示由图 17.9 程序创建的 `clients.ser` 的内容。示例截图与图 17.6 相同，因此此处不再显示。第 15 行创建了用于读取对象的 `BinaryFormatter`。程序通过创建 `FileStream` 对象来打开文件进行输入（第 51–52 行）。文件名被指定为 `FileStream` 构造函数的第一个参数。程序在 `nextButtonClick_Click` 处理程序（第 61–93 行）中从文件中读取对象。我们使用 `Deserialize`（使用第 15 行创建的 `BinaryFormatter`）来读取数据（第 67 行开始）。注意，由于 `Deserialize` 转换为 `RecordSerializable` 类型返回的是 `object` 类型的引用，我们必须执行此类型转换以访问属于 `Serializable` 类的属性。如果在反序列化过程中发生错误或到达文件末尾，将抛出 `SerializationException` 并关闭 `FileStream` 对象（第 83 行）。

```cs
// 图 17.10: ReadSequentialAccessFile.cs
// 使用反序列化读取顺序访问文件。
using System;
using System.Windows.Forms;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;
using System.Runtime.Serialization;
using BankLibrary;

namespace ReadSequentialAccessFile
{
    public class ReadSequentialAccessFileForm : BankUIForm
    {
        // 以二进制格式反序列化 RecordSerializable
        private BinaryFormatter reader = new BinaryFormatter();
        private FileStream input; // 用于从文件读取的流

        // 无参数构造函数
        public ReadSequentialAccessFile()
        {
            InitializeComponent();
        }

        // 用户点击 Open 时调用
        private void openButtonClick(object sender, EventArgs e)
        {
            // 创建并显示对话框，允许用户打开文件
            DialogResult result;
            string fileName;

            using (OpenFileDialog fileChooser = new OpenFileDialog())
            {
                result = fileChooser.ShowDialog();
                // 如果用户点击了 "OK"
                if (result == DialogResult.OK)
                {
                    // 确保文件名不为空
                    if (!string.IsNullOrEmpty(fileChooser.FileName))
                    {
                        // 获取读取权限的 FileStream
                        input = new FileStream(fileChooser.FileName, FileMode.Open, FileAccess.Read);
                        openButton.Enabled = false; // 禁用 按钮
                        nextButton.Enabled = true; // 启用 按钮
                    }
                }
                else
                {
                    // 显示无效的文件名
                    MessageBox.Show("无效的文件名", "错误", MessageBoxButtons.OK, MessageBoxIcon.Error);
                }
            }
        }

        // 用户点击 Next 时调用
        private void nextButton_Click(object sender, EventArgs e)
        {
            // 反序列化数据
            try
            {
                // 获取文件中的 RecordSerializable
                record = (RecordSerializable)reader.Deserialize(input);
                // 存储数据的字符串数组
                var values = new string[] {
                    record.Account(),
                    record.FirstName(),
                    record.LastName(),
                    record.Balance()
                };
                // 将 values 设置到 TextBox
                SetTextBoxValues(values);
            }
            catch (SerializationException)
            {
                // 关闭 FileStream
                input?.Close();
                openButton.Enabled = true; // 启用 按钮
                nextButton.Enabled = false; // 禁用 按钮
            }
            ClearTextBoxs();
        }

        private RecordSerializable record;
    }
}
```

图 17.10 | 使用反序列化读取顺序访问文件。（第 1/3 部分）

## 17.9 File 和 Directory 类

文件组织在目录（也称为文件夹）中。`File` 和 `Directory` 类允许程序管理文件和目录。`File` 类可以确定有关文件的信息，并用于打开文件。我们在之前的节中讨论了读写文件的技术。

图 17.11 列出了 `File` 的所有操作文件和确定信息的静态方法。我们在图 17.13 中演示了这些这些方法。

| 方法 | 说明 |
| --- | --- |
| AppendText | 返回一个向现有文件追加文本的 StreamWriter，如果不存在则创建。 |
| Copy | 将文件复制到新建。 |
| Create | 创建文件并返回其关联的 FileStream。 |
| CreateText | 创建文本文件并返回其关联的 StreamWriter。 |
| Delete | 删除指定的文件。 |
| Exists | 如果指定的文件存在则返回 true，否则返回 false。 |
| GetCreationTime | 返回文件/目录创建时间的 DateTime 对象。 |
| GetLastAccessTime | 返回文件/目录上次访问时间的 DateTime 对象。 |
| GetLastWriteTime | 返回文件/目录最后修改时间的 DateTime 对象。 |
| Move | 将指定的文件移动到指定位置。 |
| Open | 返回与指定文件关联并具有指定读取/写入权限的 FileStream。 |
| OpenRead | 返回与指定文件关联的只读 FileStream。 |
| OpenText | 返回与指定文件关联的 StreamReader。 |
| OpenWrite | 返回与指定文件关联的写写 FileStream。 |

图 17.11 | File 类静态方法（部分列表）。

`Directory` 提供了操作目录的能力。图 17.12 列出了 `Directory` 类的一些用于目录操作的静态方法。图 17.13 也演示了这些方法中的几种。方法返回的 `DirectoryInfo` 对象

