
![](img/36e48639a06772bcb0fa1ea2525b33a3_792_0.png)

![](img/36e48639a06772bcb0fa1ea2525b33a3_792_1.png)

![](img/36e48639a06772bcb0fa1ea2525b33a3_793_0.png)

### FIGURE 11-21 References added to StudentGov example

Notice that `IFunding` and `Organization` contain no additional references beyond those automatically added by Visual Studio.

Both the `Club` and `FratSorority` classes must add references to `Organization` and `IFunding`. Remember that placing the `using` directive at the beginning of the file allows you to use the unqualified `class` names to reference methods during design. The source code for the `Club` class follows:

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

As you review the code for the Club, FratSorority, and Intramural classes, notice that each one has one constructor that calls the `base` constructor in the Organization `class`. They send values for the organization name (orgName) and the primary contact person for the group (primaryContact).

The SetFundingAmt() method from the IFunding `interface` is implemented in the Club and FratSorority classes. The source code for the FratSorority `class` follows:

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

The last class, PresentationGUI, is used to test the components. It is a GUI Windows application. Notice that Figure 11-21 shows that a reference is added to each of the components for the PresentationGUI class. In this class, objects are constructed of the Club, FratSorority, and Intramural classes. The PresentationGUI class includes three RadioButton objects inside a GroupBox object. The radio buttons correspond to the three different types of organization objects being constructed. The PresentationGUI is created similarly to the other classes, except instead of using the **Class Library** template when the **New Project** is added to the solution, the **Windows Forms Application** template is selected. The source listing for this class follows. Due to space constraints, some of the Windows Forms Designer generated code is omitted. Table 11-2 shows what properties are set for the Form and control objects, and extra comments are added to the source code to aid you in following the example.

### TABLE 11-2 PresentationGUI property values

| Name | Object type | Property | Property value |
| --- | --- | --- | --- |
| Form1 | Form | Name | PresentationGUI |
| PresentationGUI | Form | BackColor | Teal |
| PresentationGUI | Form | Font | 12F |
| PresentationGUI | Form | ForeColor | Yellow |
| PresentationGUI | Form | Text | Student Government |
| groupBox1 | GroupBox | Text | Select organization type |
| radioButton1 | RadioButton | Name | radBtnIntr |
| radBtnIntr | RadioButton | Checked | false |
| radioButton2 | RadioButton | Name | radBtnFratSor |
| radBtnFratSor | RadioButton | Checked | false |
| radioButton3 | RadioButton | Name | radBtnClub |
| radBtnClub | RadioButton | Checked | false |
| radBtnIntr | RadioButton | Text | Intramural team |
| radBtnFratSor | RadioButton | Text | Fraternity/Sorority |
| radBtnClub | RadioButton | Text | Club |
| label1 | Label | Name | lblName |
| label2 | Label | Name | lblFundedAmt |
| lblName | Label | Text | Name: |
| lblName | Label | Visible | false |
| lblFundedAmt | Label | Text | Funding Amt: |
| lblFundedAmt | Label | Visible | false |
| textBox1 | TextBox | Name | txtBxName |
| textBox2 | TextBox | Name | txtBxFund |
| txtBxFund | TextBox | TextAlign | Right |
| txtBxName | TextBox | Visible | false |
| txtBxFund | TextBox | Visible | false |

© 2013 Cengage Learning

The final project source code listing is shown next. You will notice that the listing shows the `partial class` representing the `PresentationGUI.cs` file. It does not show the contents of the `PresentationGUI.Designer.cs` file. The `.Designer.cs` file contains the auto-generated code and is available like all the other examples in the book from the publisher.

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
