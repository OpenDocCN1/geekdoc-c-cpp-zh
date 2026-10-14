

## 处理多个 Web 表单的六项技能

要创建一个多页网站，你需要学习一些新技能，例如如何重命名 Web 表单、如何更改网站的起始页，以及如何从一个表单转移到另一个表单。在我介绍这些技能之前，我想先向你展示如何创建一个默认包含多个文件夹和文件的网站。

### 如何创建包含起始文件和文件夹的网站

虽然我使用 ASP.NET Empty Web Site 模板创建了本书中的所有网站，但你应该了解另一个可用于创建包含多个起始文件和文件夹的网站的模板。这就是 ASP.NET Web Site 模板，其生成的 文件如 Figure 3-5 所示。

首先，你应该注意到网站的根文件夹中包含一个名为 Site.master 的文件。该文件定义了一种称为 *master form* 的表单类型，并且该表单的内容会显示在网站中的其他每个表单上。你将在第 9 章了解更多关于处理 master forms 的内容。

除了 master form 之外，根目录还包含两个名为 About.aspx 和 Default.aspx 的表单。它还包含一个名为 Global.asax 的文件。你将在第 8 章学习如何使用此文件来处理应用程序事件。

接下来，注意 Account 文件夹中的四个表单。这些表单用于添加用户账户、登录网站以及更改密码。你将在第 19 章看到此类表单的工作方式。此文件夹还包含一个 web.config 文件，该文件仅适用于此文件夹中的表单。相比之下，根文件夹中的 web.config 文件适用于整个网站。

除了 Account 文件夹外，此网站还包含三个文件夹。App_Data 文件夹，如你所知，用于存储应用程序使用的数据文件，例如数据库文件。Scripts 文件夹包含一个名为 *jQuery* 的 JavaScript 库，可让你处理 HTML 元素。你将在第 21 章了解更多关于 JavaScript 和 *jQuery* 的内容。最后，Styles 文件夹包含一个名为 Site.css 的外部样式表。你将在第 5 章了解更多关于使用外部样式表的内容。

### 使用 ASP.NET Web Site 模板创建的网站

![A web site created using the ASP.NET Web Site template](img/c024ccf88e28c30c07dd410d4342288f_106_0.png)

### 网站使用的部分文件

| Folder | File | Description |
| :--- | :--- | :--- |
| Account | ChangePassword.aspx | A form that lets users change their password. |
| Account | ChangePasswordSuccess.aspx | A form that indicates if a password has been successfully changed. |
| Account | Login.aspx | A form that lets users log in to an application. |
| Account | Register.aspx | A form that lets users create new accounts. |
| Styles | Site.css | An external style sheet with styles used by the forms. |
| (root) | About.aspx | A form that lets you enter information about your web site, company, etc. |
| (root) | Default.aspx | The default form for the web site. |
| (root) | Global.asax | A file that lets you work with application data. |
| (root) | Site.master | The master page for the web site. |

### Description

- When you start a web site from the ASP.NET Web Site template, Visual Studio adds a number of folders and files to the web site. You’ll learn how to work with many of the forms, the controls used on the forms, and the files later in this book.

### How to rename a web form

When you add a web form to a web site, the form file is given the name you specify in the Add New Item dialog box. In addition, the partial class that contains the C# code for the form is given the same name, which is usually what you want. In some cases, though, you may need to rename the form file or the form class. In particular, if you use the technique in Figure 3-5 to start an ASP.NET web site, you'll want to rename the default form so its name is more descriptive. Figure 3-6 shows you how.

When you change the name of a form file, you might think that Visual Studio would change the name of the class that contains the C# code for the form to the same name. However, it doesn't. To do that, you have to open the Code Editor window for the form and change the name in the class declaration.

When you change the name of a form file, the CodeFile attribute in the Page directive for the page is changed automatically. However, if you change the name of a class, the Inherits attribute in the Page directive is not changed unless you use the Rename command from the smart tag menu that becomes available when you change the class name. If you don't use this command, you'll have to change the Inherits attribute manually when you change the name of a class.

### How to change the starting web form

If a web site consists of a single form, that form is displayed by default when you run the application. If a web site contains two or more forms, however, the current form—the one that's selected in the Solution Explorer—is displayed when you run the application. Or, if a form isn't currently selected, the form named Default.aspx is displayed. If the web site doesn't contain a form named Default, a directory listing of the application is displayed.

To make sure that the correct page is displayed when you run an application, you should set the start page for the application. To do that, just right-click on the form in the Solution Explorer and select the Set As Start Page command from the shortcut menu. Note that this only sets the start page that Visual Studio uses when you run an application. It doesn't set the page IIS displays by default when you run the application from a browser outside of Visual Studio. To do that, you have to use IIS. See appendix B (Windows 7 and Windows Vista) or appendix C (Windows XP) for more information.

### Solution Explorer 窗口中正在重命名的 Web 表单文件

![A web form file being renamed in the Solution Explorer window](img/c024ccf88e28c30c07dd410d4342288f_108_0.png)

### 重命名 Web 表单的两种方法

- Right-click the form in the Solution Explorer, and then select the Rename command from the shortcut menu. Then, change the name directly in the Solution Explorer window.
- Click on the form in the Solution Explorer to select it. Then, click on it again and change the name directly in the Solution Explorer window.

### How to rename the class that contains the C# code for a web form

- Display the code for the form in the Code Editor window. Then, change the name that's used for the form in the class declaration at the beginning of the file.
- Use the Rename command in the smart tag menu that becomes available to change the class name in the Inherits attribute of the Page directive. Alternatively, display the aspx code for the form and then change the Inherits attribute manually.

### How to change the starting web form for a web site

- Right-click on the web form that you want to use as the starting form in the Solution Explorer. Then, choose Set As Start Page from the shortcut menu.

### Note

- In most cases, you'll give a web form an appropriate name when you add it to the project. If you start a web site from the ASP.NET Web Site template, though, you may want to change the name of the web form that's added by default so it's more descriptive.

Figure 3-6 How to rename a web form and change the starting web form

### How to redirect or transfer to another page

When you develop an application with two or more pages, you'll need to know how to display one page from another page. When the user clicks the Add to Cart button on the Order page of the Shopping Cart application, for example, the Cart page should be displayed. Similarly, when the user clicks the Continue Shopping button on the Cart page, the Order page should be displayed. Three ways to do that are presented in Figure 3-7.

When you use the Transfer method of the HttpServerUtility class, ASP.NET immediately terminates the execution of the current page. Then, it loads and executes the page specified in the Transfer method and returns it to the browser. The drawback to using this method is that when the new page is sent to the browser, the browser has no way of knowing that the application returned a different page. As a result, the URL for the original page is still displayed in the browser's address box. This can be confusing to the user and prevents the user from bookmarking the page.

The Redirect method of the HttpResponse class works somewhat differently. When this method is executed, it sends a special message called an *HTTP redirect message* back to the browser. This message causes the browser to send a new HTTP request to the server to request the new page. Then, the server processes the page and sends it back to the browser.

Note that because of the way the Redirect method works, it requires an extra round trip to the browser. If this extra round trip will cause a performance problem, you may want to use the Transfer method instead. For most applications, however, the user friendliness of the Redirect method outweighs the small performance gain you get when you use the Transfer method.

Unlike the Transfer and Redirect methods, the RedirectPermanent method, which is new to ASP.NET 4, is typically used when a page is physically moved or renamed within a web site. For example, suppose you create a web site that includes a page named Products.aspx that's stored in the project folder. Later, suppose you decide to create a subfolder named Customer, and you move the Products page to this folder. Then, you can use the RedirectPermanent method as shown in the third example in this figure to redirect to the page. The main advantage of using this method is that search engines will store the new URL. That way, if the page is requested at the old location, it can be displayed from its new location.

