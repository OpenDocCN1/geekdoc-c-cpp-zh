
This chapter focuses on the NSTextView control because it's the most full-featured. If you can work with it, you can easily handle the other controls for displaying text.

## Building an interface

To get started working with text, you need a project and an interface. Perform the following steps to prepare a project for the examples in this chapter:

1. Create a project in Xcode.
2. Double-click the MainMenu.xib file in Xcode in the Resources folder.
3. In Interface Builder, open the Window window from the XIB project window if it isn't already open. Add an NSTextView to the window.

You can find the NSTextView in the Library window by scrolling or searching for NSTextView or simply TextView, as shown in Figure 11-1.

![](img/ea40cad434a338535474e82c1a6ace20_221_0.png)

4. Add two NSButton check box controls to the interface.

One check box toggles the display of a ruler in the NSTextView. The other check box causes text color changes to affect only that text which is selected. You can find the check box control in the Library window by searching for Check Box. Change the title of the check boxes by double-clicking each control and typing the new label. Figure 11-2 shows the check boxes with new titles. Select the Selected property for the top check box, so Apply to Selection is activated only when the application launches. Also, deselect the Selected property in the Button Attributes Inspector for the bottom Rulers check box because the NSTextView rulers aren't visible when the application launches.

5. Drag two NSColorWell controls and two NSTextField labels from the Library to the interface.

You can find the NSColorWell control in the Library window by searching for Color Well. To label the NSColorWell controls, drag two NSTextField controls to the window. The Library has more than one NSTextField control available. Search for Label to find the one that you want here. A Label control is an NSTextField with properties set to make the NSTextField display text that a user can't edit. One NSColorWell dictates the color of the text in the NSTextView. The other represents the background color of the view. Figure 11-3 shows the completed interface.

**Figure 11-2:** Add two NSButton check boxes to the window.

![](img/ea40cad434a338535474e82c1a6ace20_222_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_223_0.png)
![](img/ea40cad434a338535474e82c1a6ace20_223_1.png)

**Figure 11-3:** Add two Color Well controls and two labels to the window.

## Adding a controller class

As you might be expecting, the next step is to create a class that controls your interface:

1. **In the Library window of Interface Builder, search for the NSObject class and add it to the XIB project window.**
2. **With the new object selected, press ⌘+6 to open the Identity Inspector.**
   By default, the Class is `NSObject`.
3. **Change the class name.**
   To follow along with the example, name the class `MyTextController`. Figure 11-4 shows the result.
4. **Add outlets to the class.**
   Define the following outlets for the new class in the same Identity Inspector:
   - `applyCheckbox`
   - `backgroundColorWell`
   - `textColorWell`
   - `textView`

You may notice that one of the NSButton check boxes is missing from the list. That’s because you won’t need to reference it by name in code. Instead, it performs its function through an action.

5. Add the following actions to the `MyTextController` class:
   - `setBackgroundColor:`
   - `setTextColor:`
   - `toggleRuler:`

![](img/ea40cad434a338535474e82c1a6ace20_224_0.png)

**Figure 11-4:** Create a new class to act as the controller.

## Wiring the interface

To wire the components of your interface to the new `Controller` class, perform the following steps:

1. **Connect the outlets of `MyTextController` to the controls in the interface.**
   Control-drag from the XIB window `MyTextController` object to each of the four controls in turn, selecting the corresponding outlet from the black connections list overlay that appears. Figure 11-5 shows the `appleCheckbox` outlet connecting to the Apply to Selection check box.
2. **Connect the actions of the `MyTextController` object to the two ColorWells and the ruler check box.**
   To connect them, Control+drag from each control to the `MyTextController` object. Figure 11-6 shows the `toggleRuler` action connected to its switch.
3. **Select the `MyTextController` class in the project window and choose File→Write Class Files to create the class files and add them to your project in Xcode.**

![](img/ea40cad434a338535474e82c1a6ace20_225_0.png)
![](img/ea40cad434a338535474e82c1a6ace20_225_1.png)

## Adding the code

Now that you’ve assembled the interface for this chapter, it’s time to quit Interface Builder and add some code in Xcode. For starters, you need to specify which superclass **MyTextController** will use. Follow these steps:

1. In **MyTextController.h**, change this line:

   ```objc
   @interface MyTextController : /* Specify a superclass
   (eg: NSObject or NSView) */ { 
   ```

   to this:

   ```objc
   @interface MyTextController : NSObject { 
   ```

The NSColorWell controls in this project display the standard Color panel when a user clicks them. Depending on which NSColorWell a user clicks, it alters either the text color or the background color of the NSTextView in the window respectively.

2. **Add the code to alter both Color panels in the `setBackgroundColor` and `setTextColor` actions in `MyTextController.m`:**

   ```objc
   @implementation MyTextController
   - (IBAction)setBackgroundColor:(id)sender {
       [textView setBackgroundColor:[backgroundColorWell
       color]];
   }

   - (IBAction)setTextColor:(id) sender {
       if ([[applyCheckbox state]) {
           [textView setTextColor:[textColorWell color]
           range:[textView selectedRange]];
       }
       else {
           [textView setTextColor:[textColorWell color]];
       }
   }
   ```

Setting the background and text colors is as easy as using the `setBackgroundColor` and `setTextColor` methods of the NSTextView view. If the state of `applyCheckbox` is YES, the `setTextColor` method sets the color of the text of the currently selected text, passing the range as one of its parameters. This allows you to choose which portion of the text you want to colorize.

3. **To have the two ColorWells display particular colors by default, set them in Interface Builder or do so programmatically in the `awakeFromNib` function.**

For example, the following code sets the default colors for a white background and black text:

```objc
- (void)awakeFromNib
{
    //set the NSColorWells to preset colors
    [textColorWell setColor:[NSColor blackColor]];
    [backgroundColorWell setColor:[NSColor
    whiteColor]];
}
```

The NSTextView control can perform all sorts of other fantastic text manipulation operations besides color. One of these great features is the ruler.

4. **In Xcode, add the following code to the `toggleTheRuler` action to add a full-fledged ruler:**

   ```objc
   - (IBAction)toggleTheRuler:(id) sender
   {
       [textView toggleRuler:[sender state]];
   }
   ```

5. **Choose Build::Build and Go** to see your handiwork.

Figure 11-7 illustrates the use of a ruler in an `NSTextView`.

![](img/ea40cad434a338535474e82c1a6ace20_227_0.png)

**Figure 11-7:** With one line of code, you can add a ruler!

## Doing Style the Easy Way!

You can continue to add style functions to this project by manipulating the `NSTextView` programmatically. This may work great for some projects, but for others, there’s a much easier way to stylize text in an `NSTextView`. If you’re looking for traditional word-processor styles in your application, Cocoa can deliver!

Follow these steps to stylize your text:

1. In Xcode, click the **Build and Go** button in the toolbar to launch the application.
2. Choose Format::Font::**Show Fonts**.

Yes, that’s right . . . Cocoa has already implemented a Font menu for you. You don’t need to add a single line of code nor make any changes in Interface Builder. That’s all there is to it!

3. **Select a font and use it while typing** in the text view.

Figure 11-8 shows the Fonts panel after being opened by the Font menu.
