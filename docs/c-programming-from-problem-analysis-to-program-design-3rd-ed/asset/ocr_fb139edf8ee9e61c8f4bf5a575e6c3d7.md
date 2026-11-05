Figure 3-7 shows the output produced when the user types 16 feet, 3 inches for length; 14 feet, 7 inches for width; and 14.95 for price.

![](bbox=[0.22, 0.24, 0.7, 0.62])

Figure 3-7 Output from CarpetExampleWithClassMethods

Notice that Figure 3-7 includes as the last line “Press any key to continue.” This is placed there because the program was run in Visual Studio using the Debug, Start Without Debugging option (Ctrl+F5) in contrast to the Start Debugging option (F5). This was done to hold the output screen without adding the extra call to the Read( ) method as the last statement in the Main( ) method. The console window screen background and text colors were changed by selecting the Properties option from the command window menu.

Clear the prompts for input by calling the Console.Clear( ) method. This clears the screen and positions the cursor in the top-left corner.

# TYPES OF PARAMETERS

The examples using parameters presented thus far used value parameters. C# offers both call by value and call by reference parameters. Call by value is the default type. With call by value, a copy of the original value is made and stored in a separate, different memory location. If the method changes the contents of the variable sent to it, this does not affect the original value stored in the variable from the calling method. The original value is retained when control passes back to the calling method. There are three other types of parameters available in C#:

+   - ref
+   - out
+   - params