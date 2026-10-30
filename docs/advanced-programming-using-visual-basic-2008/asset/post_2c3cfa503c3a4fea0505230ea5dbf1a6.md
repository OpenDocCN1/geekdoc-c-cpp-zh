
## Working with Strings

Visual Basic provides many methods for working with text strings. Strings in Visual Studio are immutable, which means that once a string is created, it cannot be changed. Although many programs in this text seem to modify a string, actually a new string is created and the old string is discarded.

For string handling, you can use any of the many methods of the String class. You can also use the StringBuilder class, which is more efficient if you are building or modifying strings, since the string can be changed in memory. In other words, a StringBuilder is mutable (changeable) and a String is immutable.

Here is a partial list of the methods in the String class. For shared methods, you don’t need to specify a String instance; for nonshared methods, you must attach the method to the String instance. For example:

Shared Method

```
If Compare(AString, BString) > 0 Then
    ...
```

Nonshared Method

```
If MyString.EndsWith("ed") Then
    ...
```

| Method | Returns |
|---|---|
| Compare(AString, BString) (Shared) | Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| Compare(AString, BString, IgnoreCaseBoolean) (Shared) | Case insensitive if IgnoreCaseBoolean is True.
Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| Compare(AString, AStartInteger, BString, BStartInteger, LengthInteger) (Shared) | Compare substrings; start position indicates beginning character to compare for a length of LengthInteger.
Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| Compare(AString, AStartInteger, BString, BStartInteger, LengthInteger, IgnoreCaseBoolean) (Shared) | Case insensitive if IgnoreCaseBoolean is True.
Compare substrings; start position indicates beginning character to compare for a length of LengthInteger.
Integer:
Negative if AString < BString
Zero if AString = BString
Positive if AString > BString |
| EndsWith(AString) | Boolean. True if the String instance ends with AString. Case sensitive. |
| Equals(AString) | Boolean. True if the String instance has the same value as AString. Case sensitive. |
| IndexOf(AString) | Integer. Index position in String instance that AString is found. Positive: String found at this position. Negative: String not found. |
| IndexOf(AString, StartPositionInteger) | Integer. Index position in String instance that AString is found, starting at StartPositionInteger. Positive: String found at this position. Negative: String not found. |
| IndexOf(AString, StartPositionInteger, NumberCharactersInteger) | Integer. Index position in String instance that AString is found, starting at StartPositionInteger, for a length of NumberCharactersInteger. Positive: String found at this position. Negative: String not found. |
| Insert(StartIndexInteger, AString) | New string with AString inserted in the String instance, beginning at StartIndexInteger. |
| LastIndexOf(AString) | Integer. Index position of AString within String instance, searching from the right end. |
| LastIndexOf(AString, StartPositionInteger) | Integer. Index position of AString within String instance, searching leftward, beginning at StartPositionInteger. |
| LastIndexOf(AString, StartPositionInteger, NumberCharactersInteger) | Integer. Index position of AString within String instance, searching leftward, beginning at StartPositionInteger, for a length of NumberCharactersInteger. |
| PadLeft(TotalLengthInteger) | New String with String instance right justified; padded on left with spaces for a total length of TotalLengthInteger. |
| PadLeft(TotalLengthInteger, PadChar) | New String with String instance right justified; padded on left with the specified character for a total length of TotalLengthInteger. |
| PadRight(TotalLengthInteger) | New String with String instance left justified; padded on right with spaces for a total length of TotalLengthInteger. |
| PadRight(TotalLengthInteger, PadChar) | New String with String instance left justified; padded on right with the specified character for a total length of TotalLengthInteger. |
| Remove(StartPositionInteger, NumberCharactersInteger) | New String with characters removed from String instance, beginning with StartPositionInteger for a length of NumberCharactersInteger. |
| Replace(OldValueString, NewValueString) | New String with all occurrences of the old value replaced by the new value. |
| StartsWith(AString) | Boolean. True if the String instance starts with AString. Case sensitive. |

## The Startup Object

When a project begins execution, the startup form is loaded into memory. Set the startup form in Project/ProjectName Properties.

## Declaring and Showing Forms

To show a form, you instantiate an object of the form’s class and show it.

```
Dim ProgramSummaryForm As New SummaryForm
ProgramSummaryForm.Show()
```

or

```
ProgramSummaryForm.ShowDialog()
```

The Show method shows the form as a regular window, called a modeless window. The ShowDialog method displays the form as a modal window (dialog box), which means that the user must respond to the dialog box before switching to another window in the application.

VB also provides a default instance of each form in a project, so it isn’t necessary to declare and instantiate a form before showing it.

```
SummaryForm.Show()
```

## Closing Forms

Use Me.Close() to close the current form, or NamedForm.Close() to close any other form. The keyword Me refers to the current class and is assumed if omitted, so you can close the current form with just Close().

## Form Properties

The two properties of a form that you always set are the Name and Text. You also can choose whether to display minimize and maximize buttons, a close button, and a control box (the system menu that pops up at the left end of the title bar). If you want to display a form with no title bar, you must set ControlBox to false and Text to an empty string.

## Size and Location Properties

When a form is first displayed, it uses several properties to determine the location and size. Set the StartPosition to set its position on the screen. WindowState determines whether the form displays in the size you created it or maximized or minimized.

The Location property determines the form’s placement in its container, and the Size property sets the size in pixels.

Set the IsMdiContainer property to true for a parent form that will hold child forms. To create a child form, you cannot set a property at design time; instead you must set the parent in code:

```
Dim FirstChildForm As New FirstChildForm()
FirstChildForm.MdiParent = Me
FirstChildForm.Show()
```

## Accept and Cancel Buttons

One of the buttons on a form should be the accept button and one should be the cancel button. When a user types information on a form, generally he or she wants to press the Enter key when finished, rather than pick up the mouse and click a button. Set the form's AcceptButton to the button that should activate when the user presses Enter; set the CancelButton to the button to activate when the user presses the Escape key. Good programmers make sure to set an accept button on every form and a cancel button when appropriate.

## Form Events

These events occur in this order when a form first loads into memory:

| New | The constructor. Occurs once when the form is instantiated. |
| Load | Occurs once before the first time the form is displayed. The controls on a form are not available during the Load event; therefore, you cannot set the focus in this event handler. This procedure is the location most programmers use for initialization tasks. |
| Activate | Occurs when a form becomes the active window. During a project with multiple forms, the Activate event occurs each time the user switches from one form to another. The Deactivate event occurs for the form losing active status. |

These events occur as a form's life ends.

| Deactivate | Occurs when the form loses focus to another form in the project. It does not occur if the user switches to another application, the application closes, or the form closes. |
| Closing | Occurs just before the Closed event. This gives the programmer a chance to cancel the close process if necessary. |
| Closed | Occurs after the form is closed. Most programmers place cleanup code in this event handler. |

## Using Multiple Forms

A project can show and hide multiple forms. Each form is a class and can have Public and Private members. You can access the Public members (variables and procedures) of one form from another. However, this is considered poor form as it violates rules of encapsulation. Note that members declared with the Friend keyword are public to any other forms in the project.
