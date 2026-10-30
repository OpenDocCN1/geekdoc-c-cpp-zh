Listing 12-30 shows how the continuing example could use convention over configuration for registering.

# LISTING 12-30 The registration phase can be greatly simplified by using conventions.

```
private void OnApplicationStartup(object sender, StartupEventArgs e)
{
    CreateMappings();

    container = new UnityContainer();
    container.RegisterTypes(
        AllClasses.FromAssembliesInBasePath(),
        WithMappings.FromMatchingInterface,
        WithName.Default
    );

    MainWindow = container.Resolve<TaskListView>();
    MainWindow.Show();

    ((TaskListController)MainWindow.DataContext).OnLoad();
}
```

The registrations have been replaced by a call to RegisterTypes, which is the method used to provide the container with instructions on how to find classes and map them to interfaces. The instructions provided in this example tell the container to:

+   - Register all classes from the assemblies in the bin folder (which is the base path).
+   - Map those classes to the interface that matches the name of the class. The convention here is that the Service implementation class would be registered against the IService interface.
+   - Use the default to name the mapping when registering each mapping. This default is null, meaning that the mapping is unnamed.

The container will iterate through each public class in each assembly that is in the bin folder, find its implemented interfaces, and map it to the one that matches the class's name (prefixed with an I, for Interface), without providing a name for the mapping. It is not hard to imagine that the resulting registration will be quite greedy, potentially registering more classes to interfaces than you usually would if you were registering manually. However, a more important concern is whether it correctly registers the classes you want to the correct interfaces. This is the new problem introduced by conventions.

The registration is undeniably simpler than its previous incarnation, but only insofar as it is shorter: fewer lines of code. With registration by configuration, it was easy to comprehend which implementation was being used for each interface—and that they were definitely registered correctly.

The first parameter to RegisterTypes is a collection of the types to register. The AllClasses static class provides some helper methods for retrieving such a collection by using various common strategies. The second parameter requires a function that accepts a Type passed in from the collection in the first parameter—the implementation type—and returns a collection of Type instances to