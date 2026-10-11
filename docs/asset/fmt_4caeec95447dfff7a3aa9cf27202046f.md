
读取此数据时会“知道”数据对应的数据类型，这样数据就可以直接读取到该类型的对象中。

在 17.6 节中，我们知道正在输入的是一个账号，接着是名和姓字符串以及一个带小数的余额。我们还知道这些值是用逗号分隔的，且每行只有一条记录。因此，我们能够解析字符串并将账号转换为 `int`，将余额转换为 `decimal`。直接读取或写入整个对象会变得更简单。序列化提供了一种称为**对象序列化**的机制。序列化对象是表示为字节序列的对象，其中包含了数据以及对象类型和所存储数据类型的信息。在将序列化对象写入文件后，可以从文件中读取它并进行反序列化——即表示对象的类型和字节，它们可以用于在内存中重建该对象。

`BinaryFormatter` 类（命名空间 `System.Runtime.Serialization.Formatters.`）允许将对象写入流或从流中读取。`BinaryFormatter` 将序列化表示形式写入文件，而 `BinaryFormatter` 方法 `Deserialization` 则从文件中读取此表示形式并重建原始对象。如果在序列化或反序列化过程中发生错误，这两个方法都会抛出 `SerializationException`。这两个方法都需要一个 `Stream` 对象（例如 `FileStream`）作为参数，以便 `BinaryFormatter` 能够访问正确的流。

在 17.7–18 节中，我们将使用对象序列化创建并管理顺序访问文件。对象序列化是基于字节流执行的，因此创建和填充的文件将是二进制文件。二进制文件不是人类可读的。出于这个原因，我们编写了一个单独的程序读取并显示序列化对象。其他的序列化格式是人类可读和机器可读的。例如：

- `JsonSerializer`（命名空间 `System.Xml.Serialization`）可以读取和写入 XML（可扩展标记语言）格式的对象

- `DataJsonSerializer`（命名空间 `System.Runtime.Serialization.Json`）可以读取和写入 JSON（JavaScript 对象表示法）格式的对象

XML 和 JSON 是互联网传输数据的流行格式。

## 17.7 使用对象序列化创建顺序访问文件

我们从创建并向顺序访问文件写入序列化对象开始。在本节中，我们复用了 17.3 节的大部分代码，因此我们只关注新功能。

### 定义 RecordSerializable 类

让我们修改 `Record` 类（图 17.3），使得该类的对象可以被序列化。`RecordSerializable` 类（图 17.8；`BankLibrary` 项目的一部分）被标记了被称为特性（attribute）的内容——`[Serializable]`（第 7 行）——此特性告诉 CLR `RecordSerializable` 对象是可以被序列化的。表示可序列化类型的类必须在它们的声明中包含此特性，或实现 `ISerializable` 接口。

```csharp
// Fig 17.8: RecordSerializable.cs
// 表示数据记录的可序列化类。
namespace BankLibrary
{
    [Serializable]
    public class RecordSerializable
    {
        public int Account { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public decimal Balance { get; set; }

        // 默认构造函数将成员设为默认值
        public RecordSerializable()
            :this(0, string.Empty, string.Empty, 0) {}

        // 重载构造函数将成员设为参数值
        public RecordSerializable(int account, string firstName, string lastName, decimal balance)
        {
            Account = account;
            FirstName = firstName;
            LastName = lastName;
            Balance = balance;
        }
    }
}
```

图 17.8 | 表示数据记录的可序列化类。

![](img/57baed2319be0bb1b5f98674846f2711_761_0.png)

在标记了 `[Serializable]` 特性或实现了 `ISerializable` 接口的类中，必须确保类的每个实例变量都是可序列化的。所有简单类型变量和字符串都是可序列化的。对于引用类型的变量，你必须检查类声明以及可能的基类）以确保该类型是可序列化的。默认情况下，数组对象是可以序列化的。然而，如果数组包含对其他对象的引用，这些对象可能是可序列化的，也可能不是。

### 使用序列化流创建输出文件

接下来，我们创建一个带有序列化的顺序访问文件（图 17.9）。为了测试此程序，我们使用图 17.5 中的示例数据创建一个名为 `clients.ser` 的文件——我们使用 `.ser` 扩展名表示该文件存储的是序列化对象。由于示例截图与图 17.4 相同，因此在这里不再显示。第 15 行创建了一个用于写入序列化对象的 `BinaryFormatter`。第 55-56 行打开了 `FileStream`，本程序向其写入序列化对象。传递给 `FileStream` 构造函数的字符串参数表示要打开的文件名和路径。这标识了序列化对象将写入的文件。

```csharp
// Fig. 17.9: CreateFileForm.cs
// 使用序列化创建顺序访问文件。
using System;
using System.Windows.Forms;
using System.IO;
using System.Runtime.Serialization.Formatters.Binary;
using System.Runtime.Serialization;
using BankLibrary;

namespace Createfile
{
    public class CreateFileForm : UIForm
    {
        // 用于以二进制格式序列化 Record
        private BinaryFormatter formatter = new BinaryFormatter();
        // 用于写入文件的流
        private FileStream output;

        // 无参数构造函数
        public CreateFileForm()
        {
            InitializeComponent();
        }

        // saveButton_Click 处理程序
        private void saveButton_Click(object sender, EventArgs e)
        {
            // 文件名
            DialogResult result;
            string fileName;

            // 让用户创建文件
            using (SaveFileDialog filechooser = new SaveFileDialog())
            {
                // 获取对话框的结果
                result = filechooser.ShowDialog();
                fileName = filechooser.FileName;
            }

            // 确保用户点击了 "OK"
            if (result == DialogResult.OK)
            {
                // 如果用户指定的文件无效，显示错误
                if (string.IsNullOrEmpty(fileName))
                {
                    MessageBox.Show("Invalid FileName", "Error", MessageBoxButtons.OK, MessageBox.Error);
                }
                else
                {
                    // 以写入权限打开文件
                    try
                    {
                        output = new FileStream(fileName, FileMode.OpenOrCreate, FileAccess.Write);
                        // 禁用保存按钮并启用输入按钮
                        saveButton.Enabled = false;
                        enterButton.Enabled = true;
                    }
                    catch (IOException)
                    {
                        // 如果文件无法打开，通知用户
                        MessageBox.Show("Error opening file", "Error", MessageBoxButtons.OK, MessageBox.Error);
                    }
                }
            }
        }

        // enterButton_Click 处理程序
        private void enterButton_Click(object sender, EventArgs e)
        {
            // 存储 TextBox 的值的数组
            string[] values = GetTextBoxValues();

            // 确定 TextBox 字段是否为空
            if (!string.IsNullOrEmpty(values[(int)TextBoxIndices.Account]))
            {
                // 将 TextBox 的值存入 RecordSerializable 并序列化
                try
                {
                    // 从 TextBox 获取账号值
                    int accountNumber = int.Parse(values[(int)TextBoxIndices.Account]);

                    // 确定账号是否有效
                    if (accountNumber > 0)
                    {
                        // 序列化的 RecordSerializable
                        var record = new RecordSerializable(accountNumber,
                            values[(int)TextBoxIndices.First],
                            values[(int)TextBoxIndices.Last],
                            decimal.Parse(values[(int)TextBoxIndices.Balance]));

                        // 将 Record 写入 FileStream（序列化对象）
                        formatter.Serialize(output, record);
                    }
                }
                else
                {
                    // 如果账号无效，通知用户
                    MessageBox.Show("Invalid Account Number", "Error", MessageBoxButtons.OK, MessageBox.Error);
                }
            }
        }
    }
}
```

图 17.9 | 使用序列化创建顺序访问文件。（第 1 部分，共 3 部分）。

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
