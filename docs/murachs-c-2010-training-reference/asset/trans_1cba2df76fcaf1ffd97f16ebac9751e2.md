

# 一个处理文本文件的类

在第 12 章中，你学习了如何开发一个使用名为 Product 的业务类的应用程序。你还学习了如何使用名为 ProductDB 的数据库类中的两个静态方法，用以获取 `Product` 对象的数据并保存 `Product` 对象的数据。然而，你并没有学习如何编写这些数据库方法。

现在，在图 21-7 中，你可以看到一个使用文本文件实现这些方法的 `ProductDB` 类。首先，使用语句指定 `System.Collections.Generic` 和 `System.IO` 命名空间。这使得编写处理存储 `Product` 对象的泛型 `List< >` 集合的代码变得更容易，也便于处理输入输出流。然后，该类提供了两个构造函数来指定目录路径和文本文件路径。这使得这些常量对类中的所有方法可用。

`GetProducts` 方法从文件中读取产品数据，将其存储在 `Product` 对象的 `List< >` 中并返回该 `List< >` 集合。在创建 `StreamReader` 对象和 `List< >` 对象之后，`while` 循环读取文件中的数据并如上所示将 `Product` 对象存储在 `List< >` 集合中。当循环结束，`StreamReader` 和 `FileStream` 对象被关闭，方法返回 `List< >` 对象。至少如果文件已经存在，该方法就是这样工作的。

但请注意，如果执行 `GetProducts` 方法时目录或文件不存在，该方法同样有效。这种情况发生在应用程序首次运行时。在这种情况下，如果目录不存在，方法将创建目录；如果文件不存在，它将创建一个空文件。然后，后续代码仍然可以工作，但不会读取任何记录。

相比之下，`SaveProducts` 方法将 `Product` 对象中的数据写入文件。首先，该方法接受一个 `Product` 对象的 `List< >`。然后，方法将每个 `Product` 对象写入文件。由于 `FileStream` 对象是在 `Create` 模式下实例化的，如果文件不存在，将把 `Product` 对象写入新文件；如果文件已存在，则将覆盖旧文件。

为了重点关注 I/O 代码，此类没有包含异常处理。在生产环境中，尽管你可能会对像这样的类添加异常处理，以便在尽可能接近源的地方捕获并处理异常，这通常有助于减少应用程序所需的异常处理代码量。

# 一个处理文本文件的类

```csharp
using System;
using System.IO;
using System.Collections.Generic;

namespace Maintenance
{
    public class ProductDB
    {
        private const string dir = @"C:\Data\Files\";
        private const string path = dir + "Products.txt";

        public static List<Product> GetProducts()
        {
            if (!Directory.Exists(dir))
                Directory.CreateDirectory(dir);

            StreamReader textIn = new StreamReader(path, FileMode.Open, FileAccess.Read);
            List<Product> products = new List<Product>();
            while (textIn.Peek() != -1)
            {
                string row = textIn.ReadLine();
                string[] columns = row.Split('|');
                Product product = new Product();
                product.Code = columns[0];
                product.Description = columns[1];
                product.Price = Convert.ToDecimal(columns[2]);
                products.Add(product);
            }
            textIn.Close();
            return products;
        }

        public static void SaveProducts(List<Product> products)
        {
            StreamWriter textOut = new StreamWriter(path, FileMode.Create, FileAccess.Write);
            foreach (Product product in products)
            {
                textOut.Write(product.Code + "|");
                textOut.Write(product.Description + "|");
                textOut.WriteLine(product.Price);
            }
            textOut.Close();
        }
    }
}
```
图 21-7 一个处理文本文件的类

# 如何处理二进制文件

要对二进制文件读写数据，请使用 `BinaryReader` 和 `BinaryWriter` 类。你将在随后的图表中学习如何使用这些类，并将看到一个可以用于读取和写入二进制文件的类。

# 如何写入二进制文件

图 21-8 显示了如何使用 `BinaryWriter` 类将数据写入二进制文件。首先，你使用此图顶部的语法创建一个 `BinaryWriter` 对象。为了这样做，你必须提供一个 `FileStream` 作为 `BinaryWriter` 类构造函数的参数。这会将流与 `BinaryWriter` 对象关联，以便将其用于写入文件。

一旦创建了 `BinaryWriter` 对象，你就可以使用其 `Write` 方法写入所有类型的数据。该方法首先识别传递给它的数据类型。然后，它将该数据写入文件。例如，如果你向 `Write` 方法传递一个包含小数值的变量，该方法将不会将小数值转换为字符串。相反，它将把小数值直接写入文件。

示例展示了这是如何工作的。在这里，为一个指定了只写访问权限的文件流创建了一个二进制写入器。由于 `mode` 参数已设置为 `Create`，如果文件存在，则将覆盖文件；如果不存在，则将创建文件。然后，使用 `foreach` 循环将名为 `products` 的 `List< >` 集合中的元素写入文件。由于 `List< >` 集合中的每个元素都是 `Product` 类的对象，因此 `Product` 的每个属性都会被写入。当 `List< >` 集合中的每个元素写入后，使用 `Close` 方法关闭二进制写入器和关联的文件流。

# 创建 BinaryWriter 的基本语法

new BinaryWriter(stream)

# BinaryWriter 类常用的方法

| 方法 | 描述 |
| --- | --- |
| Write(data) | 将数据写入输出流。 |
| Close() | 关闭 BinaryWriter 对象和关联的文件流。 |

# 将 Product 对象集合写入二进制文件的代码

```csharp
BinaryWriter binaryOut = new BinaryWriter(
    new FileStream(path, FileMode.Create, FileAccess.Write));

foreach (Product product in products)
{
    binaryOut.Write(product.Code);
    binaryOut.Write(product.Description);
    binaryOut.Write(product.Price);
}

binaryOut.Close();
```

# 描述

- 你使用 BinaryWriter 对象向二进制文件写入数据。在大多数情况下，你会一个接一个写入字段。
- 与提供多个读取不同类型方法的 `BinaryReader` 类不同，`BinaryWriter` 类通过单一的 `Write` 方法写入数据。

# 如何读取二进制文件

图 21-9 显示了如何使用 `BinaryReader` 类从二进制文件中读取数据。与 `BinaryWriter` 类一样，传递给 `BinaryReader` 的参数是连接文件的 `FileStream` 对象名称。

在二进制文件中，没有终止符来指示一个记录的结束和另一个的开始。因此，你无法一次读取整个记录。相反，你必须一个接一个读取一个字符或一个字段。为了实现这一点，你使用图中所示的 `BinaryReader` 类的方法。在使用时，你必须根据要读取的数据类型使用相应的方法。例如，读取布尔字段时，你使用 `ReadBoolean` 方法。读取小数字段时，你使用 `ReadDecimal` 方法。

`BinaryReader` 类提供了读取 .NET 框架提供的多数数据类型的方法。然而，本图仅显示了这些方法中最常用的。完整列表请查看 `BinaryReader` 类的在线帮助信息。

在读取下一个字符或字段之前，你想确保没有到达文件末尾。为了这样做，你使用 `PeekChar` 方法。然后，如果至少有一个字符可以读取，该方法将返回该字符而不将指针移动到下一个位置。如果没有其他字符，`PeekChar` 方法将返回 -1。然后你可以使用 `Close` 方法关闭二进制读取器和关联的文件流。

