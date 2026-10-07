Exercises 479

+   6. Created a label and buttons positioned inside the View window.

+   7. Control-click-dragged from the label you created in the View window to the UILabel outlet display.

+   8. Control-click-dragged from each button in the View window to the IBAction method. For each digit, you selected the clickDigit: method. Also, for each digit, you set the tag property to the corresponding digit 0-9 so that the clickDigit: method could identify which button was pressed.

It was a worthwhile exercise learning how to use a view controller, even though it was more work than doing everything in the application delegate object. Hopefully this introduction to developing iOS applications gives you a good start for writing your own iPhone applications. As noted earlier, there are many features offered in UIKit lots for you to explore!

There are several limitations with our fraction calculator application. Many of these are addressed in the exercises that follow.

# Exercises

+   1. Add a Convert button to the fraction calculator application. When the button is pressed, use the Fraction class's convertTo method to produce the numeric representation of the fraction result. Convert that to a string and show it in the calculator's display.

+   2. Modify the fraction calculator application so that a negative fraction can be entered if the - key gets pressed before a numerator is entered.

+   3. If the value of zero is keyed in for a denominator for either the first or second operand, display the Error in the fraction calculator's display.

+   4. Modify the fraction calculator application so that calculations can be chained. For example, allow for the following operation to be keyed:1/5 + 2/7 - 3/8

+   5. You can add an icon to your application that will appear on the iPhone's home screen. This can be by dragging it to the App Icons section as shown in Figure 21.6. For a normal-sized icon (iPhone 3GS and earlier), the icon size should be 57x57 pixels large. For a Retina display iPhone (iPhone 4 and later), the icon image file should be 114x114 pixels.

Find a suitable calculator image on the Internet that you can use and set up the fraction calculator to use this image as its application icon.