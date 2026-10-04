# Basic Filters

In jQuery you can use filters to filter the result set from the selector. This opens a lot of possibilities because it enables you to get elements the first, last, all even or odd ones, all headings, or at a specific location. The table after the next exercise lists the most-used filters and gives an example of how to use them. To follow along these examples and many that follow, carry out this exercise, which sets up a test page for most of the jQuery examples.

# TRY IT OUT Setting up a jQuery Demo Page

In this exercise, you create a new demo page you can try out many of the examples in this chapter, by replacing a single line of code.

+   1. Create a page based on your custom template and call it jQueryDemo.aspx. Give the page a title and then in the cpMainContent placeholder add the following:
```html
<h1>First Header</h1>
<table id="DemoTable">
  <tr><td>Row 1<td>Cell 1</td><td>Cell 2</td></tr>
  <tr><td>Row 2<td>Cell 1</td><td>Cell 2</td></tr>
  <tr><td>Row 3<td>Cell 1</td><td>Cell 2</td></tr>
  <tr><td>Row 4<td>Cell 1</td><td>Cell 2</td></tr>
  <tr><td>Row 5<td>Cell 1</td><td>Cell 2</td></tr>
</table>
<h2 style="font-style: italic; font-weight: bold;">Header</h2>
<input id="Button1" type="button" />
<input id="Text1" type="text" />
<input id="Checkbox1" type="checkbox" />
<input id="Checkbox2" type="checkbox" />
```

You don't have to type all this code yourself. Instead, you can use VS to write most of it for you. Make use of the Table Menu and the HTML category of the Toolbox.

+   2. Add a content block for the cpClientScript before cpMainContent with the following code:
```html
</Content>
<asp:Content Id="Content3" runat="server" PlaceHolderID="cpClientScript">
<script>
$(function () {
  // Examples go here
});
</script>
</asp:Content>
```

+   3. Replace the line // Examples go here with the following code to test your setup:
```css
$('#DemoTable').css('background-color', 'green');
```

+   4. Save your changes and press Ctrl+F5 to open the page in your browser. If all went well, the background color of the cells in the table turned.

+   5. Close your work and go back to VS. Press Ctrl+Z to undo your last changes until you see the // Examples go here line again, and save the page.