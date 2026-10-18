Build and run the desktop app and see the changes...or the lack thereof!

![](bbox=[0.328, 0.091, 0.669, 0.463])

# ## Creating Reminders section

Until now, you were working on a supplementary page of the app. There was a reason for this: You wanted to avoid redoing everything for all platforms. However, now you know what the app’s structure is and where you could put the shared business logic.

# ## Repository pattern

A first idea for implementing the **RemindersViewModel** might involve directly creating, updating and deleting reminders and exposing the data and the actions to **RemindersView**. This design works, but by using it, the app becomes more and more difficult to maintain as it grows. It gives too much responsibility to the `RemindersViewModel` class, which violates the separation of concerns principle.

For instance, when you start integrating a database into the app in later chapters, you would need to update many things in the viewmodel.

One way to mitigate this issue is to use **Repository Pattern**. A repository is an object that sits in between the viewmodel and the source of your data, whether