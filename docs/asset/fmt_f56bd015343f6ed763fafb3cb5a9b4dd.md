
```csharp
public class Category
{
    private string categoryID;
    private string shortName;
    private string longName;

    public Category()
    {
    }

    public string CategoryID
    {
        get
        {
            return categoryID;
        }
        set
        {
            categoryID = value;
        }
    }

    public string ShortName
    {
        get
        {
            return shortName;
        }
        set
        {
            shortName = value;
        }
    }

    public string LongName
    {
        get
        {
            return longName;
        }
        set
        {
            longName = value;
        }
    }
}
```

## 注意

由于自动实现的属性会自动提供 `get` 和 `set` 访问器，因此你可以在业务类中使用它们，而不必使用标准属性。

## CategoryDB 类

图 17-15 的两部分展示了 `CategoryDB` 类，该类用作此应用程序的数据访问类。这个类使用 `DataObject` 和 `DataObjectMethod` 特性，将类标记为数据对象类，并将方法标记为数据对象方法。

这个类中的四个公共方法提供了此应用程序执行的选择、插入、删除和更新操作。这些方法使用标准的 ADO.NET 代码访问数据库。由于这些代码简单明了，你应该不难理解其工作原理。因此，我在此仅作简要描述。

`GetCategories` 方法从 `Halloween` 数据库的 `Categories` 表中检索所有行和列。然后，这些数据被存储在一个 `List<Category>` 对象中。为此，它对数据读取器（data reader）检索到的每一行创建一个来自 `Category` 类的对象，并将该行中的值分配给对象的相应属性。然后，它将该对象添加到 `List<Category>` 对象。最后，将 `List<Category>` 对象返回给对象数据源，对象数据源使用它来填充 `GridView` 控件。注意，由于 `List<Category>` 是强类型集合，`Category` 类公开的属性名称可以从 `GridView` 控件的“字段”对话框中获得，因此我不必手动输入它们。在本章末尾的练习 17-2 中，你将有机会对此进行试验。

为了获取到 `Halloween` 数据库的连接，`GetCategories` 方法会调用私有方法 `GetConnectionString`。该方法从 `web.config` 文件中获取连接字符串。其他公共方法也调用 `GetConnectionString` 方法。

当用户在 `DetailsView` 控件中单击 `Insert` 按钮时，对象数据源会执行 `InsertCategory` 方法。该方法被声明为仅接受一个 `Category` 对象参数。当对象数据源执行此方法时，它会把用户输入到 `DetailsView` 控件中的值传递给该对象。然后，该方法将该对象的 `CategoryID`、`ShortName` 和 `LongName` 属性分配给 `Insert` 语句的 `Values` 子句中定义的参数。当执行 `Insert` 语句时，会将包含这些值的新行插入到 `Categories` 表中。

## CategoryDB.cs 文件

```csharp
using System.Data;
using System.Data.SqlClient;
using System.Configuration;
using System.ComponentModel;
using System.Collections.Generic;

[DataObject(true)]
public static class CategoryDB
{
    [DataObjectMethod(DataObjectMethodType.Select)]
    public static List<Category> GetCategories()
    {
        List<Category> categoryList = new List<Category>();
        SqlConnection con = new SqlConnection(GetConnectionString());
        string sel = "SELECT CategoryID, ShortName, LongName "
            + "FROM Categories ORDER BY ShortName";
        SqlCommand cmd = new SqlCommand(sel, con);
        con.Open();
        SqlDataReader dr =
            cmd.ExecuteReader(CommandBehavior.CloseConnection);
        Category category;
        while (dr.Read())
        {
            category = new Category();
            category.CategoryID = dr["CategoryID"].ToString();
            category.ShortName = dr["ShortName"].ToString();
            category.LongName = dr["LongName"].ToString();
            categoryList.Add(category);
        }
        dr.Close();
        return categoryList;
    }

    private static string GetConnectionString()
    {
        return ConfigurationManager.ConnectionStrings
            ["HalloweenConnectionString"].ConnectionString;
    }

    [DataObjectMethod(DataObjectMethodType.Insert)]
    public static int InsertCategory(Category category)
    {
        SqlConnection con = new SqlConnection(GetConnectionString());
        string ins = "INSERT INTO Categories "
            + " (CategoryID, ShortName, LongName) "
            + " VALUES(@CategoryID, @ShortName, @LongName)";
        SqlCommand cmd = new SqlCommand(ins, con);
        cmd.Parameters.AddWithValue("CategoryID", category.CategoryID);
        cmd.Parameters.AddWithValue("ShortName", category.ShortName);
        cmd.Parameters.AddWithValue("LongName", category.LongName);
        con.Open();
        int i = cmd.ExecuteNonQuery();
        con.Close();
        return i;
    }
}
```

图 17-15 分类维护应用程序的 `CategoryDB` 类（第 1 部分，共 2 部分）

当用户在 `GridView` 控件中单击 `Delete` 按钮时，对象数据源会执行 `DeleteCategory` 方法。该方法同样接受一个 `Category` 对象作为唯一参数。该对象包含最初从 `Categories` 表中检索出来的值。该对象的 `CategoryID`、`ShortName` 和 `LongName` 属性被分配给 `Delete` 语句的 `Where` 子句中定义的参数。

请注意，此方法返回一个整数值。然后，当执行包含 `Delete` 语句的命令时，结果存储在一个整数变量中，该变量被返回给对象数据源。由于该值指示被删除的行数，因此可以像图 17-13 中所示的那样，用它来检查并发错误。

最后一个方法 `UpdateCategory` 在用户单击 `GridView` 控件中的 `Update` 按钮时执行。它接受两个 `Category` 对象参数。第一个包含最初从 `Categories` 表中检索的值，第二个包含该行的新值。第一个对象的 `CategoryID`、`ShortName` 和 `LongName` 属性被分配给 `Update` 语句的 `Where` 子句中定义的参数，第二个对象的 `ShortName` 和 `LongName` 属性被分配给 `Update` 语句的 `Set` 子句中定义的属性。

与 `DeleteCategory` 方法一样，`UpdateCategory` 方法返回一个整数值，指示受更新操作影响的行数。然后，该值可用于检查并发错误。

## CategoryDB.cs 文件

```csharp
[DataObjectMethod(DataObjectMethodType.Delete)]
public static int DeleteCategory(Category category)
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string del = "DELETE FROM Categories "
        + "WHERE CategoryID = @CategoryID "
        + "AND ShortName = @ShortName "
        + "AND LongName = @LongName";
    SqlCommand cmd = new SqlCommand(del, con);
    cmd.Parameters.AddWithValue("CategoryID", category.CategoryID);
    cmd.Parameters.AddWithValue("ShortName", category.ShortName);
    cmd.Parameters.AddWithValue("LongName", category.LongName);
    con.Open();
    int i = cmd.ExecuteNonQuery();
    con.Close();
    return i;
}
```

```csharp
[DataObjectMethod(DataObjectMethodType.Update)]
public static int UpdateCategory(Category original_Category, Category category)
{
    SqlConnection con = new SqlConnection(GetConnectionString());
    string up = "UPDATE Categories "
        + "SET ShortName = @ShortName, "
        + "LongName = @LongName "
        + "WHERE CategoryID = @original_CategoryID "
        + "AND ShortName = @original_ShortName "
        + "AND LongName = @original_LongName";
    SqlCommand cmd = new SqlCommand(up, con);
    cmd.Parameters.AddWithValue("ShortName", category.ShortName);
    cmd.Parameters.AddWithValue("LongName", category.LongName);
    cmd.Parameters.AddWithValue("original_CategoryID", original_Category.CategoryID);
    cmd.Parameters.AddWithValue("original_ShortName", original_Category.ShortName);
    cmd.Parameters.AddWithValue("original_LongName", original_Category.LongName);
    con.Open();
    int updateCount = cmd.ExecuteNonQuery();
    con.Close();
    return updateCount;
}
```

## 如何使用对象数据源进行分页

使用对象数据源时出现的一个复杂问题是，它不会自动为 `GridView` 等控件提供分页功能。因此，你必须设置对象数据源提供分页的属性，并且必须在数据访问类中提供分页功能。你将在接下来的两个主题中学习如何做到这一点。

## 如何创建提供分页的 ObjectDataSource 控件

要创建提供分页的 `ObjectDataSource` 控件，请设置图 17-16 中显示的四个属性。`EnablePaging` 属性仅表示对象数据源支持分页。`StartRowIndexParameterName` 和 `MaximumRowsParameterName` 属性指定将在数据访问类的 `select` 方法中使用的参数名称，以确定方法返回哪些行。你将在下一张图中看到一个示例说明其工作原理。现在，只需意识到当你使用分页器控件在绑定控件中显示另一页数据时，绑定控件会将将分配给这两个参数的值传递给 `ObjectDataSource` 控件。

最后一个属性 `SelectCountMethod`，命名了数据访问类中返回 `select` 方法检索到的总行数的方法。绑定到对象数据源的控件使用此值来确定要显示哪些分页器控件。例如，如果绑定控件使用第一页、上一页、下一页和最后一页分页器控件，它将能够确定何时显示第一页或最后一页，以便可以省略第一页和上一页或下一页和最后一页分页器控件。这由本图顶部显示的 `GridView` 控件说明，该控件绑定到此处显示的对象数据源。在这种情况下，显示第一页，因此未包含第一页和上一页分页器控件。

## 提供分页的 GridView 控件

| ID | Name | Category | Unit Price | On Hand |
| --- | --- | --- | ---: | ---: |
| pow01 | Austin Powers | costumes | $79.99 | 25 |
| blo01 | Black Light (24") | fx | $24.99 | 200 |
| vader01 | Darth Vader Mask | masks | $19.99 | 100 |
| cat01 | Deranged Cat | props | $19.99 | 45 |
| bats01 | Flying Bats | props | $69.99 | 25 |
| fogj01 | Fog Juice (1qt) | fx | $9.99 | 500 |
| fog01 | Fog Machine | fx | $34.99 | 100 |
| frank01 | Frankenstein | costumes | $39.99 | 100 |
|  | >>> |  |  |  |

## 用于分页的 ObjectDataSource 控件的属性

| Attribute | Description |
| --- | --- |
| `EnablePaging` | True if the `ObjectDataSource` control supports paging. |
| `StartRowIndexParameterName` | The name of the parameter in the `select` method of the data access class that receives the index of the first row to be retrieved. The default is `startRowIndex`. |
| `MaximumRowsParameterName` | The name of the parameter in the `select` method of the data access class that receives the maximum number of rows to be retrieved. The default is `maximumRows`. |
| `SelectCountMethod` | The name of a public method in the data access class that returns the total number of rows that are retrieved by the `select` method. |

## 提供分页的 ObjectDataSource 控件的 aspx 代码
