keys **firstBrush** and **secondBrush** are defined. These two resources are used to set the **Background** property of three buttons (**button1, button2, and button3**). The **StaticResource** markup extension is used to set the **Background** property to the resource values.

+   **5** *Press the F5 key to run the StaticResourcesDemo application. The output appears, as shown in Fig.C#-7.37.*

![](bbox=[0.34, 0.22, 0.61, 0.31])

**Fig.C#-7.37**

In **Fig.C#-7.37**, the three buttons, **button1, button2, and button3** are displayed whose **Background** property is set using a **StaticResource** markup extension.

Let's now learn about dynamic resources.

# ## Using a Dynamic Resource

When you use the **DynamicResource** markup extension, the resource is referred to as a dynamic resource. Compared to static resources, dynamic resources provide more flexibility and are useful in situations when you want to defer the assignment of a property value until run time, for instance, when you want to change the value of the resource at run time through user or system settings.

Unlike static resources that are looked up at the time of loading, dynamic resources are looked up only when they are used at run time. With dynamic resources, an expression is created for the requested resource. This expression is not evaluated until run time. When a dynamic resource is used at run time, the key of the requested resource is looked up in the resources of the element on which the property is being set. If the key is not found, then that key is looked up in the parent element and its resource dictionary up to the root element. If the key is still not found, then the application, theme, and system resources are looked up, in that order.

Let's create a standalone WPF application named **DynamicResourcesDemo** to show the use of dynamic resources. For this, perform the following steps:

+   1. *Repeat steps 1 to 3* as followed earlier while creating the **GridDemo** application in the *Using the Grid Control* section of this chapter.
+   2. *Enter the name* **DynamicResourcesDemo** *in the* **Name** *text box and specify an appropriate location for the application in the* **Location** *combo box.*
+   3. *Click the* **OK** *button. The* **DynamicResourcesDemo** *application is created.*
+   4. *Add the highlighted code given in Listing 7.21, in the* **MainWindow.xaml** *file.*

**Listing 7.21:** Using a Dynamic Resource in XAML

```
```xml
<Window x:Class="DynamicResourcesDemo.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="Demo-DynamicResources" Height="300" Width="300">
    <Window.Resources>
        <SolidColorBrush x:Key="firstBrush" Color="Lavender"/>
        <SolidColorBrush x:Key="secondBrush" Color="PowderBlue"/>
        <SolidColorBrush x:Key="thirdBrush" Color="Violet"/>
    </Window.Resources>
    <Grid Name="grid1" Background="{StaticResource firstBrush}">
```
```