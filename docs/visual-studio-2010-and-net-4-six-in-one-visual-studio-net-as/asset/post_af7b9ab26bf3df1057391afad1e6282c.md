
more and more tests will succeed. TDD makes for a very tedious process to implement all the classes, constructors, and methods used by a given test.

However now, the Generate From Usage feature is making all this really simple. With this feature, you can create classes, constructors, and methods without actually leaving the current editing position. Consider the following CalculatorTest class:

```swift
[TestClass]
public class CalculatorTest {
    [TestMethod]
    public void AddTestSuccess() {
        var calculator = new Calculator();
        var result = calculator.Add(5, 6);
        Assert.AreEqual(result, 11);
    }
}
```

Visual studios underline Calculator type name, since that's not defined anywhere in the solution.

If you open the smart tag and select the Generate New Type command, the ensuing dialog asks you to tell the IDE the following:

- Kind of item would you like to create (for example, Class, Struct, Enum, or Interface)
- The accessibility of the item you are to create
- A target file for the item from the solution
- An existing file (or an existing file within the project) where the generated item will be appended

As soon as the class is generated, the previously underlined line becomes valid, and then all you must do is add the definition method by invoking the same dialog again, and, add the implementation of the method.

Now, if you run the unit test, it will succeed.

# EXPLORING THE VISUAL DESIGNERS

Visual Studio included a lot of new designers from release to release, and included enhancements to existing ones. In Visual Studio 2010, the following designers have been added or greatly enhanced:

- WPF/Silverlight Designer
- XML Schema Designer

This section discusses new features without going into detail about a specific feature (since you can get more information about them in the following chapters).

# WPF Designer

The WPF Designer was added in Visual Studio 2008, with a basic design-time experience, and targeted to WPF projects. For Silverlight, the design surface was in read-only mode. In Visual Studio 2010, the editor has been enhanced to provide a unified design-time experience for WPF and Silverlight developers alike.

Figure 2-15 shows time-related windows within the IDE using the WPF Designer. A few things in this figure should be noted.

![](img/b5597c749e848b27b0d305153ae16106_67_0.png)

**FIGURE 2-15:** WPF development related windows

In the Toolbox, you will find the full range of controls for platforms, with drag-and-drop support to the editor surface.

On the right side of Figure 2-15, you can see a Document Outline window. This is really handy when you'd like to look at the visual tree and structure of the currently opened XAML file. You can see the Properties grid. This grid is not the one you may have used during Windows Forms development. It's a brand new, extensible, WPF-based grid.

The Properties grid features two tabs: Properties and Events. You can sort the properties alphabetically, or you can sort them by category. However, in Visual Studio 2010, you can type in partial names to filter them. Now when you are looking for a property, it's sometimes faster to type in a few letters, rather than trying to find it by scrolling.

In the middle of Figure 2-15, you will notice the split view of the design surface. You can switch between the split and normal view, or go vertically (instead of horizontally) the XAML views. On the left side of the design surface is a zoom control that enables you to zoom in and out in a fairly high range to get the ideal zoom factor for the given operation.

As you see in Figure 2-15 the Name text box is selected in the editor surface, and the selection is automatically synchronizing the XAML view (TextBox). When a new element is selected either in the XAML view or in the design view, the property of the given element is also selected in the property grid.

A powerful feature of the property grid is that it has a full-blown binding editor embedded. The binding editor can be activated by clicking the property type symbol on the right side of the property name cell. The binding editor itself is represented with an Accordion control, and every aspect of the data binding can be edited here. All edit operations are reflected instantly in the XAML view.

For debugging purposes, Visual Studio 2010 incorporates a WPF tree visualization that enables the run-time inspection of the visual tree of an element. It can be activated from a data tip, Watch window, Autos window, or from the Locals window by clicking the magnifying glass icon next to the name of a WPF object.

# XML Schema Designer

XML Schema Designer is a new addition to the IDE. In previous versions of Visual Studio, developers could only author XML schema through an XML Schema Explorer.

XML Schema Designer is a WPF-based graphical designer that aids with the visualization of the XML schema sets at different levels of abstraction, including the following:

- XML Schema Explorer — This helps the navigation within the XML schema definition.
- Start View — This is the entry point into this designer. Other functions are accessible from here.
- Graph View — This visualizes the relationships between the schema elements.
- Content Model View — This visualizes the details of the schema elements, and expands expanded tiles.

# NEW TOOLS FOR ARCHITECTS

The architect was first introduced in Visual Studio 2008 Team System, but missing from the product were a lot of tasks and tools that can help the architects to do their daily work (such as designing systems, validating code against architecture, or modeling) within the IDE.

Visual Studio 2010 incorporates unified modeling language (UML) support with forward- and reverse-engineering.

The new IDE offers a new project type named Modeling. All architectural items are contained within this project. Figure 2-16 shows a sample business-tier application structure.

![](img/b5597c749e848b27b0d305153ae16106_68_0.png)

FIGURE 2-16: Solution structure with Modeling project

The example solution contains a client application, a service, and some business logic classes. The architect can define the architecture of such system in a layer diagram by creating the boxes for each part of the system and adding dependencies. A layer diagram is a logical representation of the system. The architect can assign projects, namespaces, and types with each element in the diagram. During regular development or at every build, the architecture in the diagram can be validated against the physical solution.

Figure 2-17 shows the layer diagram for the sample solution. Notice the numbers in each box. The UI layer has one ClientApplication project associated, the Service layer has one WCF project assigned, and the Business layer has four business logic classes assigned. The first two assignments were done by dragging and dropping the projects themselves onto the boxes representing each layer. The business logic assignment was done from the Architecture Explorer.

As shown in Figure 2-18, the Architecture Explorer supports easy navigation within the solution:

- Class view — The first level is the namespace level, second level is the class level, and going beneath, the member level (the last level) is the level of method calls.
- Solution view — The first level is the project level, the next is the file level, and from there, the same levels are available as you navigate through the Class.
- File System navigation — This has been added to make the files outside a solution navigable, too.
- Saved DGQL mode — This makes the navigation possible based a saved Direct Graph Query Language (DGQL) file.

![](img/b5597c749e848b27b0d305153ae16106_69_0.png)

![](img/b5597c749e848b27b0d305153ae16106_69_1.png)

As mentioned, full UML editing support is available within the modeling project. One of the powerful features is the capability to reverse a method into a sequence diagram by executing a command from the context menu.
