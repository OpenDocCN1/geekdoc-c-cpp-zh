| Event Handler Method Name | Description |
| --- | --- |
| Application_Start | Used to set up the application environment and is only called when the application first starts |
| Session_Start | Occurs when any new user access the website |
| Application_BeginRequest | Occurs as the first event in the HTTP execution chain when responding to a request |
| Application_AuthenticateRequest | Occurs when a security module has established the identity of the user |
| Application_Error | Occurs when an unhandled exception is thrown |
| Session_End | Occurs when a user’s session ends or times out. The default timeout is 20 minutes after the user leaves the site |
| Application_End | Used to clean up the application environment when the application ends |

# # Creating a Web Application

In the rest of this hour, you create a web-based photo viewer application by creating a new project, laying out the form, and adding controls.

First, create a new ASP.NET Web Application project using the New Project dialog, as shown in Figure 19.2. In the Name field, enter PhotoViewWeb.

Just as it does with desktop applications, Visual Studio creates a solution and project for you. This time, instead of displaying the generated C# class file or XAML designer, Visual Studio displays the code editor for the applications default.aspx page and the Properties window. Figure 19.3 shows what Visual Studio should look like after having just created the project.

This editing surface is similar to the one used by the WPF XAML editor. The editor for ASPX pages can show you the source markup, the visual representation of the layout, or a split view showing both. By default, the editor shows the source markup. You can make changes in either view, and changes made in one will be reflected in the other.