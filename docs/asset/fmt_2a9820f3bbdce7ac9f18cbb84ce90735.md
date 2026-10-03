
## GetType 方法

```csharp
public static Type GetType(Assembly assembly, string className)
```

#endregion

## GetConstructors 方法

1. 在上述区域下方添加一个名为 `Fetch Members` 的区域。
2. 添加一个名为 `GetConstructors` 的公共静态 `List<string>` 方法，带有一个名为 `type` 的 `Type` 参数。

```csharp
public static List<string> GetConstructors(Type type)
```

3. 在方法中添加一个名为 `constructors` 的 `List<string>` 变量并对其实例化。
4. 使用 `foreach` 循环遍历构造函数实例的 `GetParameters` 方法的结果。
5. 添加一个新的名为 `ctor` 的 `StringBuilder` 类实例，用于创建构造函数及其参数的字符串。将类型名称和左括号添加到构造函数。

```csharp
var ctor = new StringBuilder(String.Format("{0}", type.Name));
```

6. 添加另一个名为 `parameters` 的 `StringBuilder` 实例，用于构建构造参数列表。对其进行空实例化。
7. 使用 `parameters` `StringBuilder` 变量上的 `Append` 方法，使用 `String.Format` 将构造参数添加到其中，参数类型和名称之间留空格并在末尾添加逗号。

```csharp
parameters.Append(String.Format("{0} {1}", parameter.ParameterType, parameter.Name));
```

8. 添加 `if` 语句检查 `parameters` `StringBuilder` 变量的长度是否等于 0；如果没有参数，则可以向 `ctor` 变量添加右括号。如果有参数，则必须将它们连同右括号一起添加到 `ctor` 中。在将参数参数之前，确保移除 `parameters` 变量末尾的逗号和空格。

```csharp
if (parameters.Length.Equals(0))
    ctor.Append(");");
else
    ctor.Append(String.Format("{0}", parameters.ToString().Substring(0, parameters.Length - 2)));
```

9. 将 `ctor` 变量添加到 `constructors` 集合中。
10. 在方法结束处的循环之外返回 `constructors` 集合。

目前 `Members` 类：

```csharp
public class Members
{
    #region Type Methods
    public static List<string> GetNames(Assembly assembly)
    public static Type GetType(Assembly assembly, string className)
    #endregion

    #region Fetch Type Members
    public static List<string> GetConstructors(Type type)
    {
        // 遍历构造函数
        var constructors = new List<string>();
        foreach (var constructor in type.GetConstructors())
        {
            var ctor = new StringBuilder(String.Format("{0}", type.Name));
            var parameters = new StringBuilder();

            foreach (var parameter in constructor.GetParameters())
                parameters.Append(String.Format("{0} {1}", parameter.ParameterType.Name, parameter.Name));

            if (parameters.Length.Equals(0))
                ctor.Append("{0}");
            else
                ctor.Append(String.Format("{0}",
                    parameters.ToString().Substring(0,
                    parameters.Length - 2)));

            constructors.Add(ctor.ToString());
        }
        return constructors;
    }
    #endregion
}
```

## cbo 组合框的 SelectedIndexChanged 事件

1. 添加 `SelectedIndexChanged` 方法并将返回的类型存储在名为 `type` 的变量中。
2. 对返回的类型调用 `GetType` 方法。将你之前添加到表类中的 `assembly` 变量和组合框中的文本传递给该方法。

```csharp
var type = Members.GetType(assembly, cboTypes.Text);
```

3. 清空 Info 列表框的内容。
4. 向列表框添加一个文本为“--- Constructors --”的项。
5. 通过将 `Members` 类的 `GetConstructors` 方法的调用结果传递给列表项集合的 `AddRange` 方法，将构造函数列表添加到列表框中。

```csharp
lstInfo.Items.AddRange(Members.GetConstructors(type).ToArray());
```

6. 向列表框添加一个空项作为后续信息的分割符。
7. 运行应用程序并确保 Student 类的构造函数已在列表框列表中。

### C# 初学者

到目前为止表类：

```csharp
public partial class Form1 : Form
{
    const string assemblyPath = @"C:\Sample Files\Test Assembly.dll";
    Assembly assembly;

    public Form1() ...

    private void Form1_Load(object sender, EventArgs e) ...

    private void cboTypes_SelectedIndexChanged(object sender, EventArgs e)
    {
        var type = Members.GetType(assembly, cboTypes.Text);

        lstInfo.Items.Clear();
        lstInfo.Items.Add("--- Constructors ---");
        lstInfo.Items.AddRange(Members.GetConstructors(type).ToArray());
        lstInfo.Items.Add("---");
    }
}
```

## 获取类型中的字段

在练习的这部分，你将使用加载的程序集来获取其字段（变量）的信息，并将其显示在 `lstInfo` 列表框中，每个字段占一行。

在 `Members` 类中添加一个名为 `GetFields` 的公共静态方法，该方法带有一个 `Type` 参数；它将获取字段信息并以字符串列表的形式返回。返回的数据将使用 `cboTypes` 组合框的 `SelectedIndexChanged` 事件显示在 `lstInfo` 列表框中。

你可以在 `GetFields` 方法中对传递的类型使用 LINQ 查询，并使用 `String.Format` 方法格式化输出。你需要排除任何名称中包含 `<` 的字段，因为那是系统为了支持属性而添加的字段。输出应该反映该字段是公有的还是私有的，以及其类型和名称（用空格分隔）。

### C# 初学者

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_560_0.png)

## GetFields 方法

- 打开 `Members` 类，在类顶部添加一个名为 `Constants` 的新区域。
- 在区域中添加名为 `flags` 的 `BindingFlags` 并为其分配以下值：`Instance`、`NonPublic`、`Public` 和 `DeclaredOnly`。这些标志决定了从类型中包含哪些成员。
- 在 `Members` 类中找到 `Fetch Type Member`。
- 添加一个名为 `GetFields` 的公共静态方法，该方法有一个名为 `type` 的 `Type` 参数。
- 通过在 `type` 参数上调用 `GetFields` 方法并将 `flags` 常量的 `BindingFlags` 列表传递给方法，返回 LINQ 查询获取字段的结果。

```csharp
static BindingFlags flags =
    BindingFlags.Instance | BindingFlags.NonPublic |
    BindingFlags.Public | BindingFlags.DeclaredOnly;

public static List<string> GetFields(Type type)
    from t in type.GetFields(flags)
```

到目前为止的 `Members` 类：

```csharp
public class Members
{
    #region Constants
    static BindingFlags flags =
        BindingFlags.Instance | BindingFlags.NonPublic |
        BindingFlags.Public | BindingFlags.DeclaredOnly;
    #endregion

    #region Type Methods
    public static List<string> GetTypeNames(Assembly assembly) ...
    public static Type GetType(Assembly assembly, string typeName) ...
    #endregion

    #region Fetch Members
    public static List<string> GetConstructors(Type type) ...
    public static List<string> GetFields(Type type)
    {
        return (
            from t in type.GetFields(flags)
            where t.Name.Contains("<")
            select String.Format("{0} {1} {2}", t.IsPrivate ?
                "private" : "public", t.FieldName, t.Name)
        ).ToList();
    }
    #endregion
}
```

## SelectedIndexChanged 事件

1. 在表的后代码文件中找到 `cboTypes` 组合框的 `SelectedIndexChanged` 事件。
2. 向列表框添加一个文本为“-- Fields --”的项。
3. 通过将 `Members` 类 `GetFields` 方法的调用结果传递给 `AddRange` 方法，将字段列表添加到列表框中。
4. 向列表框添加一个空项作为后续信息的分割符。
5. 运行应用程序并确保 Student 类的字段已列在列表框中。

组合框的 `SelectedIndexChanged` 事件：

```csharp
private void cboTypes_SelectedIndexChanged(object sender, EventArgs e)
{
    var type = Members.GetType(assembly, cboTypes.Text);

    lstInfo.Items.Clear();
    lstInfo.Items.Add("--- Constructors ---");
    lstInfo.Items.AddRange(Members.GetConstructors(type).ToArray());
    lstInfo.Items.Add("---");
    lstInfo.Items.Add("-- Fields --");
    lstInfo.Items.AddRange(Members.GetFields(type).ToArray());
    lstInfo.Items.Add("");
}
```

## 获取类型中的属性

在练习的这部分，你将使用加载的程序集来获取属性的信息，并将其显示在 `lstInfo` 列表框中，每个属性占一行。

在 `Members` 类中添加一个名为 `GetProperties` 的公共静态方法，该方法带有一个 `Type` 参数；它将获取属性信息并以字符串列表的形式返回。返回的数据将使用 `cboTypes` 组合框的 `SelectedIndexChanged` 事件显示在 `lstInfo` 列表框中。

你可以在 `GetProperties` 方法中对传递的类型使用 LINQ 查询，并使用 `String.Format` 方法格式化输出。输出应该反映属性是公有的还是私有的、其类型，以及访问器和赋值器是公有的还是私有的；使用以下格式：`"{0}{1}{2} {3} get; {4} set;}"`

使用类型的 `GetMethod` 和 `GetSet` 方法来获取信息。

![](img/ca0a5dd1bec9fd78e4d7f7685508abf5_562_0.png)

## GetProperties 方法

- 打开 `Members` 类并找到 Fetch 区域。
- 添加一个名为 `GetProperties` 的公共静态方法，该方法有一个名为 `type` 的 `Type` 参数。

```csharp
public static List<string> GetProperties(Type type)
```

- 返回 LINQ 获取属性的结果，通过在 `type` 参数上调用 `GetProperties` 并将 `flags` 常量的 `BindingFlags` 列表传递给方法。

到目前为止的 `Members` 类：

```csharp
public class Members
{
    #region Constants
    static BindingFlags flags =
        BindingFlags.Instance | BindingFlags.NonPublic |
        BindingFlags.Public | BindingFlags.DeclaredOnly;
    #endregion

    #region Type Methods
    public static List<string> GetTypeNames(Assembly assembly) ...
    public static Type GetType(Assembly assembly, string typeName) ...
    #endregion

    #region Fetch Members
    public static List<string> GetConstructors(Type type) ...
    public static List<string> GetFields(Type type) ...
    public static List<string> GetProperties(Type type)
    {
        return (
            from t in type.GetProperties(flags)
            select String.Format("{0}{1}{2} {3} get; {4} set;}", t.GetMethod().IsPrivate ? "private" : "public", t.PropertyName, t.Name, t.GetMethod(true).IsPrivate ? "private" : "public", t.GetMethod(true).IsPrivate ? "private" : "public")
        ).ToList();
    }
    #endregion
}
```

## SelectedIndexChanged 事件

1. 在表的后代码文件中找到 `cboTypes` 组合框的 `SelectedIndexChanged` 事件。
2. 向列表框添加一个文本为“--- Properties ---”的项。
3. 通过将 `Members` 类的 `GetProperties` 方法调用传递给列表框 `Items` 集合的 `AddRange` 方法，将字段列表添加到列表框中。

```csharp
lstInfo.Items.AddRange(Members.GetProperties(type).ToArray());
```

4. 在列表框中添加一个项目，作为后续信息的分割符。
5. 运行应用程序并确保 `Student` 类的属性已添加到列表框中。

目前组合框的 `SelectedIndexChanged` 事件：

```csharp
private void cboTypes_SelectedIndexChanged(object sender, EventArgs e)
{
    // 代码未完整提供
}
```
