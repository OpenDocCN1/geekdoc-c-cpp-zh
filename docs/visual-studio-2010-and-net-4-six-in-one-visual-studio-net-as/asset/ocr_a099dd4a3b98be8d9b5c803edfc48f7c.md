The model generally can be tested separately from other parts of the application — with the well-known unit testing techniques — because it is independent from the view and from the controller. The view is just plain UI, and the only logic behind it is the one that simply binds the element of the model to the elements of the UI.

However, testing a controller is tougher, because it has a dependency on the underlying model that generally uses some kind of persistence. If you want to test a controller from the model, your model must be mocked, and there also must be a way to inject a model into the controller. When your live runs, the controller gets the real model instance; when it is tested, a fake model can be injected into it.

Using a fake model is important from the TDD perspective. Even if you do not have your model implemented, you must be able to test a controller — and that is where you are going to use the fake model.

# What Needs to Be Changed?

There are several ways to satisfy controller testing requirements, and one possibility is demonstrated here. This approach follows the refactoring steps on the AcmeLibrary MVC application to support unit tests for the BookController class:

+   The application uses the interface-based development pattern to define the responsibilities of the model (Book) as an interface (IBook).

+   With the help of the repository pattern, the model operations executed by the BookController class have been extracted into a repository interface (IBookRepository).

+   The BookController class has been refactored so that it can accept an injected model.

+   A new unit test project has been added to the solution.

+   The classes defining the domain model of the AcmeLibrary application (entity interface, repository interface) have been moved to a separate assembly that can be referenced by both the web application's assembly and the unit test's assembly.

+   A fake model class (fake repository) has been defined for test purposes.

+   A few unit test method has been coded.

You may think that these steps generate a lot of work. That's true — however, it's not so much. But there are a few arguments that are worth mentioning:

+   If you start designing and implementing your MVC application with testing in mind, you do not need to change the application. You can build it right in the proper way.

+   With refactoring tools, you can automate the process of refactoring work. For example, you can extract the model and repository interfaces from the current implementation classes.

+   Tests applied from the beginning of the implementation give you confidence and mitigate the risk of bugs discovered too late — assuming they run successfully, and bugs discovered fixed.