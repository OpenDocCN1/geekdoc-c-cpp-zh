
as users, computers, or groups, in the group. You can also include users, computers, and group from any domain in a forest or from any trusted domain in the domain. A domain local group can be a member of other domain local group.

- Global – Refers to a group of domain objects that are based on business roles. You can define a global group in the domain naming context. A global group can include users, computers, and other global groups. It is available for use by all domain members as well as other domains in a forest and all trusted external domains. The global group is the most preferred group as it has the broadest availability across the domain, forest and the trusting domain.

- Universal – Refers to a group that contains members of multiple domains of a forest. A universal group can include users, global groups, and other universal groups from any domain in the forest. It can be a member of a universal group or domain local group. Universal groups help you to represent and consolidate groups that span domains in a forest and help you to define rules that are applicable across the forest.

6. Click the OK button to create the group.

After creating a group, you can change the group’s scope and type by using the General tab of the Properties dialog box. You can change the group scope in one of the following ways:

- Global to Universal
- Domain local to Universal
- Domain local to Global
- Universal to Global
- Universal to Domain Local

Next, let’s learn how to access AD through a Windows Forms application.

## Accessing Active Directory from a Windows Forms Application

Visual Studio 2010 allows you to create a Windows Forms application that can access AD in a specific domain controller, using username and password. Let’s create a Windows Forms application, named WorkingwithActiveDirectory (also available on the CD) to access the members of an AD of Windows Server 2008. Using the WorkingwithActiveDirectory application, you can add new users or modify the existing users in AD. Perform the following steps to create a Windows Forms application, named WorkingwithActiveDirectory:

1. Open Visual Studio 2010 IDE.
2. Select the File→New→Project option. The New Project dialog box appears (Figure 37.2).
3. Select the Installed Templates→Visual C#→Windows Forms Application template. Enter a name and location in the Name and Location text boxes, respectively. In our case, the project name is WorkingwithActiveDirectory and the project location is D:\Black Books\C# 2010\Chapter 37\, as shown in Figure 37.2.

![](img/e073a4882197be4ab61103cbe0bcb394_1751_0.png)

Figure 37.2: Creating the WorkingwithActiveDirectory Project

4. Click the OK button. The WorkingwithActiveDirectory project appears in Visual Studio 2010 IDE.

5. Modify the Text property of the Form1 form to Manipulating Users.

6. Add seven Label controls, four TextBox controls, three Button controls, and one ListBox control to Form1, and modify the properties and placement of controls on Form1, as shown in Figure 37.3:

![](img/e073a4882197be4ab61103cbe0bcb394_1752_0.png)

### Figure 37.3: Showing the Design View of Form1

> NOTE
> In Figure 37.3, the Text property of the label6 and label7 controls is blank; therefore, it is not visible at design time. However, you can see the placement of the label6 and label7 controls during the execution of the WorkingwithActiveDirectory application.

7. Add the code, given in Listing 37.1, in the code of the Form1.cs file of the WorkingwithActiveDirectory application:

### Listing 37.1: Showing the Code of the WorkingwithActiveDirectory Application:

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.DirectoryServices;
using System.Net;

namespace WorkingwithActiveDirectory
{
    public partial class Form1 : Form
    {
        DirectoryEntry entry = new DirectoryEntry("LDAP://192.168.1.95");
        string a = null;
        bool status;

        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            try
            {
                if (status == true)
                {
                    label3.Visible = true;
                    textBox3.Visible = true;
                    textBox1.Enabled = true;
                    DirectoryEntries users = entry.Children;
                    DirectoryEntry user = users.Add("CN=" + textBox1.Text, "user");
                    user.Properties["userPassword"].Add(textBox2.Text);
                    user.Properties["company"].Add(textBox3.Text);
                    user.Properties["department"].Add(textBox4.Text);
                    if (textBox1.Text == "" || textBox2.Text == "" || textBox3.Text == "" || textBox4.Text == "")
                    {
                        SetBlank();
                    }
                    else
                    {
                        user.CommitChanges();
                        label6.Text = "User details added successfully.";
                        //GetInformation();
                    }
                }
            }
            catch (Exception ex)
            {
                label6.Text = "user already exists. Please add a different user.";
            }
        }

        private void button2_Click(object sender, EventArgs e)
        {
            entry.Path = "LDAP://192.168.1.95/CN=" + a + ",CN=Users,DC=sql,DC=local";
            entry.Username = "administrator@sql.local";
            entry.Password = "kogent@321";
            if (entry.Properties.Contains("company"))
            {
                entry.Properties["company"][0] = textBox3.Text;
            }
            else
            {
                entry.Properties["company"].Add(textBox3.Text);
            }
            if (entry.Properties.Contains("department"))
            {
                entry.Properties["department"][0] = textBox4.Text;
            }
            else
            {
                entry.Properties["department"].Add(textBox4.Text);
            }

            entry.CommitChanges();
            label6.Text = "User details modified successfully.";
            EstablishConnection();
        }

        private void button3_Click(object sender, EventArgs e)
        {
            GetInformation();
        }
        private void SetBlank()
        {
            textBox1.Clear();
            textBox2.Clear();
            textBox3.Clear();
            textBox4.Clear();
            label6.Text = "";
        }
        private void GetInformation()
        {
            listBox1.Items.Clear();
            using (DirectorySearcher searcher = new DirectorySearcher())
            {
                searcher.SearchRoot = entry;
                SearchResultCollection results = searcher.FindAll();
                foreach (SearchResult result in results)
                {
                    ResultPropertyCollection props = result.Properties;
                    foreach (string propName in props.PropertyNames)
                    {
                        if (propName == "name")
                        {
                            listBox1.Items.Add(props[propName][0]);
                        }
                    }
                }
                status = true;
            }
        }

        private void listBox1_Click(object sender, EventArgs e)
        {
            SetDetails();
        }

        private void SetDetails()
        {
            SetBlank();
            textBox1.Enabled = false;
            button2.Enabled = true;
            using (DirectorySearcher searcher = new DirectorySearcher())
            {
                a = listBox1.SelectedItem.ToString();
                searcher.SearchRoot = entry;
                searcher.Filter = "(&(objectClass=user)(name=" + a + "))";
                SearchResultCollection results = searcher.FindAll();
                foreach (SearchResult result in results)
                {
                    label6.Text = "Modify user details";
                    label3.Visible = false;
                    textBox2.Visible = false;
                    ResultPropertyCollection props = result.Properties;
                    foreach (string propName in props.PropertyNames)
                    {
                        if (propName == "name" && props[propName][0].ToString() != null)
                        {
                            textBox1.Text = props[propName][0].ToString();
                        }
                        if (propName == "company")
                        {
                            textBox3.Text = props[propName][0].ToString();
                        }
                        if (propName == "department")
                        {
                            textBox4.Text = props[propName][0].ToString();
                        }
                    }
                }
            }
        }
        private void EstablishConnection()
        {
            entry.Path = "LDAP://192.168.1.95/CN=Users, DC=sql, DC=local";
            entry.Username = "administrator@SQL.local";
            entry.Password = "kogent@321";
        }
        private void Form1_Load(object sender, EventArgs e)
        {
            EstablishConnection();
            status = true;
        }
        private void listBox1_SelectedIndexChanged(object sender, EventArgs e)
        {
            SetDetails();
        }
    }
}
```

In Listing 37.1, we have imported the System.DirectoryServices namespace to access its DirectoryEntry and DirectorySearcher classes. An object of the DirectoryEntry class is used to establish a connection between the application and AD by using the LDAP provider. The code in the Click event of button1 is used to add a new user in AD by using the properties and methods of the DirectoryEntry and DirectoryEntries classes. The code in the Click event of button2 is used to search a user in AD and modify its details by using the properties and methods of the DirectorySearcher, SearchResultCollection, and ResultPropertyCollection classes. The Click event of button3 is used to display the information of users.

8. Press the F5 key to execute the WorkingwithActiveDirectory application. The output of Listing 37.1 is shown in Figure 37.4:
