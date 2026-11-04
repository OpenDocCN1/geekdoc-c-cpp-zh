
## Lesson Requirements

In this lesson, you:

- Add controls to a form and arrange them as shown in Figure 2-9. (Note the form's title and the fact that the form has a non-resizable border.)
- Give the key controls names.
- Set properties at design time on the result label (at the bottom in Figure 2-9) to make the label:
  - Display its text centered.
  - Show a border.
  - Use a 16-point font.
  - Remain invisible until the user clicks one of the buttons.
- Make the OK button be the form's default button so it fires when the user presses Enter. Make the Cancel button be the form's cancel button so it fires when the user presses Esc.
- Add code behind the OK button to display the result label with a green background as shown in Figure 2-9.
- Add code behind the Cancel button to display the result label with a hot pink background and the text "Operation Canceled."

![](img/d5be6ade75773ca6cec5c78f96a98bb1_72_0.png)

FIGURE 2-9

> NOTE You can download the code and resources for this lesson from the website at www.wrox.com/go/csharp24hourtrainer2e.

## Hints

- Create the First Name Label and TextBox first and arrange them. Then copy and paste them to make more Labels and TextBoxes.
- Use the Format menu or Layout toolbar to center the buttons and the result label.

## Step-by-Step

- Add controls to a form and arrange them as shown in Figure 2-9. (Note the form's title and the fact that the form has a nonresizable border.)
  1. Start a new project named NewCustomer. Remember to put it somewhere easy to find.
  2. Use the Properties window to set the form's Text property to New Customer.

8. Make the State ComboBox.
  a. Use the Toolbox to make a ComboBox. Set its Text property to WW and resize it so the text fits reasonably well.
  b. Drag the ComboBox so the snap lines show its baseline aligns with the Labels on that row and its left edge aligns with the left edges of the TextBoxes above.
  c. With the ComboBox selected, look in the Properties window and click the Items property. Then click the ellipsis (...) button on the right to open the String Collection Editor. Enter CO, AZ, WY, UT, and any other state abbreviations that you want to use and click OK. (If you want to enter Confusion and Denial, you'll need to make the ComboBox wider.)
  d. Use the Properties window to set the DropDownStyle property to DropDownList.

> NOTE The DropDownStyle value Simple makes the ComboBox display a TextBox where the user can type and a list below it where the user can make selections.
>
> The value DropDown makes the ComboBox display a TextBox where the user can type and a dropdown arrow that makes a dropdown list appear.
>
> The value DropDownList is similar to DropDown except the user can only select from the dropdown list and cannot type new values. DropDownList is often the best choice because it prevents the user from typing invalid values.

9. Make the Buttons.
  a. Double-click the Toolbox's Button tool twice to make two Buttons with standard sizes.
  b. Drag one Button so it is a nice distance below the TextBoxes. Drag the other Button so it's aligned vertically with the first, positioning it some reasonable distance to the side (the exact distances don't matter here).
  c. Click and drag to select both Buttons. Select Format -> Center in Form -> Horizontally.
  d. Use the Properties window to give the Buttons the Text values OK and Cancel.

10. Use the Toolbox to make the result Label. (Don't worry too much about its size and position right now. Just drop it somewhere close to where it is shown in Figure 2-9.)

Give the key controls names.

- 1. Give the key controls the names shown in Table 2-3. You don't need to give names to the other controls because the program won't need to refer to them. (Actually this example doesn't refer to the TextBoxes or ComboBox either, but a real program certainly would. A form wouldn't contain TextBoxes and ComboBoxes that it won't use.)

## TABLE 2-3

| CONTROL | NAME |
|---|---|
| First Name TextBox | firstNameTextBox |
| Last Name TextBox | lastNameTextBox |
| Street TextBox | streetTextBox |
| City TextBox | cityTextBox |
| State ComboBox | stateComboBox |
| ZIP TextBox | zipTextBox |
| OK Button | okButton |
| Cancel Button | cancelButton |
| Result Label | resultLabel |

- Set properties at design time on the result label (at the bottom in Figure 2-9) to make the label:
  - Display its text centered.
    1. Set the Label's TextAlign property to MiddleCenter. (Use the Properties window's TextAlign editor to select the middle position.)
    2. Set the Label's AutoSize property to False.
    3. Set the Label's Size property to 218, 37. (Or expand the Size property and set the Width and Height sub-properties separately.)
    4. Use the Format menu or Layout toolbar to center the Label on the form.
  - Show a border.
    1. Set the Label's BorderStyle property to Fixed3D.
  - Use a 16-point font.
    1. Expand the Properties window's Font entry. Set the Size sub-property to 16.
  - Remain invisible until the user clicks one of the buttons.
    1. Set the Label's Visible property to False.

- Make the OK button be the form's default button so it fires when the user presses Enter. Make the Cancel button be the form's cancel button so it fires when the user presses Esc.
  1. Click the form and use the Properties window to set the form's AcceptButton property to okButton.
  2. Similarly, set the form's CancelButton property to cancelButton.

Add code behind the OK button to display the result label with a green background as shown in Figure 2-9.

- 1. Double-click the OK button to create an event handler for its Click event.
- 2. Type the bold text in the following code so the event handler looks like this:

```csharp
// Create the new customer.
private void okButton_Click(object sender, EventArgs e)
{
    resultLabel.Text = "New Customer Created";
    resultLabel.BackColor = Color.LightGreen;
    resultLabel.Visible = true;
}
```

Add code behind the Cancel button to display the result label with a hot pink background and the text “Operation Canceled.”

- 1. Double-click the Cancel button to create an event handler for its Click event.
- 2. Type the bold text in the following code so the event handler looks like this:

```csharp
// Don't create the new customer.
private void cancelButton_Click(object sender, EventArgs e)
{
    resultLabel.Text = "Operation Canceled";
    resultLabel.BackColor = Color.HotPink;
    resultLabel.Visible = true;
}
```

Now run the program and experiment with it. Notice what happens when you press the Enter and Esc keys while focus is in a TextBox. See what happens if focus is on one of the Buttons.

## EXERCISES

- 1. [Games] Build a checkerboard similar to the one shown in Figure 2-10. (Hints: The squares are PictureBoxes with different background colors. Give the form a bluish background. Finally, use the Format menu or Layout toolbar to align the controls.)
- 2. [Games, WPF] Repeat Exercise 1 with a WPF application. (Hints: Place colored Rectangles inside a WrapPanel with a width that makes the Rectangles wrap in eight columns.)
- 3. [Games] Make a tic-tac-toe (or naughts-and-crosses) board similar to the one shown in Figure 2-11. (Hints: Make three Labels for each square, named after the rows and columns. For the upper-left square, name them x00Label for the

![](img/d5be6ade75773ca6cec5c78f96a98bb1_76_0.png)

little X Label, ooLabel for the little O Label, and taken00Label for the big Label. Give the smaller Labels Click event handlers that set the Text property of the corresponding big Label. Don't worry about the rules such as not allowing someone to take a square that is already taken.

- 4. [Games, WPF] Repeat Exercise 3 with a WPF application. (Hints: For each square, use a Border with Margin values set to 5. A Border can hold only one content control, so put a Canvas in each Border. Then put the three Labels inside the Canvas. Put the nine Borders inside a WrapPanel sized so they form three columns. See the video Making Event Handlers for instructions on how to make the small Labels act like buttons. Add interesting backgrounds if you like.)
- 5. [Games] Modify the tic-tac-toe program from Exercise 3 so instead of displaying X or O in each square, it displays pictures. Use your favorite football team logos, a cat and a dog, your picture and your boss's, or whatever. (Hints: Use PictureBoxes instead of the large Labels. Add two hidden PictureBoxes to the form. To set their Image properties, click the ellipsis next to the Image property in the Properties window, click the Import button, and browse for the image files. Finally, instead of setting a Label's Text property, the Click event handlers should set the appropriate PictureBox's Image property equal to one of the hidden PictureBox's Image properties. Set all SizeMode properties of the PictureBoxes to Zoom.)
- 6. [WPF] Repeat Exercise 5 with a WPF application. (Hints: Use Image controls instead of the large Labels. Use two Images with Visibility = Hidden to store the X and O images. In an event handler, use code similar to taken21Image.Source = oImage.Source.)
- 7. Make a program with a Label that says "Move Me" and four Buttons with text (0, 0), (200, 200), (0, 200), and (0, 200). Make each Button move the Label to the corresponding position by setting its Left and Top properties.
- 8. [WPF] Repeat Exercise 7 with a WPF application. (Hints: Set the Label's position with code similar to moveMeLabel.Margin = new Thickness(0, 200, 0, 0).)
- 9. The solution to Exercise 7 moves its Label in two steps by setting its Left and Top properties. Modify the program so it sets the Label's Location property in a single step using code similar to this:

```
moveMeLabel.Location = new Point(0, 0);
```

- 10. Build a hotel menu form similar to the one shown in Figure 2-12. (Hints: Copy and paste the Labels and TextBoxes from the Try It program. To set the PictureBox's image, look in the Properties window and click the ellipsis next to the Image property. In the Select Resource dialog, click Import and browse to select a picture. Finally, set the PictureBox's SizeMode property to AutoSize.)

![](img/d5be6ade75773ca6cec5c78f96a98bb1_77_0.png)

FIGURE 2-11

![](img/d5be6ade75773ca6cec5c78f96a98bb1_77_1.png)

FIGURE 2-12
