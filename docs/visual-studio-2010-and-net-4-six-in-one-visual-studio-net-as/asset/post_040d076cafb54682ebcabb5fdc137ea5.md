
# SUMMARY

There are many other advanced topics related to ASP.NET Dynamic Data. This chapter just scratched the surface of the features offered by its powerful templates and framework. This chapter also discussed many the customization possibilities offered by ASP.NET Dynamic Data and how it relates to other ASP.NET components and the data models.

Following are some key points from this chapter:

- You can create a data-driven application following many simple steps using the Dynamic Data templates.
- You can create simple and complex CRUD applications based on Dynamic Data.
- You must create a robust data model to take full advantage of Dynamic Data's features.
- You must combine Dynamic Data's features with the validation capabilities offered by the underlying data model.
- You can work with customized templates for fields, entities, and filters.
- You have the capability of defining CSS styles to customize the look and feel of the rendered web pages.
- You can create custom pages for specific entities when the templates aren't enough.

Chapter 18 takes a look at the ASP.NET Model View Controller (MVC).

# 18

## ASP.NET Model View Controller (MVC)

In Chapter 17, you read about the ASP.NET Dynamic Data feature, which became mature with .NET Framework 4. This chapter introduces ASP.NET Model-View-Controller (MVC) technology that recently reached its 2.0 version, which is a built-in component of Visual Studio 2010. ASP.NET MVC 1.0 was an out-of-band release for Visual Studio 2008, too, the MVC team made ASP.NET MVC 2 available for Visual Studio 2008, too, the version shipping with Visual Studio 2010 utilizes several new features that are released with the ASP.NET 4.0 platform.

After reading this chapter, you will be familiar with the following:

- Introduction to MVC — You will learn about MVC and similar design patterns to understand how ASP.NET MVC differs from the ASP.NET Web Forms approach.
- Creating an MVC 2 application — You will learn creating a very simple web application with MVC 2, and learn about the structure of MVC web projects. In contrast to the file-based request routing, MVC uses a different routing model. As you progress through the example, you will learn about the new routing approach.
- Adding new MVC 2 pages — You will extend the simple web site with a few pages using the corners of MVC applications: models, views, and controllers.
- Customization in MVC 2 — MVC was designed with easy extensibility and customization in mind. Here you will discover that customizing your controllers and the way views render the user interface (UI) is incredibly simple.
- Routing details — One of the keys to MVC's simplicity is the routing model it uses. You will learn more about the routing model in this chapter.
- Testing with MVC 2 — MVC has been designed and implemented with Test Driven Development (TDD). In this chapter, you will learn how to refactor an MVC application's architecture to support unit testing.

You do not need any previous experience with ASP.NET MVC to understand MVC 2. This chapter provides enough detail to dive into this topic.

## INTRODUCTION TO MVC

MVC is an architectural pattern frequently used in software development. The roots of this pattern go back to 1979, when Tryge Reenskaug described this pattern during his work on SmallTalk-80 at Xerox Palo Alto Research Center (PARC).

The MVC pattern helps to separate the data (model), the application logic (controller), and the UI (view) from each other, which helps to properly decoupled components within the application.

One of the advantages of this decoupling is that it makes the application more testable, and thus, helps developers to implement an application with the TDD approach. Or, if you are not a fan of TDD, or you are following another development method, using TDD with ASP.NET MVC is not mandatory. It is a great option, because ASP.NET MVC itself is implemented with TDD in mind. This is evidenced by the fact that the source code (which is Open Source) contains thousands of units.

The model is domain-specific data on which the user and the application operate. These are mostly Plain Old CL Object (POCO) classes without any additional behavior. These classes are used to transport input from the user through the application to process, or to display some data (for example, in a tabular format) for the user.

The application logic (also called the controller or business logic) is the application code that adds functionality or behavior to the model. Data logic function usually takes parameters from the user, or takes a model filled with data. After receiving the, the data goes through some kind of validation, and the user gets back another model representing the result. Keeping these things moving around the application is the responsibility of the controller.

The view is a representation of the UI, which is an HTML page in an ASP.NET MVC application. The view provides the surface to display the model (a model can have several views to show the model in different forms), and also allows the user to interact with the data. For example, a model provides a user name, email address, and password; and a registration form represents a related view.

Figure 18-1 shows how the previously described components interact with each other.

![](img/b5597c749e848b27b0d305153ae16106_793_0.png)

As you can see from Figure 18-1, you can reference the model directly, but the model has no knowledge about views using it. The model and the view do not know anything about controllers manipulating them.

## Similar Design Patterns

MVC is not the only design pattern that solves the software engineering problem of decoupling the data from the UI. There are several other design patterns that are very similar to MVC. Let's take a look at two frequently used design patterns.

### Model-View-Presenter

The Model-View-Presenter (MVP) pattern is a derivative of MVC. MVP is a user interface design pattern, and its goal is to help the automated testing of the presentation layer.

In MVC, the controller controls the view and operates on the data, and the view does not know about it. MVP, the view itself holds a reference to a presenter (which is the controller's counterpart in MVC), and when an interaction happens in the view, it delegates the handling of that interaction to its presenter.

Microsoft implemented the MVP pattern in the Web Client Factory, which can be found at http://www.codlex.com/websf.

### Model-View-Model

The Model-View-Model (MVVM) pattern originates from Microsoft and is based on Martin Fowler's Presenter design pattern. However, this pattern was established by Microsoft, primarily for Windows Presentation Foundation (WPF) when it was in its early design stage. Today, WPF 4.0 and Microsoft Silverlight 4.0 also have their own components that help developers use this in patterns.

The model in MVVM has the same role as MVC. View is also the same as the MVC pattern. ViewModel can also be matched to the controller in MVC, but with “extras.” The ViewModel is responsible for binding and connecting the data to the model through WPF’s sophisticated data binding system. The ViewModel executes commands to the view, which can be bound to UI controls (for example, buttons). When the user clicks the button, a command is triggered in the ViewModel.

## Microsoft and the Web Platform

Microsoft's first approach to the web platform was the classic Active Server Pages (ASP) in 1996. It was like VBS for the web. Because of the way VBScript was architected, there was no type checking, just run-time type determination.

When the Microsoft .NET Framework 1.0 was released in 2002, it brought something new to the web developers: ASP.NET 1.0. One of the great things about ASP.NET was that developers were able to choose their favorite programming language to implement an application. ASP.NET leveraged the dynamic compilation feature of the .NET Framework and provided a set of controls ready for rapid development.

ASP.NET 1.0 was implemented an event-based model to the web platform, which was very similar to the one for desktop application developers. Web applications would be stateless by the nature of how HTTP request-responses work, but ASP.NET 1.0 brought a “not-so-stateless” hybrid
