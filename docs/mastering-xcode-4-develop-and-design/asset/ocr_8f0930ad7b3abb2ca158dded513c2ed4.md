# FIGURE 5.28 Simpler constraints for maintaining vertical spacing

![](bbox=[0.28, 0.17, 0.69, 0.44])

# NEW FUNCTIONALITY

In the springs and struts demo, you needed the custom view so that the button and field would maintain the same vertical distance from each other as the window was resized (to prevent them from overlapping or growing apart).

Here’s where Autolayout with constraints really shines. To get this working the way it should have for years, you’ll remove that custom view and do it right. A simple trick to remove the view without moving the button and field is to select the custom view, then choose Editor > Unembed from the main menu. The custom view is removed and its subviews are left exactly as they are.

To fix the Autolayout constraints, just select the button and the field and drag them to the middle until they snap (as a group) to the blue vertical and horizontal centerlines that appear. You should see something similar to Figure 5.28. Run TestApp, and you’ll see an improvement. Although the text field doesn’t yet size horizontally as before, the button and the field maintain their positions relative to one another without the help of an otherwise pointless custom view. This is because of the vertical space constraint between the field and the button.