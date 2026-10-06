
## Introduction to Programming and Problem-Solving Using Scala

- Start replacing characters from the current position.

Most of the time you will probably just use i, but there are occasions when the others can be helpful. The line at the bottom of your terminal should change to show that you are now in edit mode. After you get into edit mode start typing. In vim you can also use the arrow keys with Home, End, Page Up, and Page Down to move around. If you are in a true vi install you will not, instead you will have to return to command mode to move the cursor.

To get back into command mode, simply hit escape (Esc). The bottom line will let you know that you are back in command mode. In command mode you can move the cursor around. In vim the special keys will still work for this. If you are in a true vi install you will need to use the following keys to move around.

- h Move left.
- j Move down.
- k Move up.
- Ctrl-d Page down.
- Ctrl-u – Page up.

You can do other edits while you are in command mode. Here are some of the other keys that do things for you in command mode.

- x Delete a character.
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

## Getting to Know the Tools

If you type in a number before any command, that command will be repeated number of times. This includes going into an edit mode. If you type 100 and 'A', any text you add will be added 100 times when you hit Esc. If that is not what you wanted, you will probably find the 'u' command comes in handy.

Some commands work well in patterns. For example, if you want to do a find and replace where you look out each instance before doing the replace, you might use '/' to search for the first instance, then use 'cw' to replace the word and hit Esc. After that, you use 'n' to move to the next instance of the string and '.' to repeat the 'cw' command if you want to replace that instance. The '.' command is something that would have minimal value in writing a term paper, but comes handy a lot more with programming tasks.

There are a whole set of commands that you invoke by typing a colon. For example, you might have wondered how you save files or how you get out of vi all together. Here are a few of the colon commands that you might find helpful.

- n - Jump to the nth line of the file where n is a number.
- w - Save the file as it is.
- q - Safe quit of vi. This will not work if you have made changes since the last save.
- q! - Unsafe quit of vi. This will quit and throw away any unsaved changes.
- :w - Save the file and quit.

You should spend some time getting used to these commands. If you really want to see what vi can do, read the man page. Many students who are new to vi fall into the pit of hitting 'i' as soon as they start up and use it like Notepad until they are ready to save. This approach ignores the powerful features of vi, in the long run, slows you down. Try to get used to hitting Esc whenever you pause your typing. If nothing else, it will allow you to also hit ':w' so you save your changes frequently. On systems with vim, you can run vimt to get a guided tour.

## vi Settings

You can change settings in vi by editing a file in your home directory with the name ".exrc". In particular, you should consider this line.

```
set tabstop=2
```

This makes it so that tabs display as four characters. You can use 4 if you want, the default is 8 which is a bit too large to work with Scala.

## A.2 Windows

Based on installation statistics, odds are that the computer you most use is Windows. Most of the time you will probably just use i, but there are occasions when the others can be helpful. The line at the bottom of your terminal should change to show that you are now in edit mode. After you get into edit mode start typing. In vim you can also use the arrow keys with Home, End, Page Up, and Page Down to move around. If you are in a true vi install you will not, instead you will have to return to command mode to move the cursor.

To get back into command mode, simply hit escape (Esc). The bottom line will let you know that you are back in command mode. In command mode you can move the cursor around. In vim the special keys will still work for this. If you are in a true vi install you will need to use the following keys to move around.

- h Move left.
- j Move down.
- k Move up.
- Ctrl-d Page down.
- Ctrl-u – Page up.

You can do other edits while you are in command mode. Here are some of the other keys that do things for you in command mode.

- x Delete a character.
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

## Getting to Know the Tools

If you type in a number before any command, that command will be repeated number of times. This includes going into an edit mode. If you type 100 and 'A', any text you add will be added 100 times when you hit Esc. If that is not what you wanted, you will probably find the 'u' command comes in handy.

Some commands work well in patterns. For example, if you want to do a find and replace where you look out each instance before doing the replace, you might use '/' to search for the first instance, then use 'cw' to replace the word and hit Esc. After that, you use 'n' to move to the next instance of the string and '.' to repeat the 'cw' command if you want to replace that instance. The '.' command is something that would have minimal value in writing a term paper, but comes handy a lot more with programming tasks.

There are a whole set of commands that you invoke by typing a colon. For example, you might have wondered how you save files or how you get out of vi all together. Here are a few of the colon commands that you might find helpful.

- n - Jump to the nth line of the file where n is a number.
- w - Save the file as it is.
- q - Safe quit of vi. This will not work if you have made changes since the last save.
- q! - Unsafe quit of vi. This will quit and throw away any unsaved changes.
- :w - Save the file and quit.

You should spend some time getting used to these commands. If you really want to see what vi can do, read the man page. Many students who are new to vi fall into the pit of hitting 'i' as soon as they start up and use it like Notepad until they are ready to save. This approach ignores the powerful features of vi, in the long run, slows you down. Try to get used to hitting Esc whenever you pause your typing. If nothing else, it will allow you to also hit ':w' so you save your changes frequently. On systems with vim, you can run vimt to get a guided tour.

## vi Settings

You can change settings in vi by editing a file in your home directory with the name ".exrc". In particular, you should consider this line.

```
set tabstop=2
```

This makes it so that tabs display as four characters. You can use 4 if you want, the default is 8 which is a bit too large to work with Scala.

## A.2 Windows

Based on installation statistics, odds are that the computer you most use is Windows. Most of the time you will probably just use i, but there are occasions when the others can be helpful. The line at the bottom of your terminal should change to show that you are now in edit mode. After you get into edit mode start typing. In vim you can also use the arrow keys with Home, End, Page Up, and Page Down to move around. If you are in a true vi install you will not, instead you will have to return to command mode to move the cursor.

To get back into command mode, simply hit escape (Esc). The bottom line will let you know that you are back in command mode. In command mode you can move the cursor around. In vim the special keys will still work for this. If you are in a true vi install you will need to use the following keys to move around.

- h Move left.
- j Move down.
- k Move up.
- Ctrl-d Page down.
- Ctrl-u – Page up.

You can do other edits while you are in command mode. Here are some of the other keys that do things for you in command mode.

- x Delete a character.
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

## A.2.1 Files and Directories

As with Unix/Linux, the folders are called directories. There are a number of different commands that can be used for working directories.

- cd/chdir Changes the current directory.
- copy - Copy files from one location to another.
- del/erase - Deletes files. This does not move them to Trash like the GUI. Once this has been executed the files cannot be recovered.
- dir - Lists the contents of the specified directory or the current directory if none is listed.
- md/mkdir - Make the specified directory.
- more - Print the contents of a file one at a time.
- move - Moves a file to a different directory.
- path - Let’s see the current path or change the path.
- ren/rename - Rename an existing file.
- rd/rmdir - Remove a specified directory.
- tree - Display the contents of a directory or drive as an ASCII based tree.
