# Introduction to Programming and Problem-Solving Using Scala

+   - Start replacing characters from the current position.

Most of the time you will probably just use i, but there are occasions when the others can be helpful. The line at the bottom of your terminal should change to show that you are now in edit mode. After you get into edit mode start typing. In vim you can also use the arrow keys with Home, End, Page Up, and Page Down to move around. If you are in a true vi install will not, instead you will have to return to command mode to move the cursor.

To get back into command mode, simply hit escape (Esc). The bottom line will let you know that you are back command mode. In command mode you can move the cursor around. In vim the special keys will still work for this. If you are in a true vi install you will need to use the following keys to move around.

+   - h Move left.
- j Move down.
- k Move up.
- 1-d Page down.
- Ctrl-u – Page up.

You can do other edits while you are in command mode. Here are some of the other keys that do things for you in comand mode.

+   - x Delete a character.
- dd Delete a line and place on the clipboard. (Precede with a number for multiple lines).
- yy or Y Yank a line. This copies to the clipboard. (Precede with a number for multiple lines).
- p Paste the clipboard after the current line.
- P Paste the clipboard before the current line.
- r Replace a single character.
- J Join lines.
- / Search for something. Enter the search string after the /.
- n Repeat the last search.
- cw Change the current word. This removes up to the next white space and goes into insert mode.
- . Repeat the last command.
- u Undo the last command.
- Ctrl-r Redo the last undone command.