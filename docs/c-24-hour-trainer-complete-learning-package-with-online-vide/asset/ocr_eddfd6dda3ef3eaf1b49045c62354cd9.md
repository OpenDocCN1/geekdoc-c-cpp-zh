little X Label, ooLabel for the little O Label, and taken00Label for the big Label. Give the smaller Labels Click event handlers that set the Text property of the corresponding big Label. Don't worry about the rules such as not allowing someone to take a square that is already taken.

+   4. [Games, WPF] Repeat Exercise 3 with a WPF application. (Hints: For each square, use a Border with Margin values set to 5. A Border can hold only one content control, so put a Canvas in each Border. Then put the three Labels inside the Canvas. Put the nine Borders inside a WrapPanel sized so they form three columns. See the video Making Event Handlers for instructions on how to make the small Labels act like buttons. Add interesting backgrounds if you like.)
+   
+   5. [Games] Modify the tic-tac-toe program from Exercise 3 so instead of displaying X or O in each square, it displays pictures. Use your favorite football team logos, a cat and a dog, your picture and your boss's, or whatever. (Hints: Use PictureBoxes instead of the large Labels. Add two hidden PictureBoxes to the form. To set their Image properties, click the ellipsis next to the Image property in the Properties window, click the Import button, and browse for the image files. Finally, instead of setting a Label's Text property, the Click event handlers should set the appropriate PictureBox's Image property equal to one of the hidden PictureBox's Image properties. Set all SizeMode properties of the PictureBoxes to Zoom.)
+   
+   6. [WPF] Repeat Exercise 5 with a WPF application. (Hints: Use Image controls instead of the large Labels. Use two Images with Visibility = Hidden to store the X and O images. In an event handler, use code similar to taken21Image.Source = oImage.Source.)
+   
+   7. Make a program with a Label that says "Move Me" and four Buttons with text (0, 0), (200, 200), (0, 200), and (0, 200). Make each Button move the Label to the corresponding position by setting its Left and Top properties.
+   
+   8. [WPF] Repeat Exercise 7 with a WPF application. (Hints: Set the Label's position with code similar to moveMeLabel.Margin = new Thickness(0, 200, 0, 0).)
+   
+   9. The solution to Exercise 7 moves its Label in two steps by setting its Left and Top properties. Modify the program so it sets the Label's Location property in a single step using code similar to this:
+   
+   10. Build a hotel menu form similar to the one shown in Figure 2-12. (Hints: Copy and paste the Labels and TextBoxes from the Try It program. To set the PictureBox's image, look in the Properties window and click the ellipsis next to the Image property. In the Select Resource dialog, click Import and browse to select a picture. Finally, set the PictureBox's SizeMode property to AutoSize.)

![](bbox=[0.7, 0.15, 0.88, 0.42])

FIGURE 2-11

```
moveMeLabel.Location = new Point(0, 0);
```

![](bbox=[0.55, 0.78, 0.88, 0.95])

FIGURE 2-12