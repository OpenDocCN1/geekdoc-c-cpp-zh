
```csharp
static Product()
{
    TypeDescriptor.AddProviderTransparent(
        new AssociatedMetadataTypeTypeDescriptionProvider(typeof(Product)),
        typeof(Product));
}
```

图8.4显示了文本模板被修改的位置。注意`WriteStaticConstructor`方法调用被添加到了负责生成实体类型声明的模板代码中。该方法在示例解决方案的Northwind.tt文件中的这个方法的末尾实现。

![](img/11b373b78859e17d318fd76939a0df9d_248_0.png)

图8.4 在文本模板中生成静态构造函数。

## 自动化测试

由于其重要性和相对较低的变更频率，业务逻辑总体上是自动化测试的理想候选，特别是验证逻辑。将业务逻辑封装在由实体框架部分生成的上下文和实体类中，可以直接在业务层面进行有针对性的测试。与通过用户界面进行测试不同——用户界面测试依赖于特定的表示层（如ASP.NET WebForms），并且通常需要手动测试或使用专用工具——业务层面的测试可以通过应用程序的内部API配合通用框架（如NUnit或Visual Studio单元测试框架）来完成。

自动化测试是你可以用来改进和维护应用程序质量的最强大工具之一。然而，像许多昂贵而强大的工具一样，自动化测试很难经济高效地应用。许多团队和个人开发者尝试过自动化测试，却发现实施和维护测试所需的大量额外工作并不能证明感知到的质量改进是合理的。在许多情况下，这些尝试失败了，因为开发者试图应用那些旨在解决一些大型软件应用程序和框架的算法复杂性的“最佳实践”。这些实践无法缩小到大多数信息系统的需求，这些系统最大的挑战是领域的大小（数据库中的表数量、人工工作流数量等），而不是其单个算法的复杂性。

虽然自动化测试的主题太大，无法在此详细讨论，但本节介绍了一种可以用于开始学习的实用方法。为了强调业务逻辑自动化测试的重要性，并证明其在应用程序开发项目中的实用价值，本章其余部分的代码示例以自动化测试的形式演示了验证逻辑。

### 创建单元测试

要在项目中开始实施自动化测试，首先需要创建一个测试项目。在大多数情况下，你希望自动化测试位于单独的程序集中，以避免将它们部署到生产环境中。本示例使用Visual Studio单元测试框架，该框架在所有版本（Express除外）中均可用。Visual Studio提供了特殊的项目模板，你可以使用图8.5中显示的“添加新项目”对话框来选择它。按照惯例，测试项目与被测项目同名，后跟.Tests后缀。在本例中，被测项目是DataModel，NorthwindEntities上下文类和实体类都定义在该项目中，因此测试项目名为DataModel.Tests。

![](img/11b373b78859e17d318fd76939a0df9d_249_0.png)

图8.5 向解决方案中添加新的测试项目。

![](img/11b373b78859e17d318fd76939a0df9d_251_0.png)

图8.6 向项目中添加新的单元测试。

现在你可以创建第一个测试（即测试方法），以验证Product实体的UnitPrice属性在实体实例保存到数据库时是必需的。清单8.2展示了此测试的完整实现。如你所见，测试方法名为UnitPrice_IsRequired，其中下划线用作被测属性名称与测试本身描述之间的分隔符。由于你可能针对同一属性拥有多个测试，使用下划线有助于将测试方法组织成逻辑组。

**清单8.2 测试Product实体的必需UnitPrice属性**

```csharp
using System.ComponentModel.DataAnnotations;
using System.Transactions;
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace DataModel
{
    [TestClass]
    public class ProductTest
    {
        [TestMethod]
        [ExpectedException(typeof(ValidationException))]
        public void UnitPrice_IsRequired()
        {
            using (new TransactionScope())
            using (NorthwindEntities context = new NorthwindEntities())
            {
                var product = new Product();
                product.UnitPrice = null;
                context.Products.AddObject(product);
                context.SaveChanges();
            }
        }
    }
}
```

该测试创建一个新的NorthwindEntities上下文对象，并尝试在没有有效UnitPrice的情况下向数据库提交一个新的Product实例。你期望SaveChanges方法抛出ValidationException，这就是为什么对测试方法应用了ExpectedException属性。如果此测试方法抛出预期的异常，Visual Studio会报告成功。如果测试没有抛出异常或抛出了意外类型的异常，则会报告失败。

你可以借助图8.7所示“测试视图”窗口运行此测试以及此测试项目中定义的所有其他测试。你可以在Visual Studio主菜单的“测试”窗口下找到它。

![](img/11b373b78859e17d318fd76939a0df9d_252_0.png)

图8.7 使用“测试视图”窗口运行测试。

测试执行结果显示在“测试结果”窗口中（见图8.8）。

![](img/11b373b78859e17d318fd76939a0df9d_252_1.png)

图8.8 在“测试结果”窗口中检查执行结果。

### 测试隔离

封装不良可能导致以前成功完成的测试失败。这是开发人员放弃自动化测试的最常见原因之一。请注意，在清单8.2所示的测试中，围绕NorthwindEntities上下文的TransactionScope是

```csharp
if (memberNames != null && memberNames.Contains(this.MemberName))
    return;

string message = "ValidationException was expected";
message += " with member name " + this.MemberName;
message += ". Instead " + exception.GetType().FullName + " was thrown";
if (memberNames != null && memberNames.Any())
    message += " with member name(s) " + string.Join(", ", memberNames);
message += ".";
throw new AssertFailedException(message);
}
}
```

自定义断言属性继承自基类ExpectedExceptionBaseAttribute，该基类由Visual Studio单元测试框架在Microsoft.VisualStudio.TestTools.UnitTesting命名空间中提供。它定义了一个名为MemberName的属性，该属性指定期望出现ValidationException的属性名称。ExpectedValidationExceptionAttribute还重写了Verify方法，该方法接收测试方法抛出的实际异常，并在实际异常不是ValidationException或指定了意外的MemberName时抛出AssertFailedException。

### 集成测试与单元测试对比

熟悉自动化测试的开发人员会很快指出，使用此处描述的方法创建的测试是集成测试，而不是单元测试。测试纯粹主义者经常对这种将业务和数据访问逻辑一起测试的做法皱眉，理由是测试及其结果的精度、性能和可靠性不高。按照设计，集成测试不如单元测试精确，因为它们涉及多个代码单元，可能无法让你区分由数据访问错误导致的测试失败和由业务逻辑错误导致的测试失败。由于集成测试访问外部数据库，它们比仅访问内存中对象的单元测试慢。如果实现不当，集成测试可能依赖于共享的测试数据，从而导致不正确或不可重复的测试执行结果。

从理论上讲，使用纯单元测试单独测试业务逻辑，与数据访问逻辑分开，可以提高测试的精度、性能和可靠性。采用这种方法，需要用测试替身（如存根或模拟对象）替代数据访问逻辑，使您能够区分业务逻辑错误和数据访问错误。然而，在提高测试精度的同时，也降低了测试覆盖率。仅靠业务逻辑的单元测试，当数据访问层出现问题导致故障时，您无法得知；而在使用对象关系映射器（如实体框架）创建的应用程序中，数据访问层问题更为常见。针对这个问题的规范答案是，除了业务逻辑的单元测试外，您还应该为数据访问创建单元测试。在实践中，使用...创建的自动化测试的数量和复杂性
