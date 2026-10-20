
```csharp
// The root page of your application
MainPage = new ScalePage();
}
```

运行程序，你会看到类似下面的界面：

![](img/affff2e3b09de80cc0ffe811bbf63f5d_89_0.png)

## 结论：

在本课中，我们讨论了基本的工程变换：平移、旋转、缩放，以及如何通过 Xamarin 处理它们。事实上，这类变换的需求通常出现在游戏或图形应用程序中。在本系列的后续课程中，我们将应用其中一些变换。

## 使用 Xamarin 构建联系人应用

1

在本章中，我们将开始构建一个具有高技术标准的实用应用程序。我们将使用前几课学到的知识来构建一个简单的联系人应用程序，但它使用了相对高级的技术和概念。

我们将分三个连续的部分来介绍这个应用程序，以下是各部分内容的简要描述：

**第一部分：** 解释应用程序的目的，并阐明仓库（Repository）模型在构建应用程序中的思想，同时构建应用程序的整体结构，这是本课的内容。
**第二部分：** 装备仓库的功能方面，使其可用。
**第三部分：** 实现用于显示详细信息的主界面和子界面。以及两个界面之间移动过程的实现。

## 应用程序的目的及其工作原理

应用程序的思路非常简单，归结为显示已有的联系人并支持在其中搜索，同时能够添加、编辑和删除新联系人。应用程序依赖于两个界面。第一个界面是主界面，包含一个按姓名或昵称搜索任何已有联系人的区域，此外还有一个列表用于显示搜索结果中的联系人，最后还有一个用于添加新联系人的按钮。下图显示了在未指定搜索条件时按下 FIND 的结果：

![](img/affff2e3b09de80cc0ffe811bbf63f5d_91_0.png)

当用户未指定任何条件点击 FIND 按钮时，应用程序将显示其拥有的所有联系人，在此版本的程序中，这些联系人将是应用程序内存中的模拟数据。当用户指定姓名或昵称时，应用程序将使用 AND 逻辑进行搜索。

至于第二个界面，当用户点击之前列表中的某个联系人时出现，该界面显示此联系人的详细数据：姓名、昵称、电话号码、电子邮件地址和爱好。见下图：

![](img/affff2e3b09de80cc0ffe811bbf63f5d_92_0.png)

可以修改这些数据中的任何一项，然后用户单击保存按钮进行保存，或者如果不想修改数据，可以单击顶部程序图标旁边的返回上一界面按钮。用户还可以通过单击上图所示的“删除”按钮来删除此联系人。简而言之，这就是实现思路。

## 仓库（Repository）模式

随着应用程序规模的增长和所需任务的多样化，需要一种在应用程序内组织工作的方式。事实上，Xamarin 为此支持许多模型，例如 MVVM 模型，它在 Xamarin 中被有效用于组织和分离负责界面的部分、负责业务逻辑的部分以及负责处理各种类型远程或本地数据服务器的部分。

我个人喜欢的模型之一是 Repository，我在正在开发的各种应用程序中广泛使用它。这是一种优美且合理的方法，允许应用程序平滑快速地开发以适应各种类型的环境，并且它与 MVVM 模型兼容。

仓库模型允许将负责处理数据的代码与业务逻辑隔离开。这样做有几个好处，其中最重要的是：

-   组织程序，使其更易于理解和开发。
-   开发数据处理方法，而无需对程序逻辑做任何更改。
-   能够彻底改变用于存储数据的服务类型，而业务逻辑几乎不需要改变。

我将直接介绍如何在我们应用程序中采用这种模型。我们需要使用一个接口和一个相应的实现类。关于外观模式（facades），如果你想回顾一下，请参阅这一课。现在让我们在下一段开始构建这个应用。

## 构建应用程序

首先创建一个名为 ContactsApp 的新 Blank App（Xamarin.Forms Portable）项目，然后像我们在本课中所做的那样，只保留 ContactsApp（Portable）和 ContactsApp.Droid 项目。

在“解决方案资源管理器”窗口中，右键单击 ContactsApp 项目，从出现的菜单中选择“添加”，然后从子菜单中选择“新建文件夹”以添加新文件夹。将此文件夹命名为 Entity，当它出现在解决方案资源管理器中后，右键单击它，选择“添加”，然后从子菜单中选择“类”。将出现一个窗口，允许你为此项指定名称。选择名称 Contact。这个类是该程序的主要构建块，并代表了其中的工作逻辑。请确保 Contact.cs 文件的内容如下：

```
namespace ContactsApp.Entities
{
    public class Contact
    {
        public int Id {get; set;}
        public string FirstName {get; set;}
        public string LastName {get; set;}
        public string Tel {get; set;}
        public string EMail {get; set;}
        public string Hobbies {get; set;}

        public override string ToString ()
        {
            return string.Concat (FirstName, "" " , LastName);
        }
    }
}
```

从上图可以看出，Contact 类包含任何联系人所需的基本数据，外加一个对联系人来说可能有点奇怪的爱好功能。

再次右键单击 ContactsApp 项目，从出现的列表中选择“添加”，然后从子菜单中选择“新建文件夹”以添加新文件夹。将此文件夹命名为 Abstract，当它出现在解决方案资源管理器中后，右键单击它，选择“添加”，然后从子菜单中选择“新建项”。将出现一个窗口，允许你指定要添加的项类型。选择“接口”并将其命名为 IContactsRepository。

确保 IContactsRepository.cs 文件的内容如下：

```
using System.Threading.Tasks;
using System.Collections.ObjectModel;
using ContactsApp.Entities;

namespace ContactsApp.Abstract
{
    public interface IContactsRepository
    {
        Task<ObservableCollection<Contact>> GetContactsAsync (string firstName, string lastName);

        Task<bool> AddContactAsync (Contact contactToAdd);

        Task<bool> UpdateContactAsync (Contact contactToUpdate);

        Task<bool> DeleteContactAsync (Contact contactToDelete);
    }
}
```

接口通常用于当我们想要提取抽象并将其公开时，这极大地有益于使软件代码更易于理解和重用。这就是为什么这个接口被添加到 Abstract 文件夹中。接口不包含任何软件代码，如我们所知，它包含的只是任何希望实现该接口的类必须满足的依赖契约。这个接口简要包含我们的应用完成任务所需的基本操作：按姓名和昵称获取联系人 GetContactsAsync，添加新联系人 AddContactAsync，更新现有联系人 UpdateContactAsync，以及删除联系人 DeleteContactAsync。每个函数名称中带有 Async 的原因是为了表明你应该使用我们在本课中讨论过的异步编程技术。有趣的是，这个接口不关心数据的位置，也不关心如何获取和处理数据。它们只关心应用需要什么，仅此而已。

我们现在重复同样的过程，在 ContactsApp.cs 项目中添加一个名为 Concrete 的新文件夹，该文件夹将包含实现之前 IContactsRepository 接口的项。右键单击此文件夹并选择“添加”。从子菜单中选择“类”。将此项命名为 MemoryContactsRepository，并确保其内容如下：

```
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using System.Collections.ObjectModel;
using ContactsApp.Abstract;
using ContactsApp.Entities;

namespace ContactsApp.Concrete
{
    public class MemoryContactsRepository: IContactsRepository
    {
        private ObservableCollection<Contact> contacts;

        public MemoryContactsRepository()
        {
            contacts = new ObservableCollection<Contact>()
        {
```

