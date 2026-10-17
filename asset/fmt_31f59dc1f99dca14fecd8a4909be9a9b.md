
![](img/45e6f245af31396d967c3186f196d331_725_0.png)

图 11-18 StudentGov示例的问题规格

### 分析问题

你应该查看图 11-18 中的问题规格，以确保你理解了问题定义。以下类型的组应该能够被实例化：

- 社团（Club）
- 兄弟会与姐妹会（Fraternity and sorority）
- 校内活动（Intramural）

这些小组具有一些共同特征。每个小组都有唯一的名称和联系人。其中两个小组（社团、兄弟会和姐妹会）可能会收到学生会的资助。获得特许的兄弟会姐妹会获得资助；其他的则不能。

关于社团的唯一信息包括举行会议的日期、时间和地点。校内小组相关的运动类型是校内分类特有的。兄弟会或姐妹会分类的独特特征包括小组是否获得特许以及它们的宿舍地址。在理解问题定义后，你可以开始抽象出每个类的特征。表 11-1 显示了按小组组织的数据字段。通用数据包含在 `Organization`（组织）类别中。

## 表 11-1 按类组织的数据字段

| 类 | 标识符 | 数据类型 |
| :--- | :--- | :--- |
| `Organization` | `orgName` | string |
| `Organization` | `primaryContact` | string |
| `Organization` | `fundedAmt` | decimal |
| `Club` | `meetingDay` | string |
| `Club` | `meetingTime` | string |
| `Club` | `meetingLocation` | string |
| `FratSorority` | `chartered` | bool |
| `FratSorority` | `houseAddress` | string |
| `Intramural` | `sportType` | string |

除非与社团、兄弟会、姐妹会或校内小组相关，否则在此应用程序中不应创建小组。

### 设计解决方案

预期输出是在 Windows 表单上显示关于不同组织的数据。使用 Windows Form 类创建一个应用程序来测试该设计。它应该确保可以从 `Club`、`FraternitySorority` 和 `Intramural` 类实例化对象，但不能从 `Organization` 类实例化。它应该确保派生类可以访问基类的成员。图 11-19 显示了表单的原型。

![](img/45e6f245af31396d967c3186f196d331_727_0.png)

**图 11-19** StudentGov示例的原型

业务逻辑分为几个类，包含一个作为基类的 `Organization` 类。不应从该类实例化任何对象，因此将其定义为抽象类。定义了 `Club`、`Intramural` 和 `FraternitySorority` 的派生类以继承 `Organization` 类。定义了 `IFunding` 接口以强制设置资助金额的功能。`FraternitySorority` 和 `Club` 都实现了此接口。

使用类图帮助设计和记录这些特征。图 11-20 显示了 StudentGov 示例的类图。

# 编程示例：StudentGov 应用

| `Organization` | `PresentationGUI` |
| :--- | :--- |
| +interface | +Club: string |
| +primaryContact string | +Fraternity: string Fraternity string |
| +funded(Amt): decimal | +Team: Intramural |
| +SelfFunding(Amt): void | +PresentationGUI(GUI Form) |
| | +addClub(CheckChanged): void |
| | +addFraternity(CheckChanged): void |
| | +ShowDetails(void): void |
| `Club` | `Fraternity` | `Intramural` |
| :--- | :--- | :--- |
| +meetingLocation: string | +chartered: bool | sportType: string |
| +meetingDay: string | +houseAddress: string | +SelfFunding(Amt): void |
| +meetingTime: string | | |
| +SelfFunding(Amt): void | | |

图 11-20 StudentGov 的类图

图 11-20 中的虚线表示接口链接。注意统一建模语言（UML）对接口的表示法包含*斜体*表示的方法名称，这表示必须定义实现细节。

> UML 是用于规范和记录数据及过程行业标准建模语言。类图是面向对象方法使用的建模图之一。要了解更多关于 UML 的信息，请访问 www.uml.org，这是发布它的对象管理组网站。

接口对象不能有成员数据，只能有方法。类图没有显示属性。没有为访问或更改类的私有数据成员定义访问器（accessor）或修改器（mutator）方法。但在设计过程中，决定为大多数数据成员定义具有 get 和 set 行为的属性。此应用程序只需要的业务逻辑；因此没有构建伪代码或额外的设计工具。

编写解决方案在你完成设计后，是时候将设计转换为源代码了。对于此应用程序，解决方案内部创建了六个项目。`PresentationGUI` 生成 EXE 文件；所有其他项目以 `.dll` 结尾。

首先创建 `Organization` 类。构建 DLL 以便其他类引用它。`Organization` 类的源代码所示：

```csharp
// Organization.cs
// 作为基类的抽象类
using System;
namespace OrganizationNamespace
{
    public abstract class Organization
    {
        private string orgName;
        private string primaryContact;
        private decimal fundedAmt;

        public Organization(string name, string contact)
        {
            orgName = name;
            primaryContact = contact;
            fundedAmt = 0M;
        }

        public Organization()
        {
            orgName = "unknown";
            primaryContact = "unknown";
            fundedAmt = 0M;
        }

        // 每个数据成员的属性。
        public decimal FundedAmt
        {
            set
            {
                fundedAmt = value;
            }
            get
            {
                return fundedAmt;
            }
        }

        public string OrgName
        {
            set
            {
                orgName = value;
            }
        }
    }
}
```

```csharp
get
{
    return orgName;
}
private string PrimaryContact
{
    set
    {
        primaryContact = value;
    }
    get
{
        return primaryContact;
    }
}
```

接下来创建包含接口的文件。与 `Organization` 类一样，它是一个独立组件。使用 Visual Studio 中的类库模板，向解决方案添加了以下源代码：

```csharp
// IFunding.cs · interface
using System;
namespace IFundingNamespace
{
    public interface IFunding
    {
        // SetFundingAmt() 没有实现细节。
        // 方法必须由实现接口的类定义。
        void SetFundingAmt();
    }
}
```

可以从解决方案资源管理器（Solution Explorer）窗口向解决方案添加新的接口项目。右键点击解决方案图标，然后选择“添加新项目”（Add New Project）。

`Intramural` 类继承自 `Organization` 类，但没有实现该接口。要在 `Intramural` 项目中使用 `Organization` 组件，必须在编写程序语句之前对该 DLL 建立引用。

记住，添加引用的一种方法是在解决方案资源管理器窗口中选择项目，并从项目菜单栏中选择“添加引用”（Add Reference）。由于每个组件都存储为单独的项目，请务必浏览项目子目录，以在 `bin\debug` 目录中定位 DLL。

还添加了 `using OrganizationNamespace;` 语句，以消除对 `Organization` 类完全限定引用引用。`Intramural` 类的源代码显示所示：

```csharp
// Intramural.cs
using System;

// 添加 OrganizationNamespace 以避免使用完全限定引用。
using OrganizationNamespace;

namespace IntramuralNamespace
{
    public class Intramural : Organization
    {
        private string sportType;

        public Intramural(string name, string pContact, string sport)
            : //(调用 Organization (base) 类构造函数)
            base(name, pContact)
        {
            sportType = sport;
        }

        // 默认构造函数
        public Intramural()
        {
            sportType = "unknown"
        }
        // sportType 的属性
    }
}
```

图 11-21 为 StudentGov 示例添加的引用

注意，`IFunding` 和 `Organization` 除了 Visual Studio 自动添加的引用外，没有额外的引用。`Club` 和 `FratSorority` 类都添加对 `Organization` 和 `IFunding` 的引用。记住，将 `using` 指令放在文件开头允许你在设计期间使用未完全限定的类名来引用方法。

`Club` 类的源代码如下：

```csharp
// Club.cs
using System;

// 添加 OrganizationNamespace 以避免使用完全限定引用。
using OrganizationNamespace;
using IFundingNamespace;

namespace ClubNamespace
{
    public class Club : Organization, IFunding
    {
        // 私有成员数据
        private string meetingLocation;
        private string meetingDay;
        private string meetingTime;

        public Club(string name, string pContact,
                    string mloc, string mDay,
                    string mTime)
            : base(name, pContact)
            // 调用基构造函数
        {
            meetingLocation = mLoc;
            meetingDay = mDay;
            meetingTime = mTime;
        }

        // 因为接口而需要实现的方法
        public void SetFundingAmt()
        {
            FundedAmt = 600M;
        }
    }
}
```

在查看 `Club`、`FratSorority` 和 `Intramural` 类的代码时，请注意每个类都有一个调用 `Organization` 类中基构造函数的构造函数。它们发送了用于组织名称（`orgName`）和小组主要联系人（`primaryContact`）的值。来自 `IFunding` 接口的 `SetFundingAmt()` 方法在 `Club` 和 `Sorority` 类中实现。`Sorority` 类的源代码如下：

```csharp
// Sorority.cs
using System;
using OrganizationNamespace;
using IFundingNamespace;

namespace SororityNamespace
{
    public class Sorority : Organization, IFunding
    {
        private bool chartered; // 私有成员数据
        private string houseAddress;

        public Sorority()
        {
            houseAddress = "unknown";
            chartered = false;
        }

        public Sorority(string name, string pContact,
            bool isChartered, string address)
            : base(name, pContact) // 调用基构造函数
        {
            houseAddress = address;
            chartered = isChartered;
        }

        // 因为接口而需要实现的方法
        public void SetFundingAmt()
        {
            if(chartered)
            {
                FundedAmt = 500M;
            }
            else
            {
                FundedAmt = 0M;
            }
        }

        // 属性
        public bool Chartered
        {
            get { return chartered; }
            set { chartered = value; }
        }
        public string HouseAddress
        {
            get { return houseAddress; }
            set { houseAddress = value; }
        }
    }
}
```

最后一个类 `PresentationGUI` 用于测试这些组件。注意图 11-21 显示为 `PresentationGUI` 类为每个组件都添加了引用。在类类中，`PresentationGUI` 在 `GroupBox` 对象内部包含三个 `RadioButton` 对象。这些单选按钮对应于正在构造的三个不同的组织对象。由于空间限制，省略了部分 Windows Forms 生成的代码。表 11-2 显示了为 Form 和控件对象设置了哪些属性，源代码中添加了额外的注释以帮助你理解示例。

## 表 11-2 PresentationGUI 值

| 名称 (Name) | 对象类型 (Object type) | 属性 (Property) | 值 (Value) |
| :--- | :--- | :--- | :--- |
| `PresentationGUI` | Form | BackColor | Teal |
| `PresentationGUI` | Form | Font | 12F |
| `PresentationGUI` | Form | Fore | Yellow |

## 11-2 PresentationGUI 值（续）

| 对应 (Name) | 对象类型 (Object Type) | 属性 (Property) | 值 (Value) |
| :--- | :--- | :--- | :--- |
| `PresentationGUI` | Form | Text | Student Government |
