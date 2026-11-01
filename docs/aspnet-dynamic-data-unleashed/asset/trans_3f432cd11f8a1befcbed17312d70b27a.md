
```csharp
[MetadataType(typeof(IProduct))]
public partial class Product : IProduct
{
}
```

请注意，Product 类不仅实现了 IProduct 接口，还将其指定为元数据类型。与前一个示例中未类型化的元数据类不同，元数据接口必须声明 ProductName 属性，其类型为 string，以便与真实 Product 类中的实际实现相匹配。如果两者不同步，您会立即得到编译器错误，而不是在运行时出现 InvalidOperationException。

> > **NOTE**
> >
> > 这里讨论的两种元数据类型方法都不完美。嵌套类方法实现了最佳封装；在程序集级别不会引入额外的类型。这有助于减少混淆，并使元数据类无法被误用。接口方法使维护元数据类型变得更容易，但会导致在数据模型程序集中引入额外的接口类型。接口可以声明为 internal，但它们仍会在数据模型程序集本身中可见并可能被误用。最终，是否对数据注释使用嵌套类或接口的决定可能取决于个人喜好。

## 使用 TypeDescriptor 注册元数据提供程序

如果您尝试在与 Dynamic Data Web 应用程序分离的控制台应用程序中编译并运行以下代码，您可能会惊讶地发现使用元数据类应用于 Product 类的 ProductName 属性的 RequiredAttribute 完全被忽略了。而且 ValidateObject 方法不会抛出 ValidationException，正如您所期望的那样：

```csharp
var product = new Product();
var context = new ValidationContext(product, null, null);
Validator.ValidateObject(product, context, true);
```

在幕后，Validator 使用来自 System.ComponentModel 命名空间的静态类 TypeDescriptor 来确定需要验证的对象的每个属性上应用的属性列表。应用于 Product 类的 MetadataTypeAttribute 实际上除非已为特定对象或其整个类配置，否则不会产生任何效果。Dynamic Data 在上下文注册期间会自动为所有实体类执行此操作，但要在其他类型的应用程序中执行验证，您需要通过显式调用 TypeDescriptor 的静态 AddProviderTransparent 方法并传递 AssociatedMetadataTypeTypeDescriptionProvider 类的实例来完成，如下所示：

```
namespace Unleashed.EntityFramework
{
    public class UnleashedObjectContext : ObjectContext
    {
        private const EntityState ChangedEntityStates =
            EntityState.Added | EntityState.Modified | EntityState.Deleted;

        public override int SaveChanges(SaveOptions options)
        {
            IEnumerable<ObjectStateEntry> stateEntries = this.ObjectStateManager
                .GetObjectStateEntries(ChangedEntityStates)
                .Where(stateEntry => !stateEntry.IsRelationship);

            foreach (ObjectStateEntry stateEntry in stateEntries)
                this.BeforeSaveChanges(stateEntry);

            return base.SaveChanges(options);
        }

        private void BeforeSaveChanges(ObjectStateEntry stateEntry)
        {
            if (stateEntry.State != EntityState.Deleted)
                this.Validate(stateEntry);
        }

        private void Validate(ObjectStateEntry stateEntry)
        {
            object entity = stateEntry.Entity;
            var context = new ValidationContext(entity, null, null);
            Validator.ValidateObject(entity, context, true);
        }
    }
}
```

首先，重写的 SaveChanges 方法从跟踪 ObjectContext 中所有实体的 ObjectStateManager 获取所有已更改实体的状态条目列表。对于每个已更改的状态条目，它调用 BeforeSaveChanges 方法，该方法负责在更改保存到数据库之前执行所有需要发生的特定于实体的操作。随着我们继续扩展 Entity Framework 的功能以解决现实世界的业务问题，此方法将会增长。然而，在这一点上，它仅负责已更改实体的验证。Validate 方法从 ObjectStateEntry 中提取实际实体并调用 Validator 类的熟悉的 ValidateObject 方法。如果实体对象无效，ValidateObject 方法会抛出 ValidationException，从而阻止 SaveChanges 方法将更改保存到数据库。

> **NOTE**
> 
> BeforeSaveChanges 方法有意*排除*已删除实体的验证，因为大多数规则不适用且会引起不必要的错误。第 9 章“实现业务逻辑”对此主题进行了详细讨论。

## 自定义 Entity Framework 代码生成

本书随附的示例项目中提供了在列表 8.1 中显示的 UnleashedObjectContext 类。它定义在名为 Unleashed.EntityFramework 的单独程序集中，并包含大量通用代码，任何 Entity Framework 应用程序都可以重用。虽然您可以简单地复制其代码，但您可能希望让 Entity Framework 上下文类，例如正在进行的示例中的 NorthwindEntities，继承自它 instead。这有助于将基础结构代码保留在应用程序之外，即使对于本书中讨论的示例实体模型也是有益的。

对于 Entity Framework 模型开发的数据库优先和模型优先方法，NorthwindEntities 类由 Entity Designer 生成。默认情况下，它继承自 ObjectContext。您无法直接更改其声明，因为任何修改在代码下次重新生成时都会丢失。相反，您需要更改代码生成器本身。本节展示了如何用文本模板替换内置的 Entity Framework 代码，该模板可以自定义以更改代码的生成方式。

> **NOTE**
> 
> 自定义 Entity Framework 生成的代码也可以解决其他常见问题。例如，第 9 章依赖于这种方法来向 Dynamic Data 提供有关实体属性默认值的信息。

## 用文本模板替换内置代码生成器

要替换 Entity Designer 使用的内置代码生成器，请右键单击设计表面并从上下文菜单中选择“添加代码生成项”。在“添加新项”对话框中（见图 8.1），选择 ADO.NET 实体对象生成器，并为其指定与 EDMX 文件名称匹配的名称。

> **NOTE**
> 文本模板的完整讨论超出了本书的范围。您可以在 http://www.olegsych.com/2007/12/text-template-transformation-toolkit 上找到有关此主题的详细信息。

您可以使用任何文本编辑器修改 TT 文件，例如随 Visual Studio 提供的编辑器。为了实现立即更改生成的 NorthwindEntities 基类的目标，请在模板中搜索单词 ObjectContext 并将其替换为 UnleashedObjectContext，如图 8.3 所示。当您保存 TT 文件时，其下的 Northwind.cs 会自动重新生成，并且 NorthwindEntities 类将继承自新的基类。

![](img/11b373b78859e17d318fd76939a0df9d_247_0.png)

图 8.3 在文本模板中更改上下文基类。

> **NOTE**
> Visual Studio 不为 TT 文件提供颜色语法高亮和 IntelliSense。您可以下载其中一个提供这些功能的第三方插件。图 8.3 显示了可在 http://www.devart.com/t4-editor 下载的 Devart T4 Editor。

## 自定义文本模板以生成静态构造函数

示例解决方案中的 Entity Framework 文本模板已进一步自定义，以自动为每个实体类型生成静态构造函数，如“使用 TypeDescriptor 注册元数据提供程序”部分所述。以下代码现在是生成类的<|message|> 部分，无需手工编码：
