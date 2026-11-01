
game is to be played against a computer, then there can only be one human player; otherwise the correct number of human players must be selected.

> **NOTE** Chapter 15 discusses the Styles, Control, and Item templates and shows why you can't always know what type the content of a control is.

## EXERCISES

- 14.1 A `TextBlock` control can be used to display large amounts of text, but the control does not provide any way to scroll the text itself if the text extends beyond the viewport. By combining the `TextBlock` with another control, create a window that contains a `TextBlock` with a lot of text that can be scrolled and where a scrollbar appears only if the text extends beyond the viewport.

- 14.2 The `Slider` and `ProgressBar` controls have a few things in common, such as a minimum, maximum, and current value. Using only data binding on the `ProgressBar`, create a window with a slider and a progress bar, where the `Slider` control controls the minimum, maximum, and current value of the progress bar.

- 14.3 Change the `ProgressBar` in the previous question to display itself diagonally from the bottom-left corner to the top-right corner of the window.

- 14.4 Create a new class with the name `PersistentSlider` and three properties: `MinValue`, `MaxValue`, and `CurrentValue`. The class must be able to participate in data binding and all the properties must be able to notify bound controls of changes.
  - a. In the code-behind of the window you created in the two previous exercises, create a new field of type `PersistentSlider` and initialize it with some default values.
  - b. In the constructor, bind the instance to the window's data source.
  - c. Bind the slider's `Minimum`, `Maximum`, and `Value` properties to the data source.

Answers to the exercises can be found in Appendix A.

## WHAT YOU LEARNED IN THIS CHAPTER

| KEY CONCEPT | DESCRIPTION |
|---|---|
| XAML | XAML is a language that uses XML syntax and enables controls to be added to a user interface in a declarative, hierarchical way. |
| Data binding | You can use data binding to connect properties of controls to the value of other controls. You can also define resources and use code defined in classes outside your views as a data source for both values of properties and as content for controls. `DataContexts` can be used to specify the binding source of existing object instances and thereby allow you to bind to instances that are created in other parts of your application. |
| Routed events | Routed events are special events used in WPF. They come in two flavors: bubbling and tunneling. Bubbling events are first called on the control on which they are activated and then bubble up through the view tree to the root element. Tunneling events move the other way, from the root element to the control that was activated by the user. Both bubbling and tunneling can be stopped by setting the `Handled` property of the event arguments to true. |
| INotifyPropertyChanged | The `INotifyPropertyChanged` interface is implemented by a class that will be used from a WPF view. When property setters of the class are called, they raise the event `PropertyChanged` with the name of the property that changed its value. Any control property that is bound to the property that raised the event will be notified of the change and can update itself accordingly. |
| ObservableCollections | An `ObservableCollection` is a collection that, among others, implement the `INotifyPropertyChanged` interface. You use this specialized collection when you want to provide properties or values that are lists to a WPF view for data binding. |
| Content controls | Content controls can contain a single control in their content. An example of such a control is `Button`. This control can be `Grid` or `StackPanel`; they allow you to create complex customizations. |
| Items controls | Items controls can contain a list of controls in their content. An example of such a control is the `ListBox`. Each control in the list can be customized. |
| Layout controls | You learned to use a number of controls that are used to help you create the view:<br>1. `Canvas` allows for explicit positioning of controls but little else.<br>2. `StackPanel` stacks controls horizontally or vertically.<br>3. `WrapPanel` stacks controls and wraps them to the next line or column depending on the orientation of the panel.<br>4. `DockPanel` allows you to dock controls to the edges of the control or fill the entire content.<br>5. `Grid` allows you to define rows and columns and use these to position the controls. |
| UI controls | UI controls display themselves on the view, often using the layout controls to guide their positions. These controls were used:<br>1. `Label` controls display short text.<br>2. `TextBlock` controls display text that can need multiple lines to display.<br>3. `TextBox` controls allow the users to provide text input.<br>4. `Button` controls allow the users to perform a single action.<br>5. `Image` controls are used to display an image.<br>6. `CheckBoxes` let the users answer yes/no questions such as “Play Against Computer?”<br>7. `RadioButtons` let the users select exactly one from multiple options.<br>8. `ComboBoxes` display a drop-down list of items from which the user can select a single item. The control can also display a `TextBox`, letting the user enter new options.<br>9. `ListBox` controls display a list of items. Unlike the `ComboBox`, the list is always expanded. The control allows for multiple items being selected.<br>10. `TabControls` allows you to group controls on pages. |

If any of these scenarios matches yours, consider using routed commands. In the case of the game, some of the items in the menu should also potentially be available from a toolbar. In addition, the Save action should be available only when a game is in progress and it should potentially be available from both a menu and the toolbar.

> **NOTE** It is important to have the correct default namespace set in the KarliCards GUI project in order to make the examples work. If you get compiler errors stating that a class or resource isn't a member of a namespace, you probably used a different namespace than the one that is being used in the book. The KarliCards solution uses two root namespaces: `Ch13CardLib` for the Ch13CardLib project and `KarliCards_Gui` for the KarliCards GUI project. If you experience problems, try changing the namespaces throughout the projects to match those used in the book.

## TRY IT OUT  Creating the Main Window: KarliCards Gui\MainWindow.xaml

In this example you create the main window for the game. Because this window is the main window of the application, it will use the windows you have already created.

- 1. Add a new window to the project and name it `GameClient.xaml`.
- 2. Change the title to "Karli Cards Game Client" and remove the `Height` and `Width` properties.
- 3. Set the `WindowState` property to `Maximized`.
- 4. Add this namespace:
  `xmlns:src="clr-namespace:KarliCards_Gui"`
- 5. Remove the grid from the window and copy the grid and all its content from the `StartGame` window.
- 6. Delete everything inside the `<Grid>` tags except the canvas that is positioned in `Grid.Row = 0` and the `<Grid.RowDefinitions>`.
- 7. Drag a `DockPanel` control into grid row 1. Set its properties like this:
  `Grid.Row="1" Margin="0"`
- 8. Select `DockPanel` and drag a `Menu` control onto it. Note that the control expands to fill the entire `DockPanel` — this is what you want.
- 9. Change the menu's properties to give it a black background, bold text weight, and white foreground color:
  `Background="Black" FontWeight="Bold" Foreground="White"`
- 10. Right-click the menu in the design view and choose Add MenuItem.
- 11. Change the `Header` property to `_File`. Note the leading underscore. Also, if it isn't already, go ahead and set the foreground to white.
