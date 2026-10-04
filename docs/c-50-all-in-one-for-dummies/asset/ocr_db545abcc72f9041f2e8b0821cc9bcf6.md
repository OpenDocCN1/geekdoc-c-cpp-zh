# 636 Get Your ViewModel

"object graph") that represents the data for your application. In a sales application, example objects could be classes like Customer, SalesRegion, and SalesPerson.

# Business Layer (BL)

The BL is the implementation of the business rules for the application. This layer ensures that the data in the Model adheres to the law of the land.

# View

The View represents the pieces of the application that interact with the data. For WPF, it is the collection of Windows that compose the application.

The biggest gap with displaying an object graph (Model) in a View is that applications seldom display only one type of object at a time. If the Window allows for editing a customer, then it probably needs to display the sales regions, pages, and so forth.

Combining multiple objects into a data object clouds the Model, and placing all code into the view places puts too much knowledge in the View - not to mention a total inability to unit test the code. The compilation of the required parts of the object graph should not detract from any other part of the application.

The command objects are another consideration. There isn't a tidy place in the traditional application layer to place the custom commands. The code contained in the commands is (typically) Business Logic, but the Window needs to bind to the commands and is therefore specific to the View.

# Introducing the ViewModel

The ViewModel fills that gap. It is designed to be a single class that pulls in all the necessary data points and commands into a one-stop shop for a particular view. Each view has its own ViewModel, but that is entirely dependent on your particular application.

As Chapter 3 discusses, WPF automatically monitors any class that implements INotifyPropertyChanged (for items bound to a property of a class) or INotifyCollectionChanged (for items bound to a collection of items). These interfaces should be implemented in one of two cases — the ViewModel or the Model.

Implementing those two interfaces in the ViewModel is more the academic, textbook implementation. This is because it separates user interface code from the Model. It also requires a lot of additional work, because it entails recoding all the properties and collections of your Model to include raising the proper events.