

## 如何创建 select 方法

图 17-8 显示了如何设计和编码一个 select 方法，使其可与 ObjectDataSource 控件一起使用。此图顶部表格列出了 select 方法可以返回的四种不同类型的值。最简单的是 IEnumerable 接口，它可以返回数据读取器或数据视图，因为 DataReader 和 DataView 类实现了 IEnumerable 接口。此外，IEnumerable 对象可以是使用 C# 的泛型功能创建的强类型集合。

select 方法也可以返回 DataTable 或 DataSet 对象。因为数据集可以包含多个表，所以 ObjectDataSource 控件仅使用数据集中的第一个表。因此，你必须设计 select 方法，使数据集中的第一个表包含你想要访问的数据。

返回数据集而不是数据表或数据视图的主要优点是对象数据源可以缓存数据集。然后，为了启用缓存，你可以将 ObjectDataSource 控件的 EnableCaching 属性设置为 True。在这种情况下，select 方法仅在第一次请求数据时被调用。有关缓存的更多信息，其工作原理与 SqlDataSource 控件相同，请参阅第 13 章。

你也可以向 select 方法传递参数。在这种情况下，ObjectDataSource 控件必须包含一个 SelectParameters 元素。如果使用 Data Source Configuration Wizard 创建控件，此元素会自动添加。然后，你可以创建一个 ControlParameter 元素，将参数绑定到下拉列表等控件。你在图 17-5 中看到了此示例。

### select 方法允许的返回类型

| 返回类型 | 描述 |
| --- | --- |
| IEnumerable | 一个集合，例如 ArrayList 或 HashTable，或一个强类型集合，例如 System.Collections.Generic.List。（因为 DataReader 和 DataView 类实现了 IEnumerable，所以 select 方法也可以返回数据读取器或数据视图。） |
| DataTable | 如果 select 方法返回数据表，ObjectDataSource 控件会自动从表中提取数据视图并使用该视图进行数据绑定。 |
| DataSet | 如果 select 方法返回数据集，ObjectDataSource 控件会从数据集中的第一个数据表中提取数据视图并使用该视图进行数据绑定。 |
| Object | 如果 select 方法返回一个对象，ObjectDataSource 控件会将该对象包装在一个仅包含一项的 IEnumerable 集合中，然后像方法返回 IEnumerable 对象一样进行数据绑定。 |

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

### 描述

- select 方法返回从底层数据库检索的数据。它可以以多种形式返回数据，包括数据读取器或数据集。
- 如果 select 方法返回数据集，对象数据源可以缓存数据。
- select 方法也可以使用 C# 的泛型功能返回强类型集合。有关示例，请参阅图 17-15。
- 如果 select 方法接受参数，则参数必须在 ObjectDataSource 控件的 SelectParameters 元素中声明。在此元素中，你可以使用 ControlParameter 元素声明绑定到页面上其他控件的参数。

## 如何创建 update、delete 和 insert 方法

除了 select 方法之外，对象数据源使用的数据访问类还可以提供更新、删除和插入底层数据库中数据的方法。在编码这些方法之前，你需要确定需要哪些参数。图 17-9 总结了对象数据源如何生成这些参数。

你创建的任何 insert 或 delete 方法都需要一个业务对象作为其参数。此业务对象必须包含方法所需的所有值，并且你可以为其指定任何名称。如果你不提供乐观并发检查，update 方法也需要一个业务对象作为其参数。

如果 update 方法提供乐观并发检查，则需要两个参数，如本图顶部代码所示。参数之一必须是提供要更新行的原始值的业务对象，另一个参数必须是提供该行新值的业务对象。请注意，提供新值的业务对象的参数名称可以随意选择。但是，提供原始值的业务对象的参数名称必须与提供新值的业务对象的参数名称相同，并以 OldValuesParameterFormatString 属性的值为前缀。在此示例中，此属性的值为 original_，这是默认值。

如果表的键列可更新，也需要两个参数。在这种情况下，对象数据源不会自动生成两个参数。因此，即使 update 方法不提供乐观并发检查，你也需要将对象数据源的 ConflictDetection 属性设置为 CompareAllValues，并且需要相应地设置 OldValuesParameterFormatString 属性。然后，你可以使用包含原始值的对象中包含键列值的属性来标识要更新的行。

此图还列出了可用于创建业务对象的业务类的要求。

- 首先，类必须提供一个无参数构造函数。由于 C# 在未定义任何构造函数的情况下默认提供无参数构造函数，因此你可能可以省略此构造函数。但是，我更喜欢为完整性起见包含它。
- 其次，类必须为从绑定控件传递到对象数据源的每个绑定字段定义一个公共属性。如果对象数据源绑定到使用 BoundField 元素的 GridView 或 DetailsView 控件，则这些属性的名称必须与这些元素 DataField 属性指定的名称相同。相比之下，如果对象数据源绑定到使用 TemplateField 元素的 GridView 或 DetailsView 控件，或者如果对象数据源绑定到 FormView 或 ListView 控件，则这些属性的名称必须与绑定控件的 Eval 和 Bind 方法中的名称相同。
- 第三，每个绑定字段的属性必须同时包含 get 和 set 访问器。对象数据源使用 set 访问器根据从绑定控件传递给它的值设置属性的值。而数据访问类中的 insert、update 和 delete 方法使用 get 访问器将属性的值分配给命令对象的参数。

一旦 ObjectDataSource 控件确定需要传递哪些参数，它就会使用反射来确定数据访问类是否具有接受所需参数的方法。如果有，则使用这些参数调用该方法。如果没有，则会抛出异常。

在继续之前，我想指出，你不必使用业务对象作为 insert、update 和 delete 方法的参数。相反，你可以为方法所需每个绑定字段使用一个参数。如果需要的不只是几个字段，这种技术可能会很麻烦。此外，更难确定对象数据源将生成哪些参数。处理 GridView 控件等绑定控件也更困难，因为你必须手动输入要绑定的每个字段的名称。这是因为字段在数据访问类中定义，而不是直接在数据源中定义。（当你使用业务对象时，业务类在数据源中标识，并且该类的属性可供绑定控件使用。）由于这些原因，我建议你尽可能使用业务对象。

## 如何使用属性标记数据访问类

图 17-10 显示了如何使用 C# 属性来标识数据访问类及其方法。如果您以前没有使用过属性，它们只是为类、方法、属性等提供声明性信息的一种方式。虽然其中一些属性在运行时有意义，但本图中的属性在设计时使用。特别是，Data Source Configuration Wizard 使用这些属性来确定 App_Code 文件夹中哪些类是数据访问类，以及数据访问类中哪些方法是 select、insert、update 和 delete 方法。

请注意，您不需要使用这些属性。使用它们的唯一原因是帮助 Data Source Configuration Wizard 识别数据访问类和方法。如果您没有用这些属性标记数据访问类，您仍然可以从向导中访问它们，只需在向导的 Choose a Business Object 步骤中清除 Show Only Data Components 复选框即可（参见图 17-3）。

