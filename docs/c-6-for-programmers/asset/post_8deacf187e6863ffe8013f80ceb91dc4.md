
| Custom-control techniques and PaintEventArgs properties | Description |
|---|---|
| *Custom-Control Techniques* | |
| **Inherit from a Windows Forms control** | You can do this to add functionality to a preexisting control. If you override method `OnPaint`, call the base class’s `OnPaint` method. You can only add to the original control’s appearance, not redesign it. |
| **Create a UserControl** | You can create a `UserControl` composed of multiple preexisting controls (e.g., to combine their functionality). You place drawing code in a Paint event handler or overridden `OnPaint` method. |
| **Inherit from class Control** | Define a brand new control. Override method `OnPaint`, then call base-class method `OnPaint` and add the code to draw the control. With this method you can customize both control appearance and functionality. |
| *PaintEventArgs Properties* | |
| **Graphics** | The control’s graphics object, which is used to draw on the control. |
| **ClipRectangle** | Specifies the rectangle indicating the boundary of the control. |

**Fig. 15.49** | Custom-control creation.

## Clock Control

We create a “clock” control in Fig. 15.50. This is a `UserControl` composed of a Label and a Timer—whenever the Timer raises an event (once per second in this example), the Label is updated to reflect the current time.

```csharp
// Fig. 15.50: ClockUserControl.cs
// User-defined control with a Timer and a Label.
using System;
using System.Windows.Forms;

namespace ClockExample
{
    // UserControl that displays the time on a Label
    public partial class ClockUserControl : UserControl
    {
        // constructor
        public ClockUserControl()
        {
            InitializeComponent();
        }
    }
}
```

**Fig. 15.50** | User-defined control with a Timer and a Label. (Part 1 of 2.)

```csharp
// update Label at every tick
private void clockTimer_Tick(object sender, EventArgs e)
{
    // get current time (Now); convert to string
    displayLabel.Text = DateTime.Now.ToLongTimeString();
}
```

![](img/3f5ef6be1748bb746e5f71a483bba4d0_534_0.png)

**Fig. 15.50** | User-defined control with a Timer and a Label. (Part 2 of 2.)

## Timers

**Timers** (System.Windows.Forms namespace) are non-visual components that generate Tick events at a set interval. This interval is set by the Timer’s **Interval** property, which defines the number of milliseconds (thousandths of a second) between events. By default, timers are disabled and do not generate events.

## Adding a User Control

This app contains a user control (ClockUserControl1) and a Form that displays the user control. Create a Windows app, then create a UserControl class by selecting **Project > Add User Control...**. This displays a dialog from which we can select the type of item to add—user controls are already selected. We then name the file (and the class) ClockUserControl. Our empty ClockUserControl is displayed as a grey rectangle.

## Designing the User Control

You can treat this control like a Windows Form, meaning that you can add controls using the ToolBox and set properties using the Properties window. However, instead of creating an app, you’re simply creating a new control composed of other controls. Add a Label (displayLabel) and a Timer (clockTimer) to the UserControl1. Set the Timer interval to 1000 milliseconds and set displayLabel’s text with each Tick event (lines 18–22; the default event). To generate events, clockTimer must be enabled by setting property Enabled to true in the Properties window.

Struct **DateTime** (namespace System) contains property **Now**, which returns the current time. Method **ToLongTimeString** converts Now to a string containing the current hour, minute and second (along with AM or PM, depending on your locale). We use this to set the time in displayLabel in line 21.

Once created, our clock control appears as an item in the ToolBox in the section titled *ProjectName Components*, where *ProjectName* is your project’s name. You may need to switch to the app’s Form before the item appears in the ToolBox. To use the control, simply drag it to the Form and run the Windows app. We gave the ClockUserControl1 object a white background to make it stand out in the Form. Figure 15.50 shows the output of Clock, which contains our ClockUserControl. There are no event handlers in Clock, so we show only the code for ClockUserControl.

### Sharing Custom Controls with Other Developers

Visual Studio allows you to share custom controls with other developers. To create a UserControl that can be exported to other solutions, do the following:

- 1. Create a new Class Library project.
- 2. Delete Class1.cs, initially provided with the app.
- 3. Right click the project in the Solution Explorer and select Add > User Control.... In the dialog that appears, name the user-control file and click Add.
- 4. Inside the project, add controls and functionality to the UserControl (Fig. 15.51).

![](img/3f5ef6be1748bb746e5f71a483bba4d0_535_0.png)

Fig. 15.51 | Custom-control creation.

- 5. Build the project. Visual Studio creates a .dll file for the UserControl in the output directory (bin/Debug or bin/Release). The file is not executable; class libraries are used to define classes that are reused in other executable apps. You can give the .dll file to other developers and they can follow Steps 6 and 7.
- 6. Create a new Windows app.
- 7. In the new Windows app, right click the ToolBox and select Choose Items.... In the Choose Toolbox Items dialog that appears, click Browse.... Browse for the .dll file from the class library created in Steps 1–5. The item will then appear in the .NET Framework Components tab of the Choose Toolbox Items dialog. If it’s not already checked, check this item. Click OK to add the item to the Toolbox. This control can now be added to the Form as if it were any other control.

### 15.15 Wrap-Up

Many of today’s commercial apps provide GUIs that are easy to use and manipulate. Because of this demand for user-friendly GUIs, the ability to design sophisticated GUIs is an essential programming skill. Visual Studio’s IDE makes GUI development quick and easy. In Chapters 14 and 15, we presented basic Windows Forms GUI development techniques. In Chapter 15, we demonstrated how to create menus, which provide users easy access to an app’s functionality. You learned the DateTimePicker and MonthCalendar controls, which allow users to input date and time values. We demonstrated LinkLabels, which are used to link the user to an app or a web page. You used several controls that provide lists of data to the user—ListBoxes, CheckedListBoxes and ListViews. We used the ComboBox control to create drop-down lists, and the TreeView control to display data in hierarchical form. We then introduced complex GUIs that use tabbed windows and multiple document interfaces. The chapter concluded with demonstrations of visual inheritance and creating custom controls. In Chapter 16, we introduce string and character processing.

## 16
## Strings and Characters:
A Deeper Look

## Objectives

In this chapter you'll:

- - Create and manipulate immutable character-string objects of class `string` and mutable character-string objects of class `StringBuilder`.
- - Use various methods of classes `string` and `StringBuilder`.
- - Manipulate character objects of struct `Char`.
- - Use regular-expression classes `Regex` and `Match`.

**Outline**

- 16.1 Introduction
- 16.2 Fundamentals of Characters and Strings
- 16.3 string Constructors
- 16.4 string Indexer, Length Property and CopyTo Method
- 16.5 Comparing strings
- 16.6 Locating Characters and Substrings in strings
- 16.7 Extracting Substrings from strings
- 16.8 Concatenating strings
- 16.9 Miscellaneous string Methods
- 16.10 Class StringBuilder
- 16.11 Length and Capacity Properties, EnsureCapacity Method and Indexer of Class StringBuilder
- 16.12 Append and AppendFormat Methods of Class StringBuilder
- 16.13 Insert, Remove and Replace Methods of Class StringBuilder
- 16.14 Char Methods
- 16.15 Introduction to Regular Expressions (Online)
- 16.16 Wrap-Up

## 16.1 Introduction

This chapter introduces the .NET Framework Class Library’s string- and character-processing capabilities and demonstrates how to use regular expressions to search for patterns in text. The techniques it presents can be employed in most kinds of applications, and particularly in text editors, word processors, page-layout software, computerized typesetting systems and other kinds of text-processing software. Previous chapters presented some basic string-processing capabilities. Now we discuss in detail the text-processing capabilities of class string and type char from the System namespace and class StringBuilder from the System.Text namespace.

We begin with an overview of the fundamentals of characters and strings in which we discuss *character constants* and *string literals*. We then provide examples of class string’s many constructors and methods. The examples demonstrate how to determine the *length* of strings, *copy strings*, *access individual characters* in strings, *search strings*, obtain *substrings* from larger strings, *compare strings*, *concatenate strings*, *replace characters* in strings and convert strings to *uppercase or lowercase* letters.

Next, we introduce class StringBuilder, which is used to assemble strings dynamically. We demonstrate StringBuilder capabilities for determining and specifying the size of a StringBuilder, as well as *appending*, *inserting*, *removing* and *replacing* characters in a StringBuilder object. We then introduce the character-testing methods of struct Char that enable a program to determine whether a character is a digit, a letter, a lowercase letter, an uppercase letter, a punctuation mark or a symbol other than a punctuation mark. Such methods are useful for validating individual characters in user input. In addition, type Char provides methods for converting a character to *uppercase or lowercase*.

We provide an online section at http://www.deitel.com/books/CSharpFP that discusses regular expressions. We present classes Regex and Match from the System.Text.RegularExpressions namespace as well as the symbols that are used to form regular expressions. We then demonstrate how to *find patterns* in a string, *match entire strings to patterns*, *replace characters* in a string that match a pattern and *split strings* at delimiters specified as a pattern in a regular expression.
