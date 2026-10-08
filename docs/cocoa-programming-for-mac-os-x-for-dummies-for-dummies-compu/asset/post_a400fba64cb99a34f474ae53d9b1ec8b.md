
## 2. In your application's interface window in Interface Builder, click the NSButton that you want to alter and open the Inspector window. In the Sound field, type the name of the sound file that you want to play or select it from the drop-down list.

Alternatively, you can drag sound files from the Media tab of the Library window directly on top of the push button that you want to play the sound. The sound filename appears automatically in the Sound field of the Inspector window as if you typed it by hand.

Figure 9-4 shows a button that plays the frog system sound.

## 3. Press ⌘+R in Interface Builder to test your work. A frog sound plays when you press ⌘+R.

![](img/ea40cad434a338535474e82c1a6ace20_190_0.png)

## Round button

A close relative to the push button is the round button. As its name implies, the round button has a circular shape, and that's the main difference between a round button and a push button. In addition to text, a round button can display icons. For example, one common use for a round button is as an arrow button.

To set the icon displayed on a button, perform the following steps:

1. **Drag a round button from the Library to the main window of your interface.**
2. **Select an image to use as the button’s icon from the Image drop-down list in the Button Attributes window.**
3. **Set the alignment of the button image.**

Interface Builder provides you with many different default system icons that you can use. For example, Figure 9-5 shows the NSRefreshTemplate image name. **Note:** The vertical alignment of the button doesn’t look so great. Step 3 fixes this.

Conversely, you could add an image file to your project window in Xcode (again, **Xcode**, not Interface Builder). The new image automatically appears in the list of choices in Interface Builder.

![](img/ea40cad434a338535474e82c1a6ace20_191_0.png)

In the Inspector window, click the second button in the Position button. The image on the button now centers vertically, as shown in Figure 9-6. The other elements of the segmented Position button vary the manner in which the button image is aligned in relation to text on the button. The segments display an icon to give you a visual indicator of how that segment aligns the button image.

## Check box

![](img/ea40cad434a338535474e82c1a6ace20_192_0.png)

Figure 9-6: The button's image is centered vertically now.

![](img/ea40cad434a338535474e82c1a6ace20_192_1.png)

So far, you’ve looked at buttons that users click to perform an action. Not all buttons have to trigger an action, though. The check box button, for example, can behave more passively. Rather than firing some action, a check box button might simply indicate a binary state, such as toggling a feature on and off or for answering a Yes/No question. A check box can act like a button, however, in that it’s also capable of triggering an action just like a push button. Figure 9-7 shows a check box control.

You can add a check box to your interface by dragging one from the Library window in Interface Builder. In the Inspector window, you can set the default state of the check box as well as its title and other cosmetic features.

When using check box controls, your code typically checks the state of the control and performs an appropriate operation. To demonstrate, this snippet of code checks the state of a check box control outlet, $\mathit{prefsCheckbox}$, and acts accordingly:

```cpp
if (prefsCheckbox.state)
// Save Preferences
else
// Don't Save Preferences
```

![](img/ea40cad434a338535474e82c1a6ace20_193_0.png)

**Figure 9-7:** A check box button shows the state of a setting.

## Square and rounded bevel buttons

Bevel buttons are another style of button available to you. They come in two varieties: square and rounded. Besides the beveled appearance, they differ from standard push buttons and round buttons in that they often are used to display both text and icons. Further, they can perform other functions that a push button can't.

To add a bevel button to your application, search for **Bevel Button** in the Library window of Interface Builder and then drag one to your interface.

You can use a bevel button like a standard button to trigger an action when a user clicks it. Beyond this simple button behavior, bevel buttons can also mimic other controls. Like the check box, a bevel button can indicate state by displaying a depressed look. Bevel buttons can also act like a menu by displaying a selection from a list of choices. Figure 9-8 shows the square and rounded bevel buttons with the pre-supplied **NSEveryone** and **NSFolderBurnable** images assigned to each button respectively.

![](img/ea40cad434a338535474e82c1a6ace20_194_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_194_1.png)

Figure 9-8: Bevel buttons can display text and icons.

## Radio Control

The radio control is a specialized form of the button that gives a user multiple options. When the user chooses one of these options, the other radio buttons become deselected. Because you typically use more than one radio button at a time, it is customary to use an NSMatrix of radio buttons instead of several individual buttons set to the radio style. An NSMatrix is a collection of cells. A radio button resides in each cell in the NSMatrix.

Follow these steps to add radio buttons to your interface:

1. **Drag the Radio Group control from the Library window.**
   Interface Builder adds a matrix (or group) of radio buttons to your window.
   Figure 9-9 shows the NSMatrix that appears in your window when you drag a radio button control from the Library window.

2. **Double-click the cell and edit the Title text.**
   The Title text becomes editable until you click elsewhere in the interface or press Return.
   You can also change the Title of an NSMatrix element by using the Inspector window.

![](img/ea40cad434a338535474e82c1a6ace20_194_2.png)

![](img/ea40cad434a338535474e82c1a6ace20_195_0.png)

Figure 9-9: Radio buttons usually appear as part of an NSMatrix.

3. Click the `NSMatrix` in your interface and add more radio controls to the `NSMatrix`. Open the Matrix Attributes Inspector window by choosing **Tools··Inspector** and change the **Rows** field of the Cells section, as shown in Figure 9-10.

Figure 9-10 shows an `NSMatrix` with three rows that have edited titles.

![](img/ea40cad434a338535474e82c1a6ace20_195_1.png)

Figure 9-10: Add rows to an NSMatrix in the Matrix Attributes Inspector window for that control.

4. Connect the **NSMatrix** to an outlet of a **Controller** class by **Control+dragging** from the controller to the NSMatrix control.

When connecting an outlet to an NSMatrix, make sure that you Control+drag from the Controller class to the entire matrix, not to an element of the matrix. If one element becomes highlighted when you Control+drag from the controller to the NSMatrix, move the cursor around until a dark outline appears around the entire NSMatrix (see Figure 9-11).

![](img/ea40cad434a338535474e82c1a6ace20_196_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_196_1.png)

After you have an outlet to the NSMatrix, you can find out which element the user selected in code by using the selectedRow method of NSMatrix. The selectedRow method returns an integer indicating the index of the currently selected row. Row numbers start from the top, with the first row having an index of 0. To illustrate, here’s a sample action that checks the selectedRow of colorRadios. Based on the index, it displays a message in the console telling you which color was chosen:

```objc
- (IBAction) doSomething: (id) sender
{
    switch ( [colorRadios selectedRow] )
    {
        case 0:
            NSLog(@"User chose red.");
            break;
        case 1:
            NSLog(@"User chose green.");
            break;
        case 2:
            NSLog(@"User chose blue.");
            break;
    };
}
```
