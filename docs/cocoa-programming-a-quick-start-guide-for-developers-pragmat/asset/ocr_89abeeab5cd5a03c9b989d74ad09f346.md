![](bbox=[0.295, 0.07, 0.617, 0.46])

Set the title for the other button to Forward and its keyboard equivalent to ⌘ →. Next, select the Window, and set its title to SimpleBrowser.

Finally, let’s provide the user with a default value and a hint of how to use our browser. Set the title of the text field to http://pragprog.com either by double-clicking it or by selecting it and setting the value of the title field using the Attributes inspector. Also use the drop-down list in the text field’s Attributes inspector to set the value of Action to Sent on Enter Only. This configures the text field to send its value when the user presses Enter.

Where is the text field’s value sent when the user hits Enter? We haven’t set that yet.

You’re now done creating all of the visual elements of the interface for SimpleBrowser. Use the Cocoa Simulator to take another look at the browse and adjust the sizes of the window or any of the components. Your browser still doesn’t do anything—but we will fix that in the next section.