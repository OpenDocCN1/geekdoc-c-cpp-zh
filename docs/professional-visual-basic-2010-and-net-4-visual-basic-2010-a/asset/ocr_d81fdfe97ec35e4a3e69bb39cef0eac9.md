![](bbox=[0.09, 0.09, 0.75, 0.4])

# FIGURE 25-23

Notice that your custom title for the task pane is displayed. Of course, you could exit Visual Studio right now and open an Excel spreadsheet that was completely unrelated to your current project. However, your code has been registered for COM interop, so if you do this your custom task pane appears within your totally unrelated spreadsheet. This would quickly become annoying, which is why you'll want to display your custom task pane only when the user asks for it.

The next step is to customize your ribbon so that it can control your task pane. First, within your ThisAddIn.vb logic, remove the following line:

```
ProVBTaskPane.Visible = True
```

Next, go to the designer for your ribbon and add a new ToggleButton. You can label this button with some descriptive text. Additionally, select the group control that is already on your ribbon and change the text shown as the label for that control to something such as “ProVB Add-In.” Double-click your new button and add the event handler for the Click event. Within this event you are going to again hide and show the control and update the display text of the button:

```
Private Sub ToggleButton1_Click(ByVal sender As System.Object,
    ByVal e As Microsoft.Office.Tools.Ribbon.RibbonControlEventArgs)
    Handles ToggleButton1.Click

    If ToggleButton1.Checked = True Then
        Globals.ThisAddIn.ProVBTaskPane.Visible = True
        ToggleButton1.Label = "Hide Push Me Pane"
    Else
        Globals.ThisAddIn.ProVBTaskPane.Visible = False
        ToggleButton1.Label = "Show Push Me Pane"
    End If
End Sub
```

Code snippet from RibbonAddIn.vb

The preceding code block should in fact look very similar to what you did within your Document project earlier in this chapter. However, there is a key difference when it comes to referencing the task pane. Notice that instead of accessing the CommandBars collection to make the entire pane display clear correctly, you are instead referencing the local ProVBTaskPane property that you declared in your ThisAddIn class. In addition, instead of a global reference to ThisDocument, you access the ThisAddIn object.