
| Data type | Description | Size (bits) | Range | Sample usage |
|---|---|---|---|---|
| int | Whole numbers (integers) | 32 | −2³¹ through 2³¹ − 1 | int count;<br>count = 42; |
| long | Whole numbers (bigger range) | 64 | −2⁶³ through 2⁶³ − 1 | long wait;<br>wait = 42L; |
| float | Floating-point numbers | 32 | -3.4 x 10⁻³⁸ through 3.4 x 10³⁸ | float away;<br>away = 0.42F; |
| double | Double-precision (more accurate) floating-point numbers | 64 | ±5.0 x 10⁻³²⁴ through ±1.7 x 10³⁰⁸ | double trouble;<br>trouble = 0.42; |
| decimal | Monetary values | 128 | 28 significant figures | decimal coin;<br>coin = 0.42M; |
| string | Sequence of characters | 16 bits per character | Not applicable | string vest<br>vest = "forty two"; |
| char | Single character | 16 | 0 through 2¹⁶ − 1 | char grill;<br>grill = 'x'; |
| bool | Boolean | 8 | True or false | bool teeth;<br>teeth = false; |

## Unassigned local variables

When you declare a variable, it contains a random value until you assign a value to it. This behavior was a rich source of bugs in C and C++ programs that created a variable and accidentally used it as a source of information before giving it a value. C# does not allow you to use an unassigned variable. You must assign a value to a variable before you can use it; otherwise, your program will not compile. This requirement is called the definite assignment rule. For example, the following statements generate the compile-time error message “Use of unassigned local variable ‘age’” because the Console.WriteLine statement attempts to display the value of an uninitialized variable:

Click here to view code image

```
int age;
Console.WriteLine(age); // compile-time error
```

## Displaying primitive data type values

In the following exercise, you use a C# program named PrimitiveDataTypes to demonstrate how several primitive data types work.

### Display primitive data type values

- 1. Start Visual Studio 2015 if it is not already running.
- 2. On the File menu, point to Open, and then click Project/Solution.
  The Open Project dialog box appears.
- 3. Move to the \Microsoft Press\VCSBS\Chapter 2\PrimitiveDataTypes folder in your Documents folder.
- 4. Select the PrimitiveDataTypes solution file, and then click Open.
  The solution loads, and Solution Explorer displays the PrimitiveDataTypes project.

### Note

Solution file names have the .sln suffix, such as PrimitiveDataTypes.sln. A solution can contain one or more projects. Visual C# project files have the .csproj suffix. If you open a project rather than a solution, Visual Studio 2015 automatically creates a new solution file for it. This situation can be confusing if you are not aware of this feature because it can result in you accidentally generating multiple solutions for the same project.

- 5. On the Debug menu, click Start Debugging.
  You might see some warnings in Visual Studio. You can safely ignore them. (You will correct them in the next exercise.)

![](img/16f6e3fe08f01ddadb2741a92c392b0e_75_0.png)

- 6. In the Choose A Data Type list, click string.
  The value “forty two” appears in the Sample Value box.

- 7. Again, in the Choose A Data Type list, click the int type.
  The value “to do” appears in the Sample Value box, indicating that the statements to display an int value still need to be written.

- 8. Click each data type in the list. Confirm that the code for the double and bool types is not yet implemented.

- 9. Return to Visual Studio 2015 and then, on the Debug menu, click Stop Debugging.
  You can also close the window to stop debugging.

## Use primitive data types in code

- 1. In Solution Explorer, expand the PrimitiveDataTypes project (if it is not already expanded), and then double-click MainPage.xaml.
  The form for the application appears in the Design View window.

### Hint

If your screen is not big enough to display the entire form, you can zoom in and out in the Design View window by using Ctrl+Alt+= and Ctrl+Alt+- or by selecting the size from the Zoom drop-down list in the lower-left corner of the Design View window.

- 2. In the XAML pane, scroll down to locate the markup for the ListBox control. This control displays the list of data types in the left part of the form, and it looks like this (some of the properties have been removed from this text):

Click here to view code image

```
<ListBox x:Name="type" ...
    SelectionChanged="typeSelectionChanged">
    <ListBoxItem>int</ListBoxItem>
    <ListBoxItem>long</ListBoxItem>
    <ListBoxItem>float</ListBoxItem>
    <ListBoxItem>double</ListBoxItem>
    <ListBoxItem>decimal</ListBoxItem>
    <ListBoxItem>string</ListBoxItem>
    <ListBoxItem>char</ListBoxItem>
    <ListBoxItem>bool</ListBoxItem>
</ListBox>
```

The ListBox control displays each data type as a separate ListBoxItem. When the application is running, if a user clicks an item in the list, the SelectionChanged event occurs (this is a little bit like the Click event that occurs when the user clicks a button, which is demonstrated in Chapter 1). You can see that in this case, the ListBox invokes the typeSelectionChanged method. This method is defined in the MainPage.xaml.cs file.

- 3. On the View menu, click Code.
  The Code and Text Editor window opens, displaying the MainPage.xaml.cs file.

### Note

Remember that you can also use Solution Explorer to access the code.
Click the arrow to the left of the MainPage.xaml file to expand the node, and then double-click MainPage.xaml.cs.

- 4. In the Code and Text Editor window, find the typeSelectionChanged method.

### Tip

To locate an item in your project, on the Edit menu, point to Find And Replace, and then click Quick Find. A menu opens in the upper-right corner of the Code and Text Editor window. In the text box on this shortcut menu, type the name of the item you’re looking for, and then click Find Next (the right-arrow symbol next to the text box):

![](img/16f6e3fe08f01ddadb2741a92c392b0e_78_0.png)

By default, the search is not case sensitive. If you want to perform a case-sensitive search, click the Match Case button (Aa) below the text to search for.

Instead of using the Edit menu, you can also press Ctrl+F to display the Quick Find dialog box. Similarly, you can press Ctrl+H to display the Quick Replace dialog box.

As an alternative to using the Quick Find functionality, you can also locate the methods in a class by using the class members drop-down list box above the Code and Text Editor window, on the right.

![](img/16f6e3fe08f01ddadb2741a92c392b0e_79_0.png)

The class members drop-down list box displays all the methods in the class, together with the variables and other items that the class contains. (You will learn more about these items in later chapters.) In the drop-down list, click the typeSelectionChanged method, and the cursor will move directly to the typeSelectionChanged method in the class.

If you have programmed using another language, you can probably guess how the typeSelectionChanged method works; if not, Chapter 4, “Using decision statements,” makes this code clear. At present, all you need to understand is that when the user clicks an item in the ListBox control, the details of the item are passed to this method, which then uses this information to determine what happens next. For example, if the user clicks the float value, this method calls another method named showFloatValue.

- 5. Scroll down through the code and find the showFloatValue method, which looks like this:

Click here to view code image

```
private void showFloatValue()
{
    float floatVar;
    floatVar = 0.42F;
    value.Text = floatVar.ToString();
}
```

The body of this method contains three statements. The first statement declares a variable named *floatVar* of type *float*.
The second statement assigns *floatVar* the value 0.42F.

### Important

The *F* is a type suffix specifying that 0.42 should be treated as a *float* value. If you forget the *F*, the value 0.42 is treated as a *double* and your program will not compile, because you cannot assign a value of one type to a variable of a different type without writing additional code—C# is very strict in this respect.

The third statement displays the value of this variable in the value text box on the form. This statement requires your attention. As is illustrated in Chapter 1, the way you display an item in a text box is to set its *Text* property (you did this by using XAML in Chapter 1). You can also perform this task programmatically, which is what is going on here. Notice that you access the property of an object by using the same dot notation that you saw for running a method. (Remember *Console.WriteLine* from Chapter 1?) Also, the data that you put in the *Text* property must be a string and not a number. If you try to assign a number to the *Text* property, your program will not compile. Fortunately, the .NET Framework provides some help in the form of the *ToString* method.

Every data type in the .NET Framework has a *ToString* method. The purpose of *ToString* is to convert an object to its string representation. The *showFloatValue* method uses the *ToString* method of the *float* variable *floatVar* object to generate a string version of the value of this variable. You can then safely assign this string to the *Text* property of the value text box. When you create your own data types and classes, you can define your own implementation of the *ToString* method to specify how your class should be represented as a string. You learn more about creating your own classes in Chapter 7, “Creating and managing classes and objects.”

- 6. In the Code and Text Editor window, locate the *showIntValue* method:

```
private void showIntValue()
{
    value.Text = "to do";
}
```

The *showIntValue* method is called when you click the *int* type in the list box.

- 7. At the start of the *showIntValue* method, on a new line after the opening brace, type the following two statements shown in bold:
