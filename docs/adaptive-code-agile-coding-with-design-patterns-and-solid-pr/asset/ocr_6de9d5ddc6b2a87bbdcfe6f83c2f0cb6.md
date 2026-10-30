# Specification

For the next set of tests, which build on this Account class, you will test a different part of the business logic layer: a service. The user interface for this hypothetical application could be tethered to any framework—ASP.NET MVC, Windows Presentation Foundation (WPF), or Windows Forms—and your service should be reusable regardless of the framework. This means that the service will contain no dependency specific to any of these frameworks, but it will depend on the Account class, though indirectly. Figure 5-4 shows the dependencies between the layers and classes that will form this example.

![](bbox=[0.122, 0.238, 0.886, 0.619])

**FIGURE 5-4** The dependencies and implementations that form the subsystem you will now test.

The Unified Modeling Language (UML) diagram shows the three packages that make up the three-layered architecture that you will create. The user interface will contain Model-View-Controller (MVC) controllers, although these could be view models or presenters for Model-View-ViewModel (MVVM) or Model-View-Presenter (MVP), respectively. Specifically, the AccountController will have a handler for the user interface action of adding a transaction to an account. This controller has a dependency on the interface of the AccountService that you are preparing to implement.

The AccountService lives in the business logic layer, along with its interface and the domain model, represented by the Account class that was previously implemented. Note that the packages represent the logical layers of the application, as opposed to mapping directly to Visual Studio projects and, therefore, to assemblies. The AccountService will require some way to retrieve Account