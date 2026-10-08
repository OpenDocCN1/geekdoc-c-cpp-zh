# Introducing the ViewModel

The ViewModel fills that gap. It is designed to be a single class that pulls in all the necessary data points and commands into a one-stop shop for a particular view. Each view typically has its own ViewModel, but that is entirely dependent on your particular application.

As Chapter 3 discusses, WPF automatically monitors any class that either INotifyPropertyChanged (for items bound to a property of a class) and/or INotifyCollectionChanged (for items bound to a collection of items). These interfaces should be implemented in one of two camps — the ViewModel or the Model.

Implementing these two interfaces in the ViewModel is the more academic, textbook implementation. This is because it separates user interface from the Model. It also requires a lot of additional work, because it entails recoding all the properties and collections of your Model to include raising the proper events.

Implementing in the Model reduces work, because it merely adding a few lines of code into properties already being implemented in the classes. A main argument against Model implementation resolves around code reuse. For example, if the Model is used as an ASP.NET application, those events are still raised but no one is listening. This could potentially prevent a performance issue. Of course, if you use the same model for WPF and non-WPF Views, then a simple flag passed into the constructor of the Model classes indicating whether the events should be raised or not resolves that issue.

Both ways are valid implementations. And particular and specific situation will likely dictate where those interfaces are implemented.

In Chapter 3, you discover that if a control doesn't have an explicit DataContext it is inherited from the closest parent in the control tree that has a DataContext explicitly assigned.

When developing WPF applications using the ViewModel pattern, the instantiated ViewModel becomes the Window's (or user control's) DataContext.

# Show the code!

The full code for the ViewModel samples is in the project Chapter4ViewModels and Chapter4ViewModelTests in the Chapter4 Solution.

# Just what are we building?

The Window (or, to use "architecture speak") is a simple customer maintenance form. The user can select a customer and edit his name and

![](bbox=[0.139, 0.783, 0.222, 0.853])