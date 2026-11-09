In the present scenario, Internet is emerging as the most widely-used medium for performing various tasks, such as exchanging data and information as well as conducting online shopping and bank transactions. Apart from the common people, most of the government organizations and high business houses entirely depend on this medium for transmitting and receiving critical information and conducting their day-to-day business. All this information and data need to be secured against unauthorized access from illegal and malicious sources. Security is implemented in a website mainly through two processes, i.e. authentication and authorization. Authentication refers to the process of recognizing the identity of a user; whereas, authorization is the process of providing access to various resources, such as databases and printers, to the authenticated users.

Earlier, you need to write large pieces of code to create forms and user interfaces (UI) for authenticating the user, and displaying the desired page based on the roles or rights given to the user. However, creating such forms or user interfaces with the help of standard ASP.NET server controls is quite tedious and time-consuming. Microsoft realized the problem and developed a new series of server controls, called Login controls. To use Login controls in your website, you just need to drag-and-drop them on the Web form, which means there is no more need to write lengthy code in the code-behind file. Login controls helps you to ensure that only authenticated users are allowed to access your website. The Login controls are available under the **Login** tab present in the **Toolbox**.

In this chapter, you learn about various Login controls available in ASP.NET 4.0, such as Login, LoginView, PasswordRecovery, LoginStatus, LoginName, and ChangePassword. The chapter also discusses the noteworthy properties and methods of all these controls. To use Login controls in a Web site, you need to first learn how to create a user account. So let’s begin with creating a user account in ASP.NET 4.0.

# Creating a User Account in ASP.NET 4.0

The user account can be defined as the account which helps in authenticating a user by a username and password. Generally, every Web site authenticates its visitors on the Home page itself before granting them access to important resources. The user name of every user is unique; whereas, one or more users can have the same password. A combination of the user name with its corresponding password is used to differentiate one user from another. You should first learn how to create a user account by using the **ASP.NET Web Site Administration Tool** to work with the Login controls. Let’s perform the following steps to create a user account by using the **ASP.NET Web Site Administration Tool**.

+   1. Click **Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010**.
+   2. *Select* **File→New→Web Site** from the menu bar.
+      The **New Web Site** dialog box appears.
+   3. *Select* **Visual C#** from the **Installed Templates** pane and then select the **ASP.NET Empty Web Site** template in the middle pane.
+   4. *Specify* the name of the application as **UserAccount**.
+   5. *Click* the **OK** button.
+      The **UserAccount** application is created.
+   6. *Select* the **ASP.NET Configuration** option from the Website menu, as shown in Fig.ASP-5.1:

![](bbox=[0.408, 0.709, 0.616, 0.845])