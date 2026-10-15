
![](img/d99870e80390742f93963da7be0b2e61_791_0.png)

## FIGURE 22-35

## SUMMARY

This chapter and the previous chapter offered a whirlwind tour of ASP.NET and some of the features that you can provide in the projects you develop. ASP.NET is highly focused on the area of developer productivity, and it works very hard at providing you access to functionality expected in websites today.

A nice aspect of most of the features presented is that you can either utilize the wizards that are built into the underlying technology or skip these wizards and employ the technologies by editing markup. Either way is fine. Another useful aspect of the technologies introduced is that they all enable a huge amount of customization. You can alter the behavior and output of these technologies to achieve exactly what you need. If you want to dig deeper into ASP.NET, be sure to take a look at Professional ASP.NET 4 (Evjen et al., Wiley, 2010).

## 23

## ASP.NET MVC

## WHAT YOU WILL LEARN IN THIS CHAPTER

- The Model-View-Controller (MVC) Pattern
- The goals of ASP.NET MVC
- How the MVC pattern has been applied to ASP.NET MVC
- Working with controllers and actions
- Using scaffolding to help generate views
- Validation in ASP.NET MVC 2

ASP.NET MVC is a Web framework that was originally released in March 2009 as an alternative to ASP.NET Web Forms. It was designed to limit abstractions and give developers a great deal of control over the creation of pages in an application. Specifically, ASP.NET MVC was designed to do the following:

- **Provide complete control over HTML markup** — With Web Forms, the final markup is mostly determined by the server controls on a page.
- **Have intuitive website URLs** — With Web Forms, the URL is determined by the location and name of the file being addressed.
- **Have a clear separation of concerns** — The Web Forms programming model encourages developers to put business logic and database access code in the code-behind for a page.
- **Be testable by default** — Several aspects of the Web Forms model make it difficult to write unit tests for user interface layer logic.

It’s important to repeat that ASP.NET MVC is an alternative to Web Forms, not its replacement. MVC will suit the style of some developers, and seem a step backward for others. Many have used the analogy of manual versus automatic transmission. Manual (MVC) gives you complete control but requires more effort; automatic (Web Forms) may be slightly less efficient but it does the work for you. Ultimately, the choice of framework is yours. Choose the one that best suits your development style.

As this book is being written, ASP.NET MVC 2 is in Beta and is projected to be complete with the release of Visual Studio 2010. The contents of this chapter are based on the version of ASP.NET MVC 2 included with the Beta 2 versions of Visual Studio 2010 and .NET 4.

## MODEL-VIEW-CONTROLLER AND ASP.NET

The Model-View-Controller pattern was conceived in the late 1970s by Trygve Reenskaug, a Norwegian computer scientist. It provides a powerful and elegant means of separating concerns within an application, and it applies extremely well to Web development.

The pattern separates an application into three components:

- **Model** — The business objects in the application
- **View** — The user interface
- **Controller** — Classes that handle user requests and manage application logic and flow

In the ASP.NET implementation of the pattern, requests are routed to controller classes that generally apply application logic (authorization, for example), interact with the model to retrieve or update data, determine the data that needs to be rendered in the response, and then pass control to a view to format the data and render the final markup to the user.

Another important aspect of the implementation of ASP.NET MVC is the use of convention over configuration. As we build an application in the next section, you will see that conventions are used to determine the names and locations of files in a project or to determine which class or file to load at runtime. You are not forced to follow these conventions, but doing so allows for a consistent experience across ASP.NET MVC applications.

## BUILDING AN ASP.NET MVC APPLICATION

ASP.NET MVC is a new addition to the ASP.NET family and is likely new to most of you reading this book. Following the premise that the most effective way to learn a new framework is to use it, we will spend the remainder of this chapter building an ASP.NET MVC 2 application.

## Creating the Project

Open Visual Studio and create a new ASP.NET MVC 2 Web Application named **MvcDemo**. You will immediately be asked if you want to create an associated unit test project (see Figure 23-1). Because testability is one of the core tenets of ASP.NET MVC it makes sense that the project template would encourage you to do so. Keep the default test project name and click OK to create the projects.

If you look at the MVC project in the Solution Explorer (see Figure 23-2), you’ll see that several files and folders have been created by default. Three of the folders should jump out at you immediately: Models, Views, and Controllers. These folders map to the three components of the pattern on which this style of application is based.

![](img/d99870e80390742f93963da7be0b2e61_793_0.png)

![](img/d99870e80390742f93963da7be0b2e61_793_1.png)

> Currently, there are no out-of-the-box Web site project templates for ASP.NET MVC.

If you run the application, you will see that a few pages (including the master page) are included as part of the project template (see Figure 23-3). While not exactly the same, the site will be similar in look and feel to one created when you use the non-empty Web Forms project templates.

![](img/d99870e80390742f93963da7be0b2e61_794_0.png)

## Controllers and Actions

In traditional Web application frameworks, requests are mapped to files containing markup for pages. In ASP.NET MVC, requests are mapped to methods on classes. The classes are the previously mentioned controller classes, and the methods are known as actions. Action methods are responsible for receiving user input, retrieving or saving data to the model, and passing control to the appropriate view. The view will typically return the markup for a page but it could also return other content types such as a binary file or JSON formatted data. Typical actions will handle requests to list, add, edit, or delete entities from the model.

Let’s examine these concepts further by creating a new controller. In the Solution Explorer, right-click on the Controllers folder and select Add ➜ Controller. By convention, the names of controller classes should end with “Controller.” The Add Controller dialog even encourages the use of this convention, as shown in Figure 23-4. Set the name to SimpleController and click the Add button.

![](img/d99870e80390742f93963da7be0b2e61_794_1.png)

The class that’s created will inherit from the base Controller class (System.Web.Mvc.Controller) and will have the shell for a default action method named Index:

```
Public Class SimpleController
    Inherits System.Web.Mvc.Controller
```

```
' GET: /Simple/

Function Index() As ActionResult
    Return View()
End Function

End Class
```

The Index action method is about as simple as it gets. When a request comes in for this action it just passes control to a view without any application logic or data access. Because the action method has not specified which view to show, convention states that ASP.NET MVC should look for a file matching the pattern /Views/{Controller}/{Action}.aspx. In the case of the Index action, that would be /Views/Simple/Index.aspx, which does not exist at this point.

The comment above the method is not required but it is something you'll typically see in code generated by Visual Studio. It indicates that this action will be accessed via an HTTP GET request to /Simple. This illustrates another convention. The default routing rules used by MVC expect something in the form of /{Controller}/{Action}. If the action is not specified, then ASP.NET MVC will default to calling the Index action method, so a request to /Simple or /Simple/Index will be routed to the Index action. You will learn about routing and how to add or modify routing rules later in this chapter.

![](img/d99870e80390742f93963da7be0b2e61_795_0.png)

Because the view for the Index action does not exist, let's create it. We could do this rather easily by hand, but there's no need to; Visual Studio will create it for us. In the Code Editor, right-click anywhere in the code for the Index method and select the Add View option in the context menu. In the Add View dialog, leave the default values as they are (see Figure 23-5) and click the Add button. You should be presented with a new content page that looks something like the following:

```
<%@ Page Title="" Language="VB" MasterPageFile="~/Views/Shared/Site.Master" Inherits="System.Web.Mvc.ViewPage" %>

<asp:Content ID="Content1" ContentPlaceHolderID="TitleContent" runat="server">
    Index
</asp:Content>

<asp:Content ID="Content2" ContentPlaceHolderID="MainContent" runat="server">
    <h2>Index</h2>
</asp:Content>
```

Note two things about the page: It was created in the proper folder by default (that is, \Views\Simple) and it inherits from System.Web.Mvc.ViewPage instead of System.Web.UI.Page. At this point you should be able to run the application. Once it is loaded in the browser, navigate to /Simple and you'll see a page like the one shown in Figure 23-6.
