are typed into the text area, they can be retrieved and processed. Example 10–16 shows the two events being registered for the ComboBox control. Notice that the Name property for the ComboBox object was set to `cmboFlowers`.

# Example 10-16

```
this.cmboFlowers.SelectedIndexChanged += new System.EventHandler
        (this.cmboFlowers_SelectedIndexChanged);
this.cmboFlowers.KeyPress += new
        System.Windows.Forms.KeyPressEventHandler
        (this.cmboFlowers_KeyPress);
```

![](bbox=[0.175, 0.316, 0.237, 0.367])

Another option with ComboBox objects is the TextChanged( ) event. The TextChanged( ) event is the default event handler for TextBox objects. The TextChanged( ) event is raised if the Text property is changed by either a programmatic modification or user interaction.

# Programming Event Handlers

To access text from the ComboBox and the ListBox objects shown in Figure 10–7, the event-handler methods are programmed. New TextBox objects are added to store the values retrieved from these controls. Both the cmboFlowers_SelectedIndexChanged( ) method and the cmboFlowers_KeyPress( ) method set the Text property to get the value from the ComboBox object. After retrieving the value, both methods set the text for the associated TextBox object. The body for both of those event handlers contains the following statement:

```
this.txtBoxResultFlowers.Text = cmboFlowers.Text;
```

# Using Collection Indexes

Because the ListBox object allows multiple selections, the Text property cannot be used. Text retrieves a single selection, the first one selected. To retrieve all of the choices, you have several options. You can use the SelectedItems, SelectedIndices, or Items methods to retrieve a collection of items selected. These collections are zero-based structures such as an array. You can access them as you would access an element from an array by taking advantage of the array-like nature.

![](bbox=[0.175, 0.779, 0.237, 0.828])

SelectedIndices is a collection of indexes. Thus, if the first, third, and seventh items were selected, the SelectedIndices collection would contain 0, 2, and 6 because the collection is zero-based.

It is possible to use an int to traverse through the collection of SelectedIndices, as shown in Example 10–17.