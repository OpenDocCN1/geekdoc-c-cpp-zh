
## TABLE 10-4 GardeningForm property values *(continued)*

| Name | Object type | Property | Value |
|---|---|---|---|
| `txtBxResultTrees` | `TextBox` | `Multiline` | `true` |
| `txtBxResultTrees` | `TextBox` | `ScrollBars` | `Horizontal` |
| `txtBxResultTrees` | `TextBox` | `ToolTip` | `Typed "Press and Hold the Ctrl Key for Multiple Selections!"` |
| `txtBxResultFlowers` | `TextBox` | `Text` | `(left blank)` |
| `lblFlowerAnswer` | `Label` | `Text` | `Typed "Flower preference"` |
| `lblTreeAnswer` | `Label` | `Text` | `Typed "Tree preferences"` |
| `menuFile` | `menuItem` | `Text` | `Typed "&File"` |
| `menuExit` | `menuItem` | `Text` | `Typed "Exit"` |
| `menuFormat` | `menuItem` | `Text` | `Typed "F&ormat"` |
| `menuFont` | `menuItem` | `Text` | `Typed "Font"` |
| `menuColor` | `menuItem` | `Text` | `Typed "Color"` |
| `menuHelp` | `menuItem` | `Text` | `Typed "&Help"` |
| `menuAbout` | `menuItem` | `Text` | `Typed "About"` |
| `lblOutput` | `Label` | `Text` | `Typed "Add water!"` |

The program in Example 10-20 wired a number of objects to event-handler methods. Table 10-5 shows the event handlers that are registered for specific objects. Two events are registered for the ComboBox object.

## TABLE 10-5 GardeningForm events

| Object | Event-handler method |
|---|---|
| `lstBxTrees` | `SelectedIndexChanged()` |
| `cmboFlowers` | `SelectedIndexChanged()` |
| `cmboFlowers` | `KeyPress()` |
| `menuExit` | `menuExit_Click()` |
| `menuFont` | `menuFont_Click()` |
| `menuColor` | `menuColor_Click()` |
| `menuAbout` | `menuAbout_Click()` |

For each entry in the table, a statement was added to the GardeningForm.Designer.cs file that registered the method as being the event handler for the particular object. The actual method is raised when the event is fired.

You have now wired and programmed Click(), KeyPress(), and SelectedIndexChanged() events. RadioButton and CheckBox objects fire a different type of event. When their values are changed, they raise CheckedChanged() events. These types of events are discussed in the next section.

## CheckBox and RadioButton Objects

Radio buttons and check boxes are two types of objects commonly used in Windows applications. They are often grouped together for discussion; however, they differ in appearance and functionality. You will first explore CheckBox objects.

## CheckBox Objects

CheckBox objects can be added to a Windows form application in the same manner as other objects. If you are using Visual Studio, you drag and drop the control. If you are developing in a simple text editor, such as Notepad, instantiate an `object` of the `CheckBox` class using the `new` operator. Check boxes usually appear as small boxes that allow users to make a yes/no or `true`/`false` selection. After the objects are placed on the form, `Name` and `Text` properties are normally set for each of the CheckBox objects.

Previous applications used a separate event-handler method for every `object` added to the form. You can, however, write an event-handler method and wire it to more than one control. This is illustrated in the next example. You might want to look ahead to Figure 10-20 to see an example of what the final solution looks like.

> **NOTE**
>
> A new project is started. It is also a Windows application. This application uses one `Button` to allow users to register for swim, snorkel, or dive lessons. The form enables the user to select his or her skill level. The `Text` property for the `Form` `object` is set to “Registration Form”. The `Name` property is set to `RegForm` and the `BackColor` property is set to `DarkBlue`.

### Adding CheckBox Objects

A `TextBox` `object` is added near the bottom of the form to display the final charge for the lessons. Swim lessons cost $50; snorkel lessons cost $25; scuba diving lessons cost $100. A user can select more than one lesson. Three `CheckBox` objects are added to the form. Their `Name` properties are set to `ckBxSwim`, `ckBxSnorkel`, and `ckBxDive`. The `Text` property on each is set to represent the type of lessons along with a cost (that is, `Swim—$50`, `Snorkel—$25`, and `Dive—$100`). A `Label` `object` is used to describe the `TextBox` where the total charges will be displayed. Another `Label` `object` is added near the top of the form describing the `TextBox` `object` to its right, which will accept as input the user's name. Additional `Label` objects are added above and below the check boxes with text of “*Select lesson*” and “*Check all that apply*”.

After the `Text` properties are set for the controls, the `Checked` property of the `CheckBox` objects is reviewed. The `Checked` property is set to either `true` or `false` depending on whether a check mark appears. This property can be set at design time. At run time, the `Checked` property can be set or inspected using an `if` statement to determine which selections are checked by users. All CheckBox objects remain set at their default `false` value.

### Registering CheckBox Object Events

The default event-handler method for CheckBox objects is `CheckedChanged()`. Double-clicking on one of the `CheckBox` objects registers a `CheckedChanged()` event for that one `CheckBox` `object`. The method that is fired checks all the check boxes to see which are checked. This code could be copied and pasted to different methods or the one method could be wired to all three objects. The last option is the better approach. If you copy and paste the code to three methods, any minor modifications that you make require you to make those changes to all three different methods. A run-time or logic error is easily created by this scenario. It is easy to forget to make those slight changes to all three methods. A better approach is to wire a single method to multiple objects.

In Visual Studio, the Form Designer prefixes the name of the event-handler method with the name of the object to which the method is wired. You can change the name of the method so that the method appears to be used by all three objects and not just associated with one object. If you do this, a second step is required. You cannot just change the name of the method in the method heading. You must also change the name of the method in the statement that registered the method to handle the event.

For this example, the original heading for the event-handler method for the Swim CheckBox object was:

```csharp
private void ckbBxSwim_CheckedChanged(object sender, System.EventArgs e) { }
```

The heading of the ckbBxSwim_CheckedChanged( ) method was changed to:

```csharp
private void ComputeCost_CheckedChanged(object sender, System.EventArgs e) { }
```

> NOTE The characters ckbBxSwim were replaced by ComputeCost so that the new method name is ComputeCost_CheckedChanged( ). This makes the code more readable. You could have actually wired the other two events to the method without changing any names; however, it would be more difficult to read and modify later, because it would appear that the method was associated with the Swim CheckBox object only.

If you change the name of the method, the second step you must take uses the new name to register the event for the Swim CheckBox object. Originally, the statement read:

```csharp
this.ckbBxSwim.CheckedChanged +=
new System.EventHandler(this.ckbBxSwim_CheckedChanged);
```

It was changed to:

```csharp
this.ckbBxSwim.CheckedChanged +=
new System.EventHandler(this.ComputeCost_CheckedChanged);
```

> NOTE A quick way to find that program statement in the .Designer.cs file, is to run the application. Double-clicking on the error will take you directly to the line you need to change. Notice that you are only changing the method name inside the parentheses. You do not change the name of the object on the left side of the += symbols.

After those changes are made, you can write the body for the method that will be fired when any of the CheckBox object states change. This method is shown next.
