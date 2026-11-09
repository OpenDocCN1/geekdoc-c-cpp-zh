
![](img/9862a98a1a2d3bb14334137965a1ec60_461_0.png)

Fig.C#-7.27

A message box appears, displaying the detail of the exception raised (Fig.C#-7.28).

- 14. *Click* the **OK** button to close the message box, as shown in Fig.C#-7.28:

![](img/9862a98a1a2d3bb14334137965a1ec60_461_1.png)

Fig.C#-7.28

Let’s now learn about user-defined exception classes.

## Using the User-Defined Exception Class

In addition to using the pre-defined exception classes, you can create your own exception classes to handle exceptions. Such exception classes are called **user-defined exception classes**. The exceptions handled by user-defined exception classes are called **user-defined exceptions**. It is important to note that the user-defined exception classes are derived from the **ApplicationException** class. The advantage of using the user-defined exception class is that you can distinguish between error conditions programmatically.

Let’s create an application to understand the use of a user-defined exception class, by performing the following steps:

- 1. *Start* **Visual Studio 2010**.
- 2. *Select* **File→New→Project** from the menu bar. The **New Project** dialog box opens.
- 3. *Select* **Visual C#→Windows** from the **Installed Templates** section in the left pane of the **New Project** dialog box.
- 4. *Select* **Console Application** in the right pane to create a Console application.
- 5. *Enter* the name of the application as **UserExceptionClassExample** (also available on the CD) in the **Name** text box and an appropriate location for the application in the **Location** box.
- 6. *Click* the **OK** button to close the **New Project** dialog box. The **UserExceptionClassExample** application is created, as shown in Fig.C#-7.29:

![](img/9862a98a1a2d3bb14334137965a1ec60_462_0.png)

Fig.C#-7.29

- 7. Add the code snippet, given in Listing 7.9, in Code Editor.

Listing 7.9: Showing the Code to Create and Use a User-Defined Exception Class

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace userExceptionClassExample
{
    class Program
    {
        static void Main(string[] args)
        {
            float x = -1.0F;
            try
            {
                if (x < 0)
                {
                    throw new MyException("Its a negative number");
                }
            }
            catch (MyException ex)
            {
                Console.WriteLine("Exception caught");
                Console.WriteLine(ex.Message);
            }
            finally
            {
                Console.WriteLine("Control entered in the finally block");
                Console.Read();
            }
        }
    }
    class MyException : ApplicationException
    {
        public MyException()
        {
        }
        public MyException(string message): base(message)
        {
        }
        public MyException(string message, ApplicationException ax):
        base(message, ax)
        {
        }
    }
}
```

In Listing 7.9, we have created a new exception class, named **MyException**, which is derived from the **ApplicationException** class. Within the **MyException** class, three constructors of the base class are implemented. Inside the **Main** function, we have declared a float type variable, **x**, and assigned a negative value to it. This raises the **MyException** exception and the control is transferred to the **catch** and **finally** statements.

- 8. Press the **F5** key to execute the application. The output appears, as shown in **Fig.C#-7.30**:

![](img/9862a98a1a2d3bb14334137965a1ec60_463_0.png)

Fig.C#-7.30

As seen in **Fig.C#-7.30**, the value in the **x** variable is a negative number; and therefore, the **MyException** exception is raised and the message, **Its a negative number**, is displayed. Finally, the control enters the **finally** statement and displays the message, **Control entered in the finally block**.

With this, we come to the end of the chapter. Let's now summarize the key points of the chapter.

### Summary

In this chapter, you have learned about the errors and the types of errors, such as syntax error, runtime error, and logical error. In addition, you have learned about exceptions and the techniques to handle them. Finally, you have learned about user-defined classes.

In the next part, you learn about **ASP.NET 4.0**, which includes its different versions, benefits, and new features.

## Introduction to ASP.NET 4.0

### CHAPTER 1

### In this Chapter:

- Exploring Versions of ASP.NET
- Describing Benefits of ASP.NET
- Exploring New Features in ASP.NET 4.0
- Exploring ASP.NET 4.0 Web Application
- Explaining ASP.NET 4.0 Provider Model
- Explaining ASP.NET 4.0 Coding Models
- Implementing Code Sharing
- Compiling an ASP.NET 4.0 Web Application
- Understanding Dynamic Compilation in ASP.NET 4.0

ASP.NET is a technology that is used to create dynamic Web pages for Web sites. The basic difference between a static Web page and a dynamic Web page is that static Web pages cannot change their content dynamically (at runtime); whereas, the look and feel of dynamic Web pages can be modified at runtime. ASP.NET facilitates the creation of small, personal Web sites as well as large, enterprise-level Web sites. It is the successor to Microsoft's Active Server Pages (ASP) technology and Microsoft's first server-side scripting engine used to generate dynamic Web pages. Microsoft released the first version of ASP.NET, ASP.NET 1.0, in January 2002 with .NET framework 1.0. ASP.NET is built on Common Language Runtime (CLR), which allows programmers to write ASP.NET code by using any programming language supported by .NET framework, such as C# and VB.NET.

The latest version of ASP.NET, ASP.NET 4.0, contains lots of features and enhancements and is more powerful as compared to its previous versions. ASP.NET 4.0 provides a user-friendly environment to write managed applications, which include many helpful wizards for creating code as well as useful features, such as context coloring, integrated online help, auto completion, and edit time error notification.

This chapter begins by discussing about the versions and benefits of Microsoft ASP.NET 4.0. Next, it discusses the new features introduced in ASP.NET 4.0. You also learn about provider models and coding models in ASP.NET 4.0. Towards the end, code sharing, compilation, and dynamic compilation in ASP.NET 4.0 are discussed.

Now, let’s begin our discussion by introducing the different versions of ASP.NET.

### Exploring Versions of ASP.NET

Four versions of ASP.NET have been released so far in the market: ASP.NET 1.0, ASP.NET 1.1, ASP.NET 2.0, and ASP.NET 3.5. The following is a brief description of each of these versions:

- **ASP.NET 1.0:** Refers to the first version of ASP.NET. It was released together with Visual Studio.NET 2002 on January 16, 2002.
- **ASP.NET 1.1:** Refers to the second version of ASP.NET. It was released together with VS.NET 2003 on April 24, 2003. Some of the new features added to this version are mobile controls and automatic input validation.
- **ASP.NET 2.0:** Refers to the third version of ASP.NET. It was released together with VS 2005 on November 7, 2005. It introduced several new features to ASP.NET, including master pages, personalization, and WebParts controls.
- **ASP.NET 3.5:** Refers to the fourth version of ASP.NET, which is released together with VS 2008 on November 19, 2007. This version introduces several new features to ASP.NET, including data controls, the inclusion of ASP.NET AJAX as part of the framework, and support for LINQ with the new **LinqDataSource** control.
- **ASP.NET 4.0:** Refers to the fifth version of ASP.NET, which is released together with VS 2010 on April 12, 2010. This version introduces several new features to ASP.NET, including data controls, Web Forms, Web.config file, and style sheets.

Now, let’s discuss about the benefits of ASP.NET.

### Describing Benefits of ASP.NET

ASP.NET provides several benefits, both from the perspective of developers as well as end users. Some of the benefits of ASP.NET are as follows:

- Supports robust database-driven functionality
- Executes Web sites faster
- Provides memory leak and crash protection
- Supports easy deployment
- Supports multiple languages

Let’s discuss these benefits in detail one by one in the following sections.
