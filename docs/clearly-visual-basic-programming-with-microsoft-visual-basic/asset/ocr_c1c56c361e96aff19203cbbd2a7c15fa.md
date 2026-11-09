Editor window, the *prompt*, *title*, and *defaultResponse* arguments must be enclosed in quotation marks, unless that information is stored in a String named constant or String variable. The Windows standard is to use sentence capitalization for the *prompt*, but book title capitalization for the *title*. The capitalization (if any) you use for the *defaultResponse* depends on the text itself. The *title* and *defaultResponse* arguments are optional, as indicated by the square brackets in the syntax. If you omit the *title* argument, the project name appears in the title bar. If you omit the *defaultResponse* argument, a blank input area appears when the dialog box opens. In most cases, you assign the value returned by the InputBox function to a String variable, as indicated in the examples in Figure 13-16.

# **INPUTBOX FUNCTION**

Syntax

```
`InputBox(prompt[, title][, defaultResponse])`
```

Example 1

```
`strName = InputBox("Enter your first name:", "Name Entry")`
```

Displays a dialog box that shows “Enter your first name:” as the message, “Name Entry” in the title bar, and an empty input area. Assigns the user’s response to a String variable named strName.

Example 2

```
`strState = InputBox("State name:", "State", "Alaska")`
```

Displays a dialog box that shows “State name:” as the message, “State” in the title bar, and “Alaska” in the input area. Assigns the user’s response to a String variable named strState.

Example 3

```
```
Const strPROMPT As String = "Enter the rate:"
Const strTITLE As String = "Rate"
strRate = InputBox(strPROMPT, strTITLE, ".00")
```
```

Displays a dialog box that shows the contents of the strPROMPT constant as the message, the contents of the strTITLE constant in the title bar, and “.00” in the input area. Assigns the user’s response to a String variable named strRate.

**Figure 13-16:** Syntax and examples of the InputBox function