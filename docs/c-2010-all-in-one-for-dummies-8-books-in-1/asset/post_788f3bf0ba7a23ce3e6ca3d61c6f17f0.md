
## Decomposing components into functions

After you create a document that describes what the software is doing and how, you need to break out the individual functional pieces of the software. If you have set up your software in a component fashion, the classes and methods show the functional decomposition. It's simpler than that.

The result of breaking the software into individual pieces is having a decent merit of which components need to be protected, which parts of the software interact with each component, which parts of the network and hardware system interact with each component, and which functions of the software do with each component.

## Identifying potential threats in functions

After you create the list of components that you need to protect, you tackle the tough part: Put two and two together. Identifying threats is the process that gets security consultants the big bucks, and it's almost entirely a factor of experience.

For instance, if your application connects to a database, you have to imagine that the connection could be intercepted by a third party. If you use a file to store sensitive information, the file could, theoretically, be compromised.

To create a threat model, you need to categorize the potential threats to your software. An easy way to remember the different categories of threats is the acronym STRIDE:

- **Spoofing identity**: Users pretend that they are someone
- **Tampering with data or files**: Users edit something that shouldn't be edited.
- **Repudiation of action**: Users have the opportunity to say they didn't say that they actually did do.
- **Information disclosure**: Users see something that shouldn't be seen.
- **Denial of service**: Users prevent legitimate users from accessing the system.
- **Elevation of privilege**: Users get access to something that they shouldn't have access to.

All these threats must be documented in an outline that expose the threat. This strategy not only gives you a good, discrete list of threats but also focuses your security hardening on those parts of the application that pose the greatest security risk.

| Book III |
| :--- |
| Chapter 1 |

## 404 Building Secure Windows Applications

The final step in the process is to rate the risks. Microsoft uses the DREAD model to assess risk to its applications. The acronym DREAD represents five key attributes to measure each vulnerability:

- **Damage potential**: The dollar cost to the company for a breach
- **Reproducibility**: Special conditions to the breach that might make it harder or easier to find
- **Exploitability**: A measure of how far into a corporate system a hacker can get
- **Affected users**: The number of users who are affected and who they are
- **Discoverability**: The ease with which you can find the potential breach

You can research the DREAD model at mdn.microsoft.com/security, or position your threat model to consider those attributes. The key is to determine which threats are most likely to cause problems and then mitigate them.

The framework lives in a tightly controlled sandbox when running on a client computer. Based on the realities of this sandbox, the configuration of security policy for your application becomes important.

The first place you need to look for security in writing Windows applications is in the world of authentication and authorization. *Authentication* confirms the identity of a user, and *authorization* determines what she can and can't do within an application.

When you are threat modeling, you can easily consider all of the possible authentication and authorization threats using the STRIDE acronym. (See the earlier section “Identifying potential threats in functions,” for more about STRIDE.)

To be straightforward, the best way for an application to authorize a user is make use of the Windows login. A host of arguments take place about this strategy and others, but the key is simplicity: Simple things are more secure.

For much of the software developed with Visual Studio, the application will be used in an office by users who have different roles in the company; for example, some users might be in the Sales or Accounting department. In many environments, the most privileged users are managers or administrators — yet another set of roles. In most offices, each employee has her own user account, and each user is assigned to the Windows groups that are appropriate for the roles they play in the company.

Using Windows security works only if the Windows environment is set up correctly. You can't effectively build a secure application in a workspace with a bunch of Windows XP machines where everyone logs on as the administrator, because you can't tell who is in what role.

Building a Windows application to take advantage of Windows security is straightforward. The goal is to check who is logged on (authentication) and then check that user's role (authorization).

The following steps show you how to create an application that protects the menu system for each user by showing and hiding buttons:

- 1. Start a new Windows Forms Application project by choosing File:New Project and giving your project a descriptive name. This would work for Windows Presentation Foundation (WPF) too, but it's easier to show in Windows Forms. (Book V is all about named my project Windows Security.)
- 2. Add two buttons to your form — one for Sales Menu, one for Accounting Menu, and one for Manager's Menu. My example is shown in Figure 1-

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_430_0.png)
![](img/36596fb11aa4233d5cab0d6ddd1d82e8_430_1.png)

- 3. Set every button's visible properties to False so that they aren't shown on the form by default.
- 4. Double-click the form to reach the Form1_Load event handler.

- 5. Above the Namespace statement, import the System.Security.Principal namespace this way:

```
using System.Security.Principal;
```

- 6. In the Form1_Load handler, instantiate a new Identity object represents the current user with the GetCurrent method of the WindowsIdentity myIdentity by adding this bit of:

```
WindowsIdentity myIdentity = WindowsIdentity.GetCurrent();
```

- 7. Get a reference to this identity with the WindowsPrincipal class:

```
WindowsPrincipal myPrincipal = new WindowsPrincipal(myIdentity);
```

- 8. Finally

### Listing 1-1: The Windows Security Application Code

```assembly
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Security.Principal;

namespace WindowsSecurity
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            WindowsIdentity myIdentity = WindowsIdentity.GetCurrent();
            WindowsPrincipal myPrincipal = new WindowsPrincipal(myIdentity);
            if (myPrincipal.IsInRole("Accounting"))
            {
                AccountingButton.Visible = true;
            }
            else if (myPrincipal.IsInRole("Sales"))
            {
                SalesButton.Visible = true;
            }
            else if (myPrincipal.IsInRole("Management"))
            {
                ManagerButton.Visible = true;
            }
        }
    }
}
```

## Building Secure Windows Applications 405

To successfully run this code, you must have an environment that has Accounting, Sales, and Management user groups.

In some cases, you don't need this kind of role diversification. Sometimes you just need to know whether the user is in a standard role, which System.Security provides for. Using the WindowsBuiltRole enumerator, you describe actions that should take place, for example, the administrator is logged on:

```assembly
if (myPrincipal.IsInRole(WindowsBuiltInRole.Administrator))
    // Do something
```

Encryption is, at its core, an insanely sophisticated process. Five namespaces are devoted to different algorithms. Because encryption is so complex, I don't get into the details in this book.

Nonetheless, it is important that you understand one cryptographic element for a key of element — encrypting files. When you work with a file in a Windows Forms application, you risk someone loading it up in a text editor and looking at it, unless you have encrypted the program.

The common encryption scheme Data Encryption Standard (DES) is implemented in .NET. It isn't the strongest encryption in these days of 64-bit desktop machines, but it's strong enough to encrypt the data files for a Windows application. You can find the methods to encrypt for DES in the CryptoServiceProvider in the System.Security.Cryptography namespace.

If you deploy your application using ClickOnce, you need to define the access to the PC that the application will request. ClickOnce is a server-based deployment strategy that allows users to run Windows Forms applications from a Web browser by using the WindowsSecurity tab in the My Project configuration file, shown in Figure 1-2.
