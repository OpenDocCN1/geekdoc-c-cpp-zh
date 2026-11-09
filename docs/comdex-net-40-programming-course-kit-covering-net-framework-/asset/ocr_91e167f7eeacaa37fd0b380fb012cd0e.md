Note that you can see the .xap file only when the Silverlight application is compiled. This file appears in the **Bin➜Debug** folder inside the Silverlight application project folder.

![](bbox=[0.213, 0.168, 0.275, 0.202])

> > In the Solution Explorer window, you may not be able to view the .xap file within the Silverlight application project folder. To view the .xap file, click the Show All Files button present in the toolbar of the Solution Explorer window.

A .xap file is a unit of deployment and it contains the application manifest and the assemblies of a Silverlight application. The application manifest, stored as **AppManifest.xaml**, is an XAML file that has a list of the assemblies used in the Silverlight application. It uses the **Deployment** and **AssemblyPart** elements for adding the list of the required assemblies as well as the application assembly to the application. The application assembly exists in the **Bin➜Debug** folder after you compile the application and has the same name as the Silverlight application. For instance, the application assembly of a Silverlight application named **SilverlightApplication1** is **SilverlightApplication1.dll**.

![](bbox=[0.213, 0.319, 0.275, 0.348])

> > You can change the extension of a .xap file to .zip and extract the containing files.

Let’s now learn about the controls that can be used to create a Silverlight application in Visual Studio 2010.

# ## Controls Used in Silverlight Applications

Visual Studio 2010 provides various controls to build the UI of the Silverlight 4.0 application. These controls can be added to the Silverlight applications using the XAML and code-behind files. By default, the MainPage.xaml file is created for the UI of a Silverlight application. You can use various XAML elements in this file to design the application. You can also nest the elements within one another and set different properties of these elements as per your requirement.

In Silverlight, controls are represented by different XAML elements. The controls or elements that you add to a Silverlight application become a part of a hierarchical tree that is then rendered to display controls to the clients. In the Silverlight application, a UserControl XAML element is the root element of the hierarchical tree and by default, the UserControl element has a Grid element as its child. If you want to add any control in your application, you need to place that control inside the Grid element such that it becomes the child element of the Grid element.

Table 11.1 shows the list of various controls that can be used in Silverlight 4.0 applications:

| Control | Description | XAML Element Example |
|---|---|---|
| AutoCompleteBox | Represents a control that includes a text box where a user can enter some input and a drop-down list that displays all the possible matches based on the user input. | `<sdk:AutoCompleteBox x:Name="ACB" />` |
| Border | Allows you to add a border and a background to some other control. | `<Border BorderBrush="Blue" BorderThickness="3"/>` |
| Button | Allows you to provide a button that responds to the mouse and keyboard events. | `<Button Content="Hello" ClickMode="Press"/>` |
| Calender | Allows you to view a calendar and work with days, months, and years. | `< Calendar DisplayMode="Month" IsTodayHighlighted="True"/>` |
| Canvas | Allows you to position and arrange the containing controls at given locations. | `<Canvas>`<br>`<Button Content="Hello" Canvas.Left="50" Canvas.Top="50"/>`<br>`</Canvas>` |