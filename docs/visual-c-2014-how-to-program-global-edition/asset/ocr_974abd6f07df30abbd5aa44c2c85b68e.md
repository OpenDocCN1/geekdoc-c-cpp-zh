# 15.6 ListBox Control 655

Click on third LinkLabel
to open Notepad

![](bbox=[0.212, 0.15375, 0.796, 0.26925])

Fig. 15.14 | Using LinkLabels to create hyperlinks. (Part 3 of 3)

The event handlers for LinkLabels method Start of class Process (namespace System.Diagnostics), allows you to execute other programs, load documents or web sites from an app. Method Start can take one argument, or one, two arguments, to run and its command-line arguments. Method Start’s arguments can be in the same form as if they were provided for input to the Windows Run command (Start > Run...). For apps known to Windows, full names are not needed, and the file extension can be omitted. To open a file of a type that Windows recognizes (and how to handle), simply use the file's full name. For example, if you pass the a .docx file, Windows will open it in Microsoft Word (whatever is registered to open .docx files, if any). The Windows operating system must be able to use the app associated with the file’s extension to open the file.

The event handler for dLinkLabelClicked events the C: drive (lines 19–26). Line 23 sets the Linked property to true, which changes the link’s color from blue to purple (the LinkVisited colors can be configured through the Properties window in Visual Studio). The event handler then passes "C:\" to method Start (line 25), which indicates that all characters in the string are interpreted literally—this is known as a verbatim string, the backslash within the string is not considered to be the first character of an escape sequence. This simplifies representing directory paths, you do not need to use \ for each \ character in the path.

The event handler for detailLinkLabelClicked events (lines 29–36) opens the web page www.deetail.com in the user’s default browser. We achieve this by passing the web-address as a string (line 35), which opens the web page in a new browser window or tab. Line 33 sets the Linked property to true

The event handler for notepadLinkLabel events (lines 39–48) opens the Notepad app. Line 43 sets the Linked property to true so that the link appears as a visited link. Line 47 passes the argument "notepad" to method Start, which runs notepad.exe. In neither, the extension is required—Windows automatically recognizes the argument given to method Start as an executable file.

# 15.6 ListBox Control

The ListBox allows the user to view and select from multiple items in a list. ListBoxes are static GUI entities, which means users cannot directly edit the list of items.