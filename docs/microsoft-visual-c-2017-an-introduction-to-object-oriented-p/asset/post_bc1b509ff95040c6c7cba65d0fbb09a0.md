
# CHAPTER 13 Handling Events

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_658_0.png)

**Figure 13-24** Execution of Events with a Single Handler

## Handling Multiple Events with a Single Handler

When a Form contains multiple Controls, you can create a separate event handler for each Control. However, you can also create the same event handler with multiple Controls. For example, suppose you create a Form that contains three Buttons and Label1. The buttons have been labeled A, B, and I. Further suppose you want to display one message when the user clicks a letter button or a number button. In the IDE, you can double-click the second button and create an associated method such as the following:

```csharp
private void Button1_Click(object sender, EventArgs e)
{
    buttonInfoLabel.Text = "You clicked a letter button";
}
```

If you click the second button so its properties are displayed in the IDE's Properties list, you can click the Events icon to see the list of events associated with the second. If no event has been chosen, a list box is available. This list contains all the existing events that have the correct signature to be the event handler for the event. Because the Button1_Click() handler also can handle a Button2_Click() event, you can select it for button2. When you run the program, clicking either letter button produces the output shown in Figure 13-25.

> When you associate an event with Label1, nothing happens when the user clicks it. To complete the application that is running in Figure 13-25, you would want to associate an event with the Button3 to modify the Label1's Text to **You clicked a number button.**

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_658_1.png)

**Figure 13-25** Output of the SingleHandler program after a letter is clicked

- When two or more controls generate the same event, many programmers prefer to generalize the event method. For example, if button1 and button2 call the same method when clicked, it makes sense to name the event LetterButton_Click() instead of Button1_Click().

## Continuing to Learn about Controls and Events

Perhaps you have shopped online at a site that offers multiple ways to “buy now.” For example, you might click a grocery cart icon, choose *Place order now* from a menu, or click a button. Often, *Place order now* buttons are displayed at several locations on the page. If you want to encourage a user’s behavior, you should provide multiple ways to accommodate it.

Watch the video *Managing Multiple Controls.*

## TWO TRUTHS & A LIE Managing Multiple Controls

- 1. The Control TabStop property can be set to true or false; it identifies whether the Control will serve as a stopping place in a sequence of Tab keys.
- 2. On a Form with multiple Controls, one Control must have a TabIndex of 0.
- 3. When a Form contains multiple Controls, you can associate the same event with them.

The false statement is #2. TabIndex is a numeric property that indicates the order in which the controls receive focus. Programmers typically use small numbers for TabIndex values, beginning with 0. The control will receive focus when the user presses the Tab key. However, you might choose not to use any TabIndex values, or if you do, you might choose not to start with 0.

> If you explore the Visual Studio IDE, you will discover many additional Controls that contain hundreds of properties and events. No single book or programming course can demonstrate all of them for you. If you understand programming principles and the syntax and structure of *C#* programs, learning each new *C#* feature becomes progressively easier. When you encounter a new control in the IDE, you can probably use it without understanding all the code generated in the background, but when you understand the background, your knowledge of *C#* is more complete.

Continue to explore the Help facility in the Visual Studio IDE. Particularly, read the brief tutorials here. Also, search the Internet for C# discussion groups. C# is a new, dynamic language, and programmers pose many questions to each other online. These discussions can provide you with valuable information and suggest new approaches to resolving problems.

## You Do It

### Using TabIndex

In the next steps, you create a Form in the Visual Studio IDE and add four Buttons so you can demonstrate how to manipulate their TabIndex properties.

- 1. Open the Visual Studio IDE and start a new project. Define it to be a Windows Forms Application named ManyButtons.
- 2. Change the size of the Form so it is wider and shorter, and change the Text property of Form1 to Many Buttons.
- 3. Draw four buttons onto the Form, and place them so that they are similar to the layout shown in Figure 13-26. Change the Name properties of the buttons to redButton, whiteButton, blueButton, and favoriteButton. Change the Text on the Buttons to Red, White, Blue, and My favorite color, respectively. Adjust the size of the last button so its longer Text is fully displayed.

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_660_0.png)
**Figure 13-26** Four Buttons on the Many Buttons

- 4. Examine the Properties list for the Red button. The TabIndex is 0. Examine the White, Blue, and favorite color buttons. The IDE has set their TabIndex values to 1, 2, and 3, respectively.
- 5. Click the Save All button, and run the program. When the Form appears, the Red button has focus. Press the Tab key, and notice that focus changes to the White button. When you press Tab again, focus changes to the Blue button. Press Tab several more times, and observe that the focus rotates among the Buttons.
- 6. Dismiss the Form.
- 7. Change the TabIndex of the blue button to 0, and change the TabIndex of the Red button to 2. The white button remains 1 and the favorite color button remains 3. Save the program again, and then run it. This time, the Blue button begins with focus. When you press Tab, the order in which the Controls receive focus is Blue, White, Red, then favorite color. (Clicking the Buttons enters no event).

### Associating One Method with Multiple Events

In the next steps, you add three methods to the Many Buttons Form and cause one of the methods to execute each time the user clicks one of the four Buttons.

- 1. If it is not open, the ManyButtons project in the Visual Studio IDE.
- 2. Double-click the Red button on the Form to view the code for the shell of a RedButton_Click() method. Rename the method to start with an uppercase letter, and then, between the method's braces, insert a statement that will change the Form's background color to red as follows:

```csharp
this.BackColor = Color.Red;
```

> At glance, you might think this refers to the Button that is clicked. However, if you examine the RedButton_Click() code in the Form1.cs file in the IDE, you will discover that the method of the Form class refers, therefore. BackColor refers to the Form's BackColor property.

- 3. Select the Form1.cs [Design] tab, and double-click the White button. Rename the generated method, and add the following code to the WhiteButton_Click() method:
```csharp
this.BackColor = Color.White;
```
- 4. On the Form, double-click the Blue button. Rename its Click() method, and add the following statement:
```csharp
this.BackColor = Color.Blue;
```
- 5. On the form, click the My favorite color button. In its Properties list, click the Events button (the lightning bolt). Select the Click event. From the list box next to the Click event, select one of the three events to correspond to your favorite color.
