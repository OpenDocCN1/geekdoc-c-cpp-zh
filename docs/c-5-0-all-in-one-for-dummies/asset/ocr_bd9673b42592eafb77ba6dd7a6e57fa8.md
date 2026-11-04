Implementing in the Model reduces work, because it merely entails adding a few lines of code into properties already being implemented in the classes. A main argument against Model implementation revolves around code reuse. For example, if the Model is also used by an ASP.NET application, those events are still raised, but no one is listening. This could potentially present a performance issue. Of course, if you use the same model for WPF and non-WPF Views, then a simple flag passed into the constructor of the Model classes indicating whether the events should be raised or not resolves that issue.

Both ways are valid implementations. Your application and specific situation will most likely dictate where those interfaces are implemented.

In Chapter 3, you discover that if a control doesn’t have an explicit DataContext, it is inherited from the closest parent in the control tree that does have a DataContext explicitly assigned.

When developing WPF applications using the ViewModel pattern, the instantiated ViewModel becomes the Window’s (or user control’s) DataContext.

# Show me the code!

The full code for the ViewModel samples is in the project Chapter4ViewModelModels and Chapter4ViewModelModelsTests in the Chapter4 Solution.

# Just what are you building?

The Window (or View, to use “architecture speak”) is a simple customer maintenance form. The user can select a customer and edit his name and sales region. Clicking the Add Customer button adds a customer to the list. You’re right — not very realistic, but it demonstrates the ViewModel principles. Figure 4-6 shows the completed sample user interface.

![](bbox=[0.15, 0.87, 0.5, 0.94])

# The model

Okay, enough talk. For the sample ViewModel, you need to define a Model.