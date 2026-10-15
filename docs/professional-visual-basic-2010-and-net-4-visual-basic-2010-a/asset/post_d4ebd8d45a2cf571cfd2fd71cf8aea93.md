
As the preceding code illustrates, the document has two events available within VSTO. The first handles the startup event; the second handles the shutdown event. These are the only two events that are added to your project by default. You’ll learn more about these shortly, but first add another event. This is the BeforeSave event; and as you might expect, it fires just before your document is saved:

```
Private Sub ThisDocument_BeforeSave(ByVal sender As Object, _
    ByVal e As Microsoft.Office.Tools.Word.SaveEventArgs) _
    Handles Me.BeforeSave

Dim res As DialogResult = MessageBox.Show(_
    "Should I save?", "Before Save", _
    MessageBoxButtons.YesNo)

If res = DialogResult.No Then
    ' This code could call a backend data store and then
    ' not save the associated document so the document would remain
    ' unchanged.
    e.Cancel = True
Else
    ' This code would allow you to encourage the user to
    ' always save a new copy of the document
    e.ShowSaveAsDialog = True
End If
End Sub
```

Code snippet from ThisDocument.vb

The preceding code illustrates a custom override of the BeforeSave event on the document. Note that after the event handler is declared, the code creates a local variable to hold a dialog result. It then shows a message box asking the user if it should save. Normally this isn’t something you would do on this event, but in this case it enables you to see two of the attributes of the SaveEventArgs class.

If the user chooses not to save, then you have the option to not save data. Alternatively, you don’t have to offer a choice to the user; instead, you can simply add code ensuring that the user simultaneously saves data to a back-end data store. Whether you need to call a Web service or update a database, this is a good place to call that logic. You then can save to the database and decide whether or not you actually want to update the underlying document. In some cases you might quietly save the data to the database and never save the document; then, when the document is next opened, you retrieve the data from the database as part of the startup. This is a particularly useful trick if you don’t trust the file system’s read-only privileges or you want to ensure that data from multiple different users is properly refreshed each time the document is opened.

Alternatively, you can force the user to perform a “save as” instead of a typical save. This uses the self-explanatory ShowSaveAsDialog property. The idea, again, is that you might not want the user to replace the original document; to keep that from happening, you can have Word automatically prompt the user to save the document with a different name. You can also save data to a database or other data store during this process.

## Adding a Ribbon and an Actions Pane

The preceding work provides some baseline code in your application but it doesn’t provide either a custom ribbon or a custom task pane. Therefore, before testing this, let’s add one of each of these items to the project. To add either of these controls, right-click on your project in the Solution Explorer and then select the Add button to open the Add New Item dialog.

As shown in Figure 25-13, when this dialog opens you can select from one or more categories. In order to manage the available selections, select the Office category. This will reduce the number of available options from dozens to the three that are appropriate for a Word Document project. Start by adding a new ribbon bar. There are two options: XML and visual designer. Select visual designer and enter DocRibbon for your control’s name.

![](img/d99870e80390742f93963da7be0b2e61_860_0.png)

# FIGURE 25-13

Figure 25-13 shows two alternatives for the Ribbon control, for backward compatibility. Previously, if you were customizing a ribbon bar for Office 2007 under Visual Studio 2005 and VSTO 2005 SE, then you didn’t have access to a visual designer for the ribbon bar. Instead, you needed to create and edit an XML file, which would define your ribbon and the controls that were placed on it. There was neither a designer nor a tool customized for this task.

With the release of Visual Studio 2008, the VSTO team had an opportunity to create a visual designer for the ribbon bar. Thus, unless you are working with a legacy XML definition file, you should always select the ribbon with visual design support. Once you have modified the name of the new control to DocRibbon, select OK and return to Visual Studio. The control template will generate the control and open in Design view.

In Design mode, note that if you open the control Toolbox, you have a new category of controls available at the top. The Office Ribbon Controls, shown on the left in Figure 25-14, provide a list of controls that you can add to the default ribbon. Note that these controls are Windows Forms controls, not WPF controls.

![](img/d99870e80390742f93963da7be0b2e61_860_1.png)

# FIGURE 25-14

Add a button to the default Group1 in the designer. Once the button has been added, go to its properties and change the label for the button to “Hide/Show the Actions Pane.” You can optionally add an icon to the button. For this I went into the Visual Studio directory to retrieve one of the icons that ship with Visual Studio 2010. If you navigate to the folder where you installed Visual Studio 10 and navigate the folder tree Common7\VS2010ImageLibrary\1033, within this folder you’ll find a zip file: VS2010ImageLibrary.zip. Within this zip file are several thousand different images and icons that you can leverage within your application. Figure 25-14 shows the updated button display which includes an icon on the left side. The icon named NewDocument.bmp was taken from the VS2010ImageLibrary.

For now, skip implementing a handler for this button, as you want to see the default behavior of the ribbon and the actions pane. Instead, right-click on your project and again request to add a new item. In the Add New Item dialog, select an actions pane and name it DocActionPane. Once you have created your new actions pane you’ll again be in Visual Studio, this time in the designer for your new pane.

Unlike the Ribbon control, the designer for the actions pane doesn’t require a special set of controls and by default has a white background. Unfortunately, I’ve had trouble delineating the edges of the control in a white-on-white scenario. Therefore, before doing anything else, I proceed to the properties for the control and select the BackColor property. Visual Studio 2010 opens a small window with three tabs, Custom, Web, and System, as shown in Figure 25-15.

![](img/d99870e80390742f93963da7be0b2e61_861_0.png)

FIGURE 25-15

This illustrates the default setting for the background, which is the system-defined color for control surfaces. Specifically, the System tab colors are those defined for your system based on setting your own visual preferences. The other two tabs present color options the developer has selected. If you only want to change the display color while you are working on the design and layout, it’s good to capture the original color and then go to the highlighted Custom tab and select a nice bright color such as red to highlight the actual surface area of your actions pane.

Now it’s time to add a simple control to this panel. Once again, drag a button onto the design surface. Orient it in the upper-left corner and change the label to “Load.” Eventually this button will be used to load some data into the document, but this is a good time to test run your project using F5. Your project will start and Visual Studio will start Microsoft Word. When Word opens, your document will display the image that you’ve embedded, as shown in Figure 25-16.

![](img/d99870e80390742f93963da7be0b2e61_861_1.png)

FIGURE 25-16

Figure 25-16 shows your custom document in Word. Note a few things about the running application at this point. First, the tab Add-Ins is set to display the custom ribbon bar. This isn’t an error; even though you have created a custom VSTO Document solution, the customizations you made to the ribbon bar were automatically placed in this section.

Next, Figure 25-16 also captures the message box that was added to the BeforeSave event earlier. Because the Save button in the upper-left corner of the title bar was selected, the event was fired. Below this you see the custom smart graphics that were added to the document itself. So far, so good, but where is the document’s actions pane?

Unlike the ribbon bar, which is automatically associated with your custom document when you add it to your project, the document actions pane needs to be manually associated with your document. As a result, Figure 25-16 does not show your custom actions pane, so your next step is to add that pane to your document, and in this case have it shown or hidden based on the selection of the toggle button added to the ribbon bar. Close the running document and return to Visual Studio once the debugger has stopped.

## Activating the Actions Pane

If you choose to view all files in your project, you can select and open your DocActionPane.Designer.vb source file. Within this file you’ll find that your DocActionPane class inherits from System.Windows.Forms.UserControl. That’s right; the document actions pane is just a customized user control.

Knowing this tells you that you can in fact include not only individual controls, but also panel controls, such as a tab panel, or other custom user controls in this display area. More important, you can take a user control that you might be using in your current application logic and use it with no significant changes within the document’s actions pane. However, anticipating your probable question, the reason the panel didn’t show up is that both Word and Excel expect you to associate a user control with the ActionsPane property of your document.

Because the actions pane is actually open for use by any user control in your project, it is up to you to tell Word which control to assign. View the code for your document in the ThisDocument.vb file. Earlier you saw that the template created the Startup event handler by default. Add to this handler the following line:

```
Private Sub ThisDocument_Startup() Handles Me.Startup

    ActionsPane.Controls.Add(New DocActionPane())

End Sub
```

Code snippet from ThisDocument.vb

That line of code takes the built-in actions pane associated with your document and adds a control to that pane. Of course, you could also add items such as buttons and text boxes directly to your document’s actions pane. However, as the control you added demonstrated, the preferred method is to create a custom user control and add this one control to the embedded actions pane in your document. The New DocActionPane() literally creates a new instance of your user control and places it onto the actions pane.

However, this isn’t very flexible, in that you want users to be able to show or hide that pane. Instead of relying on the built-in controls for displaying or hiding the pane, you want to be able to toggle the actions pane on and off, which is why you have already added a button to the ribbon. That means customizing the Click handler for your toggle button. Before leaving the ThisDocument.vb display, make sure you close this file’s editor so that later you’ll be able to get to the document itself.

Next, select DocRibbon and double-click your button to add an event handler for your ToggleButton1 control’s Click event. This is where you want to alter the status of your actions pane’s display. The way to access the actions pane from the ribbon bar is through the application’s Globals collection. Within VSTO you’ll find a reference to the current document or workbook within this collection. From here you have access to objects such as the actions pane. In fact, you can type Globals.ThisDocument.ActionsPane to get access to the actions pane to which you assigned your user control.
