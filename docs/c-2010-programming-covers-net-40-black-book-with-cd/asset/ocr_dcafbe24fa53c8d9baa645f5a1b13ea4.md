The TabControl class has some properties that allow you to work with the tabs in a TabControl control. Table 17.14 lists the noteworthy properties of the TabControl class:

| Table 17.14: Noteworthy Properties of the TabControl Class |
| Property | Description |
| SelectedContent | Retrieves the content in the currently selected tab. By default, the value of the property is a null reference. |
| SelectedIndex | Sets or retrieves the index of the currently selected tab. The starting index of tab is zero, which implies that the first tab in the TabControl control has the index zero, the second tab has the index one, and the rest. If no tab is selected, then value of this property is -1. |
| SelectedItem | Sets or retrieves the currently selected tab. The value of this property is a null reference if no tab is selected. |
| TabStripPlacement | Sets or retrieves a value that indicates the alignment of the tab headers with respect to the tab content. |

The TabControl class has an event named SelectionChanged that occurs whenever you select a tab (TabItem object). The tabs in the TabControl class are instances of the TabItem class. Every TabItem instance can hold a single content, that is, it can hold only one UI control or a group of multiple controls held by a container control.

As you know that, the designer of Silverlight is split into the Design view and XAML view. Both the Design view and XAML view support XAML editing and IntelliSense features as well as navigating between the XAML elements or tags. The Silverlight applications are processed as a tree of nodes. The root node is the Window or MainPage control that has a container control as the child node. The controls that you add become the child nodes of the container control.

Next, let’s discuss about the Silverlight AutoCompleteBox control

# The AutoCompleteBox control

The AutoCompleteBox control is a new control in Silverlight 3.0 and provides a text box where the users can input some data and a drop-down list that displays possible matches as the users type a word or character in the text box. Using the AutoCompleteBox control, users can select an appropriate item from the drop-down list to complete their input in the text box rather than typing the entire word. For instance, if an AutoCompleteBox control contains the names of the days, Monday, Tuesday, Wednesday, and Thursday and a user enters T in the text box, then a drop-down list appears displaying the days, Tuesday and Thursday. Another common example of an AutoCompleteBox control that you might be familiar with is the Google search box. Figure 17.16 shows an AutoCompleteBox control:

![](bbox=[0.3, 0.69, 0.78, 0.92])

Figure 17.16: The AutoCompleteBox Control in Silverlight 3.0