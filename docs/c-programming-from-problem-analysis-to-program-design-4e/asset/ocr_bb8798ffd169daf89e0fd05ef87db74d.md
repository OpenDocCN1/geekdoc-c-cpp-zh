The program in Example 10-20 wired a number of objects to event-handler methods. Table 10-5 shows the event handlers that are registered for specific objects. Two events are registered for the ComboBox object.

**TABLE 10-5** GardeningForm events

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

# CheckBox and RadioButton Objects

Radio buttons and check boxes are two types of objects commonly used in Windows applications. They are often grouped together for discussion; however, they differ in appearance and functionality. You will first explore CheckBox objects.

# CheckBox Objects

CheckBox objects can be added to a Windows form application in the same manner as other objects. If you are using Visual Studio, you drag and drop the control. If you are