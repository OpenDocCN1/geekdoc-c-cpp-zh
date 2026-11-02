# # FlipView Features and Styling

The `WinJS.UI.FlipView` is a very capable and flexible control for any situation where you want to page through items in a data source one at a time. We saw the basics earlier, in “Quickstart #2,” so let’s now see the rest of its features through the other scenarios of the HTML FlipView control sample. (It’s worth mentioning again that although this sample demonstrates the control’s capabilities in a relatively small area, a FlipView can be any size. Refer again to Guidelines for FlipView controls for more.)

Scenario 2 in the sample (“Orientation and Item Spacing”) demonstrates the control’s `orientation` property. This determines the placement of the arrow controls: left and right (`horizontal`) or top and bottom (`vertical`) as shown below. It also determines the enter and exit animations of the items and whether the control uses the left/right or up/down arrow keys for keyboard navigation. This scenario also lets you set the `itemSpacing` property (an integer), which determines the number of pixels between items when you swipe items using touch (below right). Its effect is not visible when using the keyboard or mouse to flip; to see it on nontouch devices, use touch emulation in the Visual Studio simulator to drag items partway between page stops.

![](bbox=[0.136, 0.425, 0.503, 0.589])

![](bbox=[0.53, 0.425, 0.894, 0.589])

Scenario 3 (“Using interactive content”) shows the use of a renderer function instead of a declarative template, as we learned about in “How Templates Work with Collection Controls.” Scenario 3 uses a renderer (a function called `myTemplate` in `js/interactiveContent.js`) to create a “table of contents” for the item in the data source marked with a “contentArray” type.

![](bbox=[0.139, 0.695, 0.456, 0.836])

Scenario 3 also sets up a listener for `click` events on the TOC entries, the handler for which flips to the appropriate item by setting the FlipView’s `currentPage` property. The picture items then have a back link to the TOC. See the `clickHandler` function in the code for both of these actions.