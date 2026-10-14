
# 图 17-6 展示了 `ProductDB` 类的 C# 代码

要创建此类，我使用了 `Website→Add New Item` 命令向 `App_Code` 文件夹添加了一个类文件。然后，我添加了 `public GetAllCategories` 和 `GetProductsByCategory` 方法的代码。我还创建了一个名为 `GetConnectionString` 的私有方法。此方法被两个 `public` 方法使用，用于检索 `Halloween` 数据库的连接字符串。

在解释这些方法的工作细节之前，我想指出此类的 `DataObject` 和 `DataObjectMethod` 属性。这些属性用于将类和方法标识为数据对象，你将在图 17-10 中学习如何使用它们。现在，只需意识到它们被 `Data Source Configuration Wizard` 使用，以确定在配置对象数据源时要显示哪些类和方法。

## `GetAllCategories` 方法

`GetAllCategories` 方法首先创建到 `Halloween` 数据库的连接。为了获取此数据库的连接，它调用 `GetConnectionString` 方法。接下来，此方法创建包含将用于从 `Halloween` 数据库检索数据的 `Select` 语句的字符串：

```
SELECT CategoryID, LongName
FROM Categories
ORDER BY LongName
```

然后，使用包含 `Select` 语句的字符串和连接对象作为参数创建 `SqlCommand` 对象。最后，打开连接，调用命令对象的 `ExecuteReader` 方法以创建包含请求数据的 `data reader` 对象，并将 `data reader` 返回给对象数据源。

## `GetProductsByCategory` 方法

`GetProductsByCategory` 方法稍微复杂一些，因为它在 `Select` 语句中使用了一个参数：

```
SELECT ProductID, Name, UnitPrice, OnHand
FROM Products
WHERE CategoryID = @CategoryID
ORDER BY ProductID
```

同样，使用此 `Select` 语句和连接对象创建 `SqlCommand` 对象。然后，在打开连接之前，将名为 `CategoryID` 的参数添加到命令的 `Parameters` 集合中，并执行命令以返回包含请求数据的 `data reader`。

## `GetConnectionString` 方法

`GetConnectionString` 方法使用 `ConfigurationManager` 类从 `web.config` 文件中检索名为 `"HalloweenConnectionString"` 的连接字符串。因此，`Halloween` 数据库的连接字符串必须存储在此文件中。要刷新你关于如何存储它的记忆，请参阅第 13 章中的图 13-4。

```csharp
using System;
using System.Collections;
using System.Configuration;
using System.Data;
using System.Data.SqlClient;
using System.ComponentModel;

[DataObject(true)]
public static class ProductDB
{
    [DataObjectMethod(DataObjectMethodType.Select)]
    public static IEnumerable GetAllCategories()
    {
        SqlConnection con = new SqlConnection(GetConnectionString());
        string sel = "SELECT CategoryID, LongName "
            + "FROM Categories ORDER BY LongName";
        SqlCommand cmd = new SqlCommand(sel, con);
        con.Open();
        SqlDataReader dr = cmd.ExecuteReader(CommandBehavior.CloseConnection);
        return dr;
    }

    [DataObjectMethod(DataObjectMethodType.Select)]
    public static IEnumerable GetProductsByCategory(string CategoryID)
    {
        SqlConnection con = new SqlConnection(GetConnectionString());
        string sel = "SELECT ProductID, Name, "
            + "UnitPrice, OnHand "
            + "FROM Products "
            + "WHERE CategoryID = @CategoryID "
            + "ORDER BY ProductID";
        SqlCommand cmd = new SqlCommand(sel, con);
        cmd.Parameters.AddWithValue("CategoryID", CategoryID);
        con.Open();
        SqlDataReader dr = cmd.ExecuteReader(CommandBehavior.CloseConnection);
        return dr;
    }

    private static string GetConnectionString()
    {
        return ConfigurationManager.ConnectionStrings
            ["HalloweenConnectionString"].ConnectionString;
    }
}
```

## Note

- `DataObject` 和 `DataObjectMethod` 属性在图 17-10 中有描述。

# 如何创建数据访问类

使用对象数据源最具挑战性的方面是开发它们所需的数据访问类。因此，以下主题解释了如何设计和实现这些类。

## 如何设计数据访问类

如图 17-7 所示，被 `ObjectDataSource` 控件使用的的数据访问类可以有四种不同类型的方法，用于选择、插入、更新和删除数据。你可以为这些方法使用任何方法名称，并且可以设计类使其具有多于一种的每种类型的方法。例如，前一图中使用 `ProductDB` 类有两个名为 `GetAllCategories` 和 `GetProductsByCategory` 的 `select` 方法。

数据访问方法可以是静态方法或实例方法。如果将它们定义为实例方法，`ObjectDataSource` 控件将在调用方法之前创建数据访问类的实例，并在方法执行后销毁该对象。为此工作，数据访问类必须提供一个无参数构造函数。在 C# 中，如果类没有构造函数，则默认提供无参数构造函数。

由于创建和销毁数据访问对象可能耗时，我建议你尽可能对 `select`、`insert`、`update` 和 `delete` 方法使用静态方法。这样，`ObjectDataSource` 控件在调用数据访问方法时就不必创建数据访问类的实例。

尽管你通过使用 `SelectMethod`、`InsertMethod`、`UpdateMethod` 和 `DeleteMethod` 属性提供 `ObjectDataSource` 控件调用的方法名称，但 `ObjectDataSource` 控件要到运行时才会生成将传递给这些方法的参数。因此，`ObjectDataSource` 控件必须使用 .NET 的 `reflection` 特性来确定它调用的方法是否包含正确的参数。它还使用 `reflection` 来确定 `select` 方法的返回类型。正如你将在下一图中看到的，这使你可以设计一个 `select` 方法，使其能够以多种形式返回所选数据。

如果之前没有遇到过 `reflection`，它是 .NET 的一个特性，可在运行时提供有关已编译类的信息。例如，`reflection` 可以确定特定类提供了哪些方法。此外，它可以确定每个方法需要哪些参数以及方法返回的类型。

## 数据访问类中的方法类型

| 方法类型 | 描述 |
|---|---|
| `Select` | 从数据库检索数据并将其作为 `IEnumerable` 对象返回。 |
| `Insert` | 向底层数据库插入一行的数据。新的行的值通过一个或多个参数传递。 |
| `Update` | 更新底层数据库中一行的數據。更新行的值以及用于实现乐观并发的任何值都通过一个或多个参数传递。 |
| `Delete` | 从底层数据库删除一行。待删除行的键或键以及用于实现乐观并发的任何值都通过一个或多个参数传递。 |

## 对象数据源如何确定调用哪个方法

- 用于 `select`、`insert`、`update` 和 `delete` 操作的方法名称由 `SelectMethod`、`InsertMethod`、`UpdateMethod` 或 `DeleteMethod` 属性指定。
- `ObjectDataSource` 控件根据要插入、更新或删除的数据字段以及是否使用乐观并发来确定需要传递给数据访问类方法的参数。
- `ObjectDataSource` 控件使用 `reflection` 来确定数据访问类提供的 `insert`、`update` 和 `delete` 方法的参数签名。
- 在运行时，如果类没有提供具有正确名称和参数的方法，则会抛出异常。

## 描述

- 数据访问类可以声明 `public` 方法来选择、插入、更新和删除数据。这些方法可以是实例方法或静态方法。
- 你可以为 `select`、`insert`、`update` 和 `delete` 方法使用任何方法名称。
- 如果 `select`、`insert`、`update` 和 `delete` 方法是静态方法，则在不创建数据访问类的实例的情况下使用这些方法。
- 如果 `select`、`insert`、`update` 和 `delete` 方法是实例方法，则为每次数据访问操作创建并销毁数据访问类的实例。在这种情况下，数据访问类必须提供一个无参数构造函数。
- 你可以使用参数将选择条件或其他数据传递给 `select`、`insert`、`update` 和 `delete` 方法。有关 `insert`、`update` 和 `delete` 方法使用的参数的更多信息，请参阅图 17-9。
- `Reflection` 是 .NET 的一个特性，可在运行时提供有关已编译类和方法的的信息。

图 17-7 如何设计数据访问类

## 如何创建 select 方法

图 17-8 显示了如何设计和编码一个 `select` 方法，使其可与 `ObjectDataSource` 控件一起使用。此图顶部表格列出了 `select` 方法可以返回的四种不同类型的值。最简单的是 `IEnumerable` 接口，它可以返回数据读取器或数据视图，因为 `DataReader` 和 `DataView` 类实现了 `IEnumerable` 接口。此外，`IEnumerable` 对象可以是使用 C# 的泛型功能创建的强类型集合。

`select` 方法也可以返回 `DataTable` 或 `DataSet` 对象。因为数据集可以包含多个表，所以 `ObjectDataSource` 控件仅使用数据集中的第一个表。因此，你必须设计 `select` 方法，使数据集中的第一个表包含你想要访问的数据。

返回数据集而不是数据表或数据视图的主要优点是对象数据源可以缓存数据集。然后，为了启用缓存，你可以将 `ObjectDataSource` 控件的 `EnableCaching` 属性设置为 `True`。在这种情况下，`select` 方法仅在第一次请求数据时被调用。有关缓存的更多信息，其工作原理与 `SqlDataSource` 控件相同，请参阅第 13 章。

你也可以向 `select` 方法传递参数。在这种情况下，`ObjectDataSource` 控件必须包含一个 `SelectParameters` 元素。如果使用 `Data Source Configuration Wizard` 创建控件，此元素会自动添加。然后，你可以创建一个 `ControlParameter` 元素，将参数绑定到下拉列表等控件。你在图 17-5 中看到了此示例。

### select 方法允许的返回类型

| 返回类型 | 描述 |
| --- | --- |
| `IEnumerable` | 一个集合，例如 `ArrayList` 或 `HashTable`，或一个强类型集合，例如 `System.Collections.Generic.List`。（因为 `DataReader` 和 `DataView` 类实现了 `IEnumerable`，所以 `select` 方法也可以返回数据读取器或数据视图。） |
| `DataTable` | 如果 `select` 方法返回数据表，`ObjectDataSource` 控件会自动从表中提取数据视图并使用该视图进行数据绑定。 |
| `DataSet` | 如果 `select` 方法返回数据集，`ObjectDataSource` 控件会从数据集中的第一个数据表中提取数据视图并使用该视图进行数据绑定。 |
| `Object` | 如果 `select` 方法返回一个对象，`ObjectDataSource` 控件会将该对象包装在一个仅包含一项的 `IEnumerable` 集合中，然后像方法返回 `IEnumerable` 对象一样进行数据绑定。 |

### 返回数据读取器的 select 方法

```
public static IEnumerable GetAllCategories()
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string sel = "SELECT CategoryID, LongName "
        + "FROM Categories ORDER BY LongName";
    SqlCommand cmd = new SqlCommand(sel, con);
    con.Open();
    SqlDataReader dr = cmd.ExecuteReader(CommandBehavior.CloseConnection);
    return dr;
}
```

### 返回数据集的 select 方法

```
public static DataSet GetAllCategories()
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string sel = "SELECT CategoryID, LongName "
        + "FROM Categories ORDER BY LongName";
    SqlDataAdapter da = new SqlDataAdapter(sel, con);
    DataSet ds = new DataSet();
    da.Fill(ds, "Categories");
    return ds;
}
```

## 描述

- `select` 方法返回从底层数据库检索的数据。它可以以多种形式返回数据，包括数据读取器或数据集。
- 如果 `select` 方法返回数据集，对象数据源可以缓存数据。
- `select` 方法也可以使用 C# 的泛型功能返回强类型集合。有关示例，请参阅图 17-15。
- 如果 `select` 方法接受参数，则参数必须在 `ObjectDataSource` 控件的 `SelectParameters` 元素中声明。在此元素中，你可以使用 `ControlParameter` 元素声明绑定到页面上其他控件的参数。

## 如何创建 update、delete 和 insert 方法

除了 `select` 方法之外，对象数据源使用的数据访问类还可以提供更新、删除和插入底层数据库中数据的方法。在编码这些方法之前，你需要确定需要哪些参数。图 17-9 总结了对象数据源如何生成这些参数。

你创建的任何 `insert` 或 `delete` 方法都需要一个业务对象作为其参数。此业务对象必须包含方法所需的所有值，并且你可以为其指定任何名称。如果你不提供乐观并发检查，`update` 方法也需要一个业务对象作为其参数。

如果 `update` 方法提供乐观并发检查，则需要两个参数，如本图顶部代码所示。参数之一必须是提供要更新行的原始值的业务对象，另一个参数必须是提供该行新值的业务对象。请注意，提供新值的业务对象的参数名称可以随意选择。但是，提供原始值的业务对象的参数名称必须与提供新值的业务对象的参数名称相同，并以 `OldValuesParameterFormatString` 属性的值为前缀。在此示例中，此属性的值为 `original_`，这是默认值。

如果表的键列可更新，也需要两个参数。在这种情况下，对象数据源不会自动生成两个参数。因此，即使 `update` 方法不提供乐观并发检查，你也需要将对象数据源的 `ConflictDetection` 属性设置为 `CompareAllValues`，并且需要相应地设置 `OldValuesParameterFormatString` 属性。然后，你可以使用包含原始值的对象中包含键列值的属性来标识要更新的行。

此图还列出了可用于创建业务对象的业务类的要求。

- 首先，类必须提供一个无参数构造函数。由于 C# 在未定义任何构造函数的情况下默认提供无参数构造函数，因此你可能可以省略此构造函数。但是，我更喜欢为完整性起见包含它。
- 其次，类必须为从绑定控件传递到对象数据源的每个绑定字段定义一个公共属性。如果对象数据源绑定到使用 `BoundField` 元素的 `GridView` 或 `DetailsView` 控件，则这些属性的名称必须与这些元素 `DataField` 属性指定的名称相同。相比之下，如果对象数据源绑定到使用 `TemplateField` 元素的 `GridView` 或 `DetailsView` 控件，或者如果对象数据源绑定到 `FormView` 或 `ListView` 控件，则这些属性的名称必须与绑定控件的 `Eval` 和 `Bind` 方法中的名称相同。
