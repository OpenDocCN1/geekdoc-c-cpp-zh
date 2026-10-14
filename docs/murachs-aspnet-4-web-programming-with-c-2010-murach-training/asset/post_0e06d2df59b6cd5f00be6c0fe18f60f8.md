
## IIS application pools

![](img/c024ccf88e28c30c07dd410d4342288f_820_0.png)

## Description

- After you install ASP.NET 4, four application pools will be defined for IIS. To display these pools, click the Application Pools node in the Connections pane.
- If you create a new IIS application or virtual directory from Visual Studio, it’s assigned to an application pool based on the target framework you specify. If you create an IIS application from the IIS Management Console, you specify the pool you want to use.
- To add an application pool, click the Add Application Pool link in the Actions Pane to display the dialog box shown above. Then, enter a name for the pool, select the .NET Framework the application uses, and click OK.
- To change the application pool that an application runs in, select the application in the Connections pane, click the Basic Settings link in the Actions pane, click the Select button in the Edit Application dialog box that’s displayed, and select the pool from the Application Pool drop-down list.
- To change the default application pool for the server, select the Default Web Site node instead of a specific application.
- You can also perform a variety of operations on individual application pools by selecting a pool in the Application Pool page and then using the links in the Action pane.

Figure B-4    How to work with application pools

## Appendix C

## How to work with web applications using IIS under Windows XP

In several places throughout this book, we’ve indicated that you can perform certain operations on a web application using IIS. Although you don’t need to know how to use IIS to perform these operations to develop web applications as described in this book, you’ll probably need these skills as a professional programmer. So if you’re using Windows XP, we recommend that you read these topics when we refer to them in the book or after you’ve completed the book.

- How to create a virtual directory ......................................................... 804
- How to set the default page for a web site ............................................... 806
- How to force a page to use a secure connection ....................................... 808

## How to create a virtual directory

In appendix A, you learned how to create a virtual directory for a file-system web site from within Visual Studio. But if you prefer, you can create a virtual directory from the IIS Management Console. In figure C-1, for example, you can see two of the dialog boxes for creating a virtual directory named Ch03Cart that points to the web site stored in the C:\aspnet4_cs\Ch03Cart directory.

After you create a virtual directory, it will appear under the Default Web Site node in the IIS Management Console. Then, you can use Visual Studio to open the web site from this directory so you can run the application under IIS. You can also run the application from outside of Visual Studio. Note that you can also create a virtual directory in a subdirectory of the Default Web Site node. In the illustration in this figure, for example, the virtual directory is being created in the aspnet_2010 directory.

## The dialog boxes for creating a virtual directory in IIS

![](img/c024ccf88e28c30c07dd410d4342288f_824_0.png)

## How to create a virtual directory for a file-system web site

- 1. Open the Control Panel, double-click Administrative Tools, and double-click Internet Information Services to open the IIS Management Console.
- 2. Use the tree to locate the Default Web Site node, right-click Default Web Site (or a directory that’s subordinate to that node), and choose New➜Virtual Directory to start the Virtual Directory Creation Wizard.
- 3. Enter the name you want to use for the virtual directory on the Virtual Directory Alias page of the wizard, enter the path for the directory that contains the web site on the Web Site Content Directory page, and accept the defaults on the Access Permissions page.

## Description

- In chapter 4, you can learn how to create a virtual directory for a new or existing web site using Visual Studio. You can also create a virtual directory for a web site from IIS. Then, you can use Visual Studio to open the web site from the virtual directory, and you can run the web site under IIS.

Figure C-1    How to create a virtual directory

## How to set the default page for a web site

To run a web application from outside of Visual Studio, you typically enter the URL of the application and the starting page in a browser. If you don’t enter a starting page, however, IIS will look for a page with a name in the default document list for the application. By default, this list doesn’t include a document with the aspx extension. Because of that, you’ll need to add the name of the page you want to be displayed by default to this list if you want the users of the application to be able to omit the starting page from the URL for the application. Figure C-2 shows how you do that.

The dialog box in this figure shows the default document list for the Ch03Cart application after I added the document named Order.aspx. Note that when you add a document to the list, it’s displayed at the end of the list. Because IIS will check for documents in the order that they appear in the list, you’ll usually want to move the document you add to the beginning of the list. To do that, you use the up arrow button to the left of the list.

When you develop a web site, you typically use meaningful names for the pages it contains. If you frequently use the same name for the starting page of an application, however, you can add this name to the default document list. For example, you might use the name Default.aspx for your starting pages since this is the default name of the first page that’s added to a web site. To add this name to the list, you use the same technique shown in this figure, but you change the list for the Default Web Site node instead of for a specific web site.

## The Documents tab of the Properties dialog box

![](img/c024ccf88e28c30c07dd410d4342288f_826_0.png)

## How to work with the list of default documents for a web site

- To display the list of default documents for a web site, display the IIS Management Console, and locate the web site. Then, right-click on the web site, select Properties from the shortcut menu, and click the Documents tab in the Properties dialog box that’s displayed.
- To add a document to the list of default documents, click the Add button, enter the document name in the dialog box that’s displayed, and click OK.
- To change the order in which IIS looks for the documents, use the up and down arrow buttons to the left of the document list.
- To remove a document from the list, select the document and click the Remove button.

## Description

- By default, if you run a web application from a browser outside of Visual Studio and you don’t include the name of the page you want to display in the URL, IIS looks for a document with the name Default.htm, Default.asp, index.htm, or iisstart.asp. If you want IIS to look for a document with a different name, you can use the procedure above to add that document to the list of default documents.
- You can also add a document to the list of default documents for all your web sites. To do that, use the procedure above, but right-click the Default Web Site node instead of a specific web site. For example, you might want to add Default.aspx to the list since this is the default name of the first page that’s added to a new web site in Visual Studio.

## The dialog boxes for securing a web page

![](img/c024ccf88e28c30c07dd410d4342288f_828_0.png)

## How to set the security for a web page

- 1. Display the IIS Management Console, locate the web site that contains the page you want to secure, and select the web site or the folder within the web site that contains the page.
- 2. Right-click the page (.aspx) in the right pane of the IIS Management Console, select the Properties command from the shortcut menu, and display the Directory Security tab of the Properties dialog box that’s displayed.
- 3. Click the Edit button in the Secure Communications section to display the Secure Communications dialog box. Then, select the Require Secure Channel (SSL) option. If you want the page to be displayed only if 128-bit encryption is used, select the Require 128-bit Encryption option.

## Description

- In chapter 18, you can learn how to add C# code to a page to be sure that it uses a secure connection. Another way to do that is to set IIS security properties for the page.
- You can also set the security for all the pages within a folder of a web site or for all the pages of a web site. To do that, display the properties for the folder or web site, display the Directory Security tab, and then set the appropriate options.
