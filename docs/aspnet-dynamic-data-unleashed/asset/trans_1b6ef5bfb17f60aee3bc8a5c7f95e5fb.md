

将 Supplier 实体的 SupplierID 属性的 int 值转换为 Join 方法所期望的 int? 类型，以便与 Product 实体的可为空的 SupplierID 属性兼容。使用 LINQ 表达式对象，可以这样构建此键选择器：

```
ParameterExpression parameter = Expression.Parameter(typeof(Supplier));
MemberExpression property = Expression.Property(parameter, "SupplierID");
UnaryExpression converted = Expression.Convert(property, typeof(int?));
LambdaExpression supplierKeySelector = Expression.Lambda(
    converted,
    parameter);
```

最后，resultSelector 参数是一个 lambda 表达式，它接受一个 Product 对象和一个 Supplier 对象作为参数，并返回 Product 对象。在原始查询中，该 lambda 表达式如下所示：(p, s) => p。使用 LINQ 表达式对象，可以这样构造此 lambda：

```
ParameterExpression product = Expression.Parameter(typeof(Product));
ParameterExpression supplier = Expression.Parameter(typeof(Supplier));
LambdaExpression resultSelector = Expression.Lambda(
    product, product, supplier);
```

> **注意**
> 
> Expression.Lambda 方法中参数的顺序有点令人困惑。lambda 表达式的主体作为第一个参数指定，后面跟着一个参数数组（C# 关键字 params），用于指定 lambda 表达式的参数。换句话说，参数的顺序与你直觉预期的相反。记住这一点，并在 Visual Studio 调试器中仔细检查每个表达式对象，可以帮助你在编写 LINQ 表达式时避免这个陷阱。

至此，你已经知道如何为 Queryable.Join 方法提供所有参数；剩下要做的就是构造方法调用本身。请记住，Join 运算符将由实体框架转换为 SQL，并由数据库服务器执行。换句话说，Join 扩展方法不会由应用程序本身调用，你需要将其构造为 MethodCallExpression 对象。你可以借助 Expression.Call 工厂方法（更具体地说，是这个特定的重载）来完成此任务：

```
public static MethodCallExpression Call(
    Type type,
    string methodName,
    Type[] typeArguments,
    params Expression[] arguments
)
```

type 参数表示你要调用其方法的类型，在示例中是 Queryable。methodName 参数是一个包含要调用的方法名称的字符串，在此示例中是 "Join"。typeArguments 是一个类型参数数组，.NET 运行时将使用它来创建泛型 Join 方法的特定实现。arguments 参数是一个 Expression 对象数组，表示将传递给方法的参数。使用之前构建的选择器，以下是在代码中创建 Join LINQ 表达式的方式：

```csharp
MethodCallExpression joinCall = Expression.Call(
    typeof(Queryable),
    "Join",
    new Type[] {
        typeof(Product),
        typeof(Supplier),
        typeof(int?),
        typeof(Product)
    },
    new Expression[] {
        productQuery.Expression,
        supplierQuery.Expression,
        productKeySelector,
        supplierKeySelector,
        resultSelector
    }
)
```

> **注意**
> 
> typeArguments 与 arguments 很容易混淆。由于 Expression.Call 方法定义了十几种不同的重载，这会导致编译器错误几乎没有意义，也无助于理解问题。在处理 MethodCallExpression 对象时，请记住，在泛型方法调用中，typeArguments 是放在 < > 之间的内容，而 arguments 是放在 ( ) 之间的内容。

使用表达式对象构造 LINQ 查询的最后一步是将 LINQ 表达式转换为 IQueryable 对象并替换原始查询。以下是在产品和供应商示例中完成此操作的方法：

```csharp
IQueryProvider queryProvider = productQuery.Provider;
productQuery = queryProvider.CreateQuery(joinCall);
```

在这里，你使用原始产品查询的 Provider 属性返回的 IQueryProvider 对象。IQueryProvider 接口定义了一个 CreateQuery 方法，该方法接受一个 lambda 表达式对象作为参数，并返回一个表示新查询的 IQueryable 对象。通过将 MethodCallExpression 传递给查询提供程序的 CreateQuery 方法，你可以创建一个新的 IQueryable（即新的 LINQ 查询），它返回 Product 和 Supplier 查询之间联接的结果。

> 注意
> 每个支持 LINQ 的框架（例如实体框架或 LINQ to SQL）都提供了自己的 IQueryProvider 实现，这使得同一段代码可以独立于底层数据访问技术来构造 LINQ 查询。

## 父筛选器模板中的查询逻辑

与上一节中硬编码类型和属性名称不同，父筛选器模板动态构建 Join 查询，依赖于描述外键列及其关联的子表和父表的元数据信息。不过，代码的结构与刚刚讨论的具体示例类似，你应该很容易理解。清单 12.9 显示了父筛选器模板的其余实现。它包括重写的 GetQueryable 方法以及用于构建所需 lambda 表达式的辅助方法：BuildChildKeySelector 和 BuildResultSelector。

对于筛选器模板，只有在用户实际在其控件中输入了搜索条件时才修改查询，这一点很重要。在阅读此代码时，请记住 childQuery 是由页面上的 EntityDataSource 控件创建的 IQueryable 对象（在示例中是 Product 查询）。请注意，代码如何通过调用描述父实体的 MetaTable 对象的 GetQuery 方法为父实体创建一个空查询（一个返回所有 Supplier 的查询）。这个空的父查询被传递给嵌套筛选器模板的 GetQueryable 方法。只有当它返回的查询与原始空查询不同时，父筛选器模板才会生成 Join 查询。如果嵌套筛选器模板返回了空查询，而没有父表的任何筛选条件，换句话说，如果用户没有为父表输入任何筛选条件，那么向子查询添加 Join 就没有必要，并且只会降低其速度。

> 注意
> 调用 MetaTable 对象的 GetQuery 方法，而不是直接使用 ObjectContext 的相应实体集属性（例如 Suppliers），这一点对于保持与动态数据体系结构的一致性非常重要。MetaTable 类的 GetQuery 方法是虚拟的，可以重写以实现第 14 章中讨论的行级安全性。同样重要的是，将前面讨论的 ContextCreated 事件处理程序收集的同一个 ObjectContext 传递给它，以确保联接中的两个查询来自同一个 ObjectContext。

### 清单 12.9 父筛选器模板（查询逻辑）

```
using System;
using System.Linq;
using System.Linq.Expressions;
using System.Web.DynamicData;
using System.Web.UI.WebControls;
```

```
namespace WebApplication.DynamicData.Filters
{
    public partial class ParentFilter : UnleashedFilterTemplate
    {
        public override IQueryable GetQueryable(IQueryable childQuery)
        {
            MetaTable parentTable = this.ForeignKeyColumn.ParentTable;
            IQueryable emptyQuery = parentTable.GetQuery(this.dataSourceContext);
            IQueryable parentQuery = this.filter.FilterTemplate.GetQueryable(emptyQuery);
            if (parentQuery != emptyQuery)
            {
                MetaTable childTable = this.ForeignKeyColumn.Table;
                MetaColumn childColumn = childTable.GetColumn(
                    this.ForeignKeyColumn.ForeignKeyNames[0]);
                MetaColumn parentColumn = parentTable.PrimaryKeyColumns[0];

                MethodCallExpression joinCall = Expression.Call(
                    typeof(IQueryable),
                    "Join",
                    new Type[] {
                        childQuery.ElementType,
                        parentQuery.ElementType,
                        childColumn.EntityTypeProperty.PropertyType,
                        childQuery.ElementType
                    },
                    new Expression[] {
                        childQuery.Expression,
                        parentQuery.Expression,
                        BuildChildKeySelector(childQuery.ElementType, childColumn.Name),
                        BuildParentKeySelector(parentQuery.ElementType, parentColumn.Name,
                            childColumn.EntityTypeProperty.PropertyType),
                        BuildResultSelector(childQuery.ElementType, parentQuery.ElementType)
                    });

                childQuery = childQuery.Provider.CreateQuery(joinCall);
            }

            return childQuery;
        }

        private static LambdaExpression BuildChildKeySelector(
            Type entityType, string propertyName)
        {
            ParameterExpression parameter = Expression.Parameter(entityType, "child");
            MemberExpression property = Expression.Property(parameter, propertyName);
```

