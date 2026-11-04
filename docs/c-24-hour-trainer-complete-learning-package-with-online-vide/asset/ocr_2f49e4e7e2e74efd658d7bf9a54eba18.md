+   - An Image.
+   - A StackPanel holding a Label and a TextBox.
+   - A Grid containing a 3 × 3 arrangement of RadioButtons.

14. Make a Windows Forms program with five levels of nested menus. In other words, make a menu File → Level 1 → Level 2 → Level 3 → Level 4 → Level 5. Make the bottommost menu item display a message box. (Again, I'm not saying this is a good idea in an actual program.)

15. [WPF] Repeat Exercise 14 with a WPF application.

16. A useful user interface technique is to not allow the user to do things that are inappropriate at the time. In a drawing application, for example, if the user isn't editing a drawing, you should disable the drawing tools.

Write a program that has three menus: File, Customers, and Employees. Give them each one menu item: Exit (and give it code), New Customer, and New Employee.

Give the program's form three RadioButtons labeled General, Manage Customers, and Manage Employees. When the user clicks a RadioButton, enable and disable the appropriate menus. (Some applications hide inappropriate menus, but that can be confusing to users who know a menu should exist but can't find it.)

For example, when the user clicks the Manage Customers button, enable the Customers menu and disable the Employees menu. Disable both menus when the user clicks the General button. (Hint: Make sure the program starts with the correct menus enabled.)

17. [WPF] Repeat Exercise 16 with a WPF application.

18. Generally it's better to use as little code as possible so you have less to program, debug, and maintain over time. Copy the application you wrote for Exercise 5-16 and change it so all three RadioButtons share a single event handler.

19. [WPF] Repeat Exercise 18 with the WPF application you wrote for Exercise 17. (Hint: IsChecked.Value tells whether a RadioButton is checked.)

> NOTE Please select the videos for Lesson 5 online at www.wrox.com/go/csharp24hourtrainer2evideos.