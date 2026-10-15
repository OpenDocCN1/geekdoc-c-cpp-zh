+   - MonthCalendar
+   - NotifyIcon
+     - Gives a form an icon in the system tray
+     - ToolTip of the icon is set by the Text property of the control.
+     - Pop-up menus are set using a ContextMenu control (see the “Menus” section earlier in chapter).
+   - NumericUpDown
+     - A single-line text box that displays a number and up/down buttons that increment/decrement the number when clicked
+   - PictureBox
+     - Image property defines the graphic to display instead of Picture.
+     - Use the SizeMode property to autostretch or center the picture.
+   - ProgressBar
+     - Has a Step method that automatically increments the value of the progress bar by the amount defined in the Step property
+   - RadioButton
+     - Use CheckAlign and TextAlign to specify where the radio button and text appear in relation to the area of the control.
+   - RichTextBox
+     - Use the Lines array to get or set specific individual lines of the control’s text.
+   - TabControl
+     - Has a TabPages collection of TabPage objects. A TabPage object is a subclass of the Panel control specialized for use in the TabControl.
+     - Uses the Appearance property to display the tabs as buttons, if desired (formerly the Style property of the TabStrip control)
+   - TextBox
+     - Now has a CharacterCasing property that can automatically adjust the text entered into uppercase or lowercase
+     - The ReadOnly property is used to prevent the text from being edited.
+     - Now has Cut, Copy, Paste, Undo, and ClearUndo methods
+   - Timer
+     - Special version of Timer that conforms to the Windows Forms threading model (Don’t use Timer classes from other namespaces in Windows Forms.)
+   - TrackBar
+   - TreeView
+   - VScrollBar
+   - WebBrowser
+     - Even smart client applications often need to display HTML or browse websites. The WebBrowser control is in an intelligent wrapper around the browsing control built in to Windows.

# Handling Groups of Related Controls

Occasionally it is necessary for a set of controls to be treated as a group. For example, a set of RadioButton controls might be related, and you might want to channel the Click event for all the controls in the group to the same event handler.