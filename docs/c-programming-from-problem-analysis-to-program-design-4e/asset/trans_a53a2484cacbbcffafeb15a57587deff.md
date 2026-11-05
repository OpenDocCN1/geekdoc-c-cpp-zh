

![](img/36e48639a06772bcb0fa1ea2525b33a3_792_0.png)

![](img/36e48639a06772bcb0fa1ea2525b33a3_792_1.png)

![](img/36e48639a06772bcb0fa1ea2525b33a3_793_0.png)

### 图 11-21 添加到 StudentGov 示例的引用

请注意，除了 Visual Studio 自动添加的引用之外，`IFunding` 和 `Organization` 不包含其他引用。

`Club` 和 `FratSorority` 这两个类都必须添加对 `Organization` 和 `IFunding` 的引用。请记住，将 `using` 指令放在文件开头，可以让你在设计期间使用非限定的 `class` 名称来引用方法。`Club` 类的源代码如下：

```csharp
// Club.cs
using System;

// OrganizationNamespace added to avoid fully qualifying references.
using OrganizationNamespace;
using IFundingNamespace;

namespace ClubNamespace
{
    public class Club : Organization, IFunding
    {
        // Private member data
        private string meetingLocation;
        private string meetingDay;
        private string meetingTime;

        public Club(string name, string pContact,
                    string mLoc, string mDay, string mTime)
            // Call to base constructor
            : base(name, pContact)
        {
            meetingLocation = mLoc;
            meetingDay = mDay;
            meetingTime = mTime;
        }

        // Required method - because of interface
        public void SetFundingAmt()
        {
            FundedAmt = 600M;
        }
    }
}
```

在查看 Club、FratSorority 和 Intramural 类的代码时，请注意每个类都有一个构造函数，它调用 Organization `class` 中的 `base` 构造函数。它们为组织名称（orgName）和该团体的主要联系人（primaryContact）传递值。

来自 IFunding `interface` 的 SetFundingAmt() 方法在 Club 和 FratSorority 类中实现。FratSorority `class` 的源代码如下：

```csharp
// FratSorority.cs
using System;
using OrganizationNamespace;
using IFundingNamespace;

namespace FratSororityNamespace
{
    public class FratSorority : Organization, IFunding
    {
        private bool chartered; // Private member data
        private string houseAddress;

        public FratSorority()
        {
            houseAddress = "unknown";
            chartered = false;
        }

        public FratSorority(string name, string pContact,
                            bool isChartered, string address)
            : base(name, pContact)
        {
            // Call to base constructor
            houseAddress = address;
            chartered = isChartered;
        }

        // Required method - because of interface
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

        // Properties
        private bool Chartered
        {
            get
            {
                return chartered;
            }
            set
            {
                chartered = value;
            }
        }

        private string HouseAddress
        {
            get
            {
                return houseAddress;
            }
            set
            {
                houseAddress = value;
            }
        }
    }
}
```

最后一个类 PresentationGUI 用于测试这些组件。它是一个 GUI Windows 应用程序。请注意，图 11-21 显示为 PresentationGUI 类的每个组件都添加了引用。在这个类中，构造了 Club、FratSorority 和 Intramural 类的对象。PresentationGUI 类在一个 GroupBox 对象内包含三个 RadioButton 对象。这些单选按钮对应于正在构造的三种不同类型的组织对象。PresentationGUI 的创建方式与其他类类似，不同之处在于：向解决方案添加**新建项目**时，选择的是 **Windows 窗体应用程序**模板，而不是**类库**模板。该类的源代码清单如下。由于篇幅限制，省略了部分 Windows 窗体设计器生成的代码。表 11-2 显示了为窗体和控件对象设置了哪些属性，并且源代码中添加了额外注释，以帮助你理解该示例。

### 表 11-2 PresentationGUI 属性值

| 名称 | 对象类型 | 属性 | 属性值 |
| --- | --- | --- | --- |
| Form1 | Form | Name | PresentationGUI |
| PresentationGUI | Form | BackColor | Teal |
| PresentationGUI | Form | Font | 12F |
| PresentationGUI | Form | ForeColor | Yellow |
| PresentationGUI | Form | Text | 学生政府 |
| groupBox1 | GroupBox | Text | 选择组织类型 |
| radioButton1 | RadioButton | Name | radBtnIntr |
| radBtnIntr | RadioButton | Checked | false |
| radioButton2 | RadioButton | Name | radBtnFratSor |
| radBtnFratSor | RadioButton | Checked | false |
| radioButton3 | RadioButton | Name | radBtnClub |
| radBtnClub | RadioButton | Checked | false |
| radBtnIntr | RadioButton | Text | 校内团队 |
| radBtnFratSor | RadioButton | Text | 兄弟会/姐妹会 |
| radBtnClub | RadioButton | Text | 俱乐部 |
| label1 | Label | Name | lblName |
| label2 | Label | Name | lblFundedAmt |
| lblName | Label | Text | 名称： |
| lblName | Label | Visible | false |
| lblFundedAmt | Label | Text | 资助金额： |
| lblFundedAmt | Label | Visible | false |
| textBox1 | TextBox | Name | txtBxName |
| textBox2 | TextBox | Name | txtBxFund |
| txtBxFund | TextBox | TextAlign | Right |
| txtBxName | TextBox | Visible | false |
| txtBxFund | TextBox | Visible | false |

© 2013 Cengage Learning

最终项目的源代码清单如下所示。你会注意到，该清单展示了表示 `PresentationGUI.cs` 文件的 `partial class`。它没有显示 `PresentationGUI.Designer.cs` 文件的内容。`.Designer.cs` 文件包含自动生成的代码，并且可以像本书中所有其他示例一样从出版商处获取。

```csharp
// PresentationGUI.cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using ClubNamespace;           // Namespace for Club class
using IntramuralNamespace;    // Namespace for Intramural class
using FratSororityNamespace;   // Namespace for FratSorority class

namespace PresentationGUI
{
    public partial class PresentationGUI : Form
    {
        // Object of Club class declared
        private Club aClub;
        // Object of Intramural class declared
        private Intramural aTeam;
        // Object of FratSorority class declared
        private FratSorority aFratSorority;

        public PresentationGUI()
        {
            InitializeComponent();
        }

        // Objects are instantiated when the form is loaded.
        // Another GUI could be designed for entering data.
        private void PresentationGUI_Load(object sender,
                                          EventArgs e)
        {
            aClub = new Club
                ("ACM", "Jones", "Davis 203",
                 "Tues", "12:30");
            aFratSorority = new FratSorority
                ("Delta Pi", "Brenda Wynn",
                 true, "86 SmithField");
            aTeam = new Intramural
                ("Winners", "Joe Kitchen", "VolleyBall");
        }

        // Three CheckedChanged event-handler methods included.
        // Double-clicking on the RadioButton adds the method
        // heading and registers the event.
        private void radBtnClub_CheckedChanged(object sender,
                                               EventArgs e)
        {
            txtBxName.Text = aClub.OrgName;
            aClub.SetFundingAmt();
            txtBxFund.Text = aClub.FundedAmt.ToString("C");
            ShowDetails();
        }
    }
}
```

