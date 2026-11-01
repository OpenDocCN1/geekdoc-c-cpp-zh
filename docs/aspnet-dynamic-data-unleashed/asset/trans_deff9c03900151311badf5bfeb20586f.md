

新行、ROWVERSION 列，服务器会在每次插入和更新时生成递增值，以及数据库表级别定义的计算列。

动态数据始终选择只读字段模板来显示生成的列的值，无论实体本身是以插入模式还是编辑模式显示。

```csharp
public bool IsCustomProperty { get; }
```

MetaColumn 类的 IsCustomProperty 对于开发人员在代码中定义的属性返回 true，而非数据模型本身定义的普通属性。默认情况下，自定义属性不能用于排序或筛选目的。框架也无法验证它们是否正确持久化到数据库中。基于这些原因，动态数据稳妥起见，默认情况下不会为自定义属性创建筛选器或字段控件；尽管可以通过在代码中向属性应用 UIHintAttribute 和 FilterUIHintAttribute 来改变此行为。

> **注意**
>
> 自 .NET 4.0 版 Service Pack 1 起，用于 Entity Framework 的动态数据提供程序不支持自定义属性，你不会找到描述它们的 MetaColumn 对象。这就是为什么不可能将自定义属性用作显示列。如前所述，可以通过扩展元数据提供程序来解决此问题，这将在第 13 章中讨论。

## 数据注释

MetaColumn 公共接口的很大一部分专门用于数据注释——开发人员可以在代码中应用于实体属性的 .NET 特性。

```csharp
public AttributeCollection Attributes { get; }
```

应用于特定实体属性的所有特性都可以通过 MetaColumn 类的 Attributes 属性访问。与 MetaTable 类的 Attributes 属性类似，此属性也包括来自 System.ComponentModel 和 System.ComponentModel.DataAnnotations 命名空间的内置特性，以及你在应用程序中可能创建的任何自定义特性。

尽管可以直接通过 Attributes 集合获取所有数据注释，但这样做需要反复扫描它，这会迅速耗尽你的 Web 服务器宝贵的 CPU 资源。相反，动态数据仅在创建 MetaColumn 对象时扫描一次特性，并将它们的值存储在对象的字段中，以便以后即时访问。

## 脚手架支持

多个数据注释和 MetaColumn 属性在脚手架过程中扮演重要角色，在这个过程中，动态数据确定特定列是否需要在页面上由字段或筛选器控件表示，以及如何选择该控件的模板。

```csharp
public virtual bool Scaffold { get; set; }
```

MetaColumn 类的 Scaffold 属性确定动态数据是否会为其表示的实体属性生成字段模板。默认情况下，对于自动生成的、自定义的以及作为外键一部分的基元属性，Scaffold 返回 false。你可以通过应用 ScaffoldColumnAttribute 或指定 AutoGenerateField 属性值的 DisplayAttribute 来更改此属性的默认值。

```csharp
public virtual string UIHint { get; }
```

MetaColumn 类的 UIHint 属性返回动态数据在为实体属性生成控件时首先尝试的字段模板的名称。除非你在代码中向实体属性应用 UIHintAttribute，否则 UIHint 属性返回空字符串。

```csharp
public DataTypeAttribute DataTypeAttribute { get; }
```

DataTypeAttribute 属性返回在代码中应用于实体属性的 DataTypeAttribute。UIHint 和数据类型优先于动态数据在搜索适当字段模板时尝试的基于 .NET 类型的更通用的模板名称。

```csharp
public string FilterUIHint { get; }
```

FilterUIHint 属性与 UIHint 类似，但指定筛选器模板的名称。默认情况下它也返回空字符串，可以通过向实体属性应用 FilterUIHintAttribute 来指定。动态数据在生成筛选器控件时使用筛选器提示，通常作为 List 页面模板中 QueryableFilterRepeater 的一部分。

```csharp
public bool AllowInitialValue { get; }
```

MetaColumn 的 AllowInitialValue 属性确定实体属性是否可以在插入模式下输入值。对于生成的属性和只读属性，AllowInitialValue 返回 false。你也可以通过向实体属性应用指定了 AllowInitialValue 值的 EditableAttribute 来覆盖它。

## 业务逻辑支持

MetaColumn 类的几个属性为基于数据注释的业务逻辑提供支持。这个数字小得令人惊讶，因为它只涵盖了第 3 章“字段模板”中讨论的三个特性。

```csharp
public object DefaultValue { get; }
```

MetaColumn 类的 Description 属性返回通过在代码中向实体属性应用 DescriptionAttribute 所指定的描述。动态数据提供的内置字段模板当前不使用此属性。但是，你可以轻松修改它们，并使用此属性为字段模板中的数据控件生成工具提示。

## 格式化选项

最后值得提及的数据注释属性是与格式化选项相关的属性，可以通过向实体属性应用 DisplayFormatAttribute 来指定这些选项。DynamicControl 和 DynamicField 控件使用这些属性来实现灵活且一致的字段值格式。

```csharp
public string DataFormatString { get; }
```

DataFormatString 属性返回一个包含 .NET 格式字符串（如 "{0:C}"）的字符串，该字符串将用于通过调用 String 类的 Format 方法将字段值转换为字符串。尽管包含参数编号 0 似乎没有必要，因为只有一个字段值要格式化，但它是格式字符串正常工作的必要条件。

```csharp
public bool ApplyFormatInEditMode { get; }
```

ApplyFormatInEditMode 属性确定动态数据是否不仅会在 List 和 Details 页面的只读模式下使用 DataFormatString，还会在编辑模式下使用。

```csharp
public string NullDisplayText { get; }
```

NullDisplayText 属性指定当字段值为 null 时动态数据将显示的文本。

```csharp
public bool ConvertEmptyStringToNull { get; }
```

ConvertEmptyStringToNull 属性确定 NullDisplayText 是否也将用于空字符串。

```csharp
public bool HtmlEncode { get; }
```

HtmlEncode 属性确定字段值中可能包含的任何特殊字符是否将使用 HTML 转义序列进行编码。此属性默认为 true，使动态生成的页面免受 HTML 注入攻击。只有当你的应用程序允许用户以 HTML 表单输入格式化文本，并在保存到数据库之前对用户输入的值进行彻底清理以删除危险 HTML 标签（如 <script>）时，才应考虑更改它。

## MetaForeignKeyColumn 类

MetaForeignKeyColumn 类是 MetaColumn 类的专用后代，表示多对一和一对一导航属性，例如 Northwind 数据模型中 Product 实体的 Supplier 属性。动态数据元数据 API 中的这些“外键”列具有可以通过此类访问的附加属性。

```csharp
public MetaTable ParentTable { get; }
```

ParentTable 属性返回一个 MetaTable 对象，该对象描述外键引用的父实体。对于 Product 实体的 Supplier 属性，ParentTable 属性返回描述 Supplier 实体的 MetaTable 对象。此属性在实现筛选和导航功能方面发挥重要作用。特别是，ForeignKey 字段和筛选器模板使用它从父表中检索行，以下拉列表的形式显示。

```csharp
public ReadOnlyCollection<string> ForeignKeyNames { get; }
```

MetaForeignKeyColumn 类的 ForeignKeyNames 属性返回构成外键的基元实体属性的集合。对于 Product 实体的 Supplier 属性，此属性返回一个包含单个列名——SupplierID 的集合。只有当父表具有复合主键并且外键包含多个基元属性时，此属性返回的集合才有多个项。

### 呈现逻辑

MetaForeignKeyColumn 类的其余属性和方法为在动态数据应用程序中实现呈现逻辑提供支持。

```csharp
public bool IsPrimaryKeyInThisTable { get; }
```

MetaForeignKeyColumn 类的 IsPrimaryKeyInThisTable 属性，如果外键的任何基元组件是实体自身主键的成员，则返回 true。例如，Northwind 数据模型中的 Order_Detail 实体有一个由 OrderID 和 ProductID 属性组成的复合主键。Order 导航属性由 MetaForeignKeyColumn 表示，其 IsPrimaryKeyInThisTable 返回 true，因为 OrderID 是 Order_Detail 实体主键的一部分。

> **注意**
>
> 默认情况下，动态数据不允许编辑主键值，并使用 IsPrimaryKeyInThisTable 属性在编辑模式下为属于主键一部分的外键列显示只读字段模板。

```csharp
public IList<object> GetForeignKeyValues(object row);
```

