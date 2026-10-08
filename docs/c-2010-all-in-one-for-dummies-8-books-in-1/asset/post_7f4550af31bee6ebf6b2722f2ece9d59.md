
## 492 Breaking Down the Projects

- WPF User Control Library: The finished product of this looser control format doesn't appear in the toolbox but is much easier to build because it doesn't require coding the whole thing in C#.

- Windows Forms control library: Like the WPF control library but for Windows Forms. It helps to build a control that you can use from the toolbox.

- Web Projects: Web projects are programs that require a server to run (well, usually) and are used from the browser. They render HTML to the browser, rather than fancy formats like Silverlight. Projects include

- ASP.NET Web Application: This is the centerpiece of the Web development space. It creates an application that can be run on IIS, and presents a Web page to the user.

- ASP.NET Service Application: This is a class library for service-oriented applications. If you're going to distribute applications over several machines, or provide broadly distributed applications, your project type will provide a standards-based implementation for your service offerings.

- ASP.NET AJAX Server Control: Asynchronous JavaScript And XML is a development style that provides a significant quantity of user interactions within the Web browser. This allows you to build controls that support this pattern.

- WCF Service Application: This project belongs in the Communication Foundation section. It's like the ASP.NET Web Service Application, except it provides a number of different standards-based implementations for your service offerings. ASP.NET Web services provide only one.

- ASP.NET Server Control: This control would appear in the toolbox, enabling you to drag the select functionality right onto the Web page in development.

- ASP.NET AJAX Server Control Extender: This control extends the functionality of another AJAX control. It targets a control and adds a feature.

- Dynamic Data Linq to SQL Application: This is an ASP.NET Web application that uses Linq to make a data-active Web page.

- Dynamic Data Entities Web Application: This ASP.NET application uses ADO.NET Entities to make a data-active Web page.

- Office Projects: Office projects are part of the Visual Studio Tools for Office package, and use Office as a platform instead of Windows or a Web browser. To find out more, look at the book I coauthored with Peter Jaunovich, Office For Dummies. Office Projects include

- Excel 2007 Workbook: Has a Microsoft Excel Workbook (a collection of Excel worksheets) as an output.

- Word 2007 Template: Has a Microsoft Word 2007 template (a .dot file) as an output.

- Project 2007 Add-in: Creates an add-in for Microsoft Project.

- Visio 2007 Add-in: Creates an add-in for Microsoft Visio.

- Word 2007 Add-in: Creates an add-in for Microsoft Word.

- Excel 2007 Add-in: Creates an add-in for Microsoft Excel.

- Outlook 2007 Add-in: Creates an add-in for Microsoft Outlook.

- Word 2007 Document: Has a Microsoft Word 2007 document as an output.

- Excel 2007 Template: Has a Microsoft Excel 2007 template (an .xlt file) as an output.

- InfoPath Add-in: Creates an add-in for Infopath.

- PowerPoint 2007 Add-in: Creates an add-in for Microsoft PowerPoint.

**Communication Foundation Projects:** Windows Communication Foundation is Microsoft's way to provide a mechanism for programs to talk with one another:

- Syndication Service Library: Creates a syndicated feed service (RSS) that speaks ATOM or RSS.

- WCF Service Library: A class library for Communication Foundation.

- Declarative Flowchart Service Library: Makes a set of services that use flowchart-style workflow to provide services.

**Workflow Projects:** Foundation Workflow is the standard library for creating workflows in Microsoft programs. You can set up standard approvals, movement of documents, and the like:

- Activity Designer Library: This project assists you with creating a user interface for creating activities.

- Activity Library: If you’re not in the mood to create user interfaces for the creation of activities, you can create an activity library.

- Flowchart Workflow Console application: This project, and the sequential project, provides a way to test WF workflows in a safe environment.

- Sequential Workflow Console Application: This is just like the flowchart WF project, but for sequential workflows.

**Special Projects:** Refers to anything that doesn't fit into the preceding bullets:

- Test Project: If you're working in Visual Studio, right-click a method, and select Create Unit Test, you will get this kind of project. In the case where you want to make a test project manually, this is your project.

- Silverlight: Admitted, Microsoft Expression would be your best choice for Silverlight. If you want to use Visual Studio, however, you can use this project.

- SQL Server Project: Again, I would use Microsoft SQL Server Management Studio to manage database projects. If you have to use Visual Studio for some reason, this is your project.

- Reports Application: You can include reports right in your Windows or Web application. If you're deploying directly to Reporting Services, this project does the job.

**Other kinds of projects:** It's easy to make a project type, and there are a bunch of them. Some of them are patterns, some of them are languages, and some of them are new outputs:

- ASP.NET MVC: Model View Controller (MVC), a project type that allows for separation of duties between development teams. Search MSDN for more.

- MVC4WPF: Allows for Model View Controller development for Windows Foundation. It has templates just like regular applications. Check it out at www.mvc4f.com.

- IRONRuby: An implementation of Ruby in Visual Studio.

- IRONPython: An implementation of Python in Visual Studio.

## Chapter 2: Using the Interface

In This Chapter

- Using the Designer
- Exploring Solution Explorer
- Coding with Code View
- Using Tools Menu

Integrated Development Environments, or IDEs, are the Swiss army knife of the programmer's toolkit. IDEs provide a mechanism for storing program code, organizing and building it, and looking at finished products with design editors. IDEs make things happen, and in the bargain, cut hours from a task.

Visual Studio is becoming globally recognized as the cream of the crop of IDE, even by Microsoft developers. I know Python programmers who will rail on Windows all day while surfing their Linux box and switch to a Windows partition to use Visual Studio to create IRONPython.

## Designing in the Designer

One thing that is integrated into an Integrated Development Environment is a way to edit files graphically—sometimes a Graphic Development Environment or designer. Visual Studio allows you to graphically edit five different types of code bases and provide adjunct tools for the further management of code bases.
