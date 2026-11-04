```
makeBinding.Mode = BindingMode.OneTime;
BindingOperations.SetBinding(lblCarMake,
    Label.ContentProperty, makeBinding);

Binding modelBinding = new Binding("Model");
modelBinding.Mode = BindingMode.OneTime;
BindingOperations.SetBinding(lblCarModel,
    Label.ContentProperty, modelBinding);

}
this.DataContext = car;
```

Run the application and observe that it runs the same way as when the bindings were defined using XAML.

![](bbox=[0.15, 0.38, 0.25, 0.52])

Dependency properties are typically defined with the suffix "Property," but you only see them this way navigating MSDN documentation and accessing them through code. In XAML, you specify dependency property attributes by dropping the "Property" suffix on the name.

# Editing, Validating, Converting, and Visualizing Your Data

In the preceding section, you got a taste of binding syntax and saw data appear on the screen. This section builds on this knowledge and shows you a simple example of updating data, from user interface elements as well as updating the user interface with changes happening to objects behind the scenes.

![](bbox=[0.12, 0.7, 0.22, 0.85])

The complete solution is available on the web in the BindingSample2 project.

To do this, follow these steps:

+   1. Create a new WPF Application project and name it BindingSample2.
+      Reuse the Car class that you created in BindingSample1 (Note: If copying and pasting this class, ensure you change the namespace of the class to BindingSample2.)
+      In this example, you display the make and model of a Car object (the DataContext) in TextBox controls. This enables you to edit the values of the Car properties. You will also use a TwoWay data binding mode so that changes made from the user interface will be reflected in the underlying Car object, and any changes made to the Car object from code-behind will be reflected in the user interface.
+   2. Define two buttons, one that shows a message box containing the current value of the DataContext, the other that forces changes to the DataContext through code-behind.

In MainWindow.xaml, replace the Grid content with this: