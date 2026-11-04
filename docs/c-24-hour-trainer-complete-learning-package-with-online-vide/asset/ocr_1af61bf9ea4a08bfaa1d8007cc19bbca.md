(continued)

You could type in RichTextBoxStreamType followed by a dot to see a list of available choices, but there's an even easier (in other words, better) way to do this: press Ctrl+Space. That makes IntelliSense display a list of things that you might be trying to type. At this point, IntelliSense is smart enough to guess that you want to type RichTextBoxStreamType so it initially selects that type and even displays more information about it, as shown in Figure 7-6.

![](bbox=[0.15, 0.3, 0.85, 0.42])

FIGURE 7-6

Now you can press Tab to make IntelliSense fill in the highlighted value RichTextBoxStreamType for you.

Next, press the "." key to see the list of choices shown in Figure 7-7, pick one, and press Tab to add it to the code. Finally, add a semicolon at the end of the line and you're done.

![](bbox=[0.15, 0.64, 0.75, 0.72])

FIGURE 7-7

I know this sounds like a big mess, but with a little practice it becomes surprisingly quick and easy. Typing everything by hand, I can enter the previous LoadFile statement in about 30 seconds. With IntelliSense's help, I can type the same line in under 10 seconds.

The following code shows how a program can use the SaveFile method. As with LoadFile, the first parameter gives the file's name and the second gives its type:

```
```
contentRichTextBox.SaveFile("Test.rtf", RichTextBoxStreamType.RichText);
```
```

# USING WPF COMMANDS

A program can use commands to manipulate the contents of a RichTextBox. That control also provides commands that the user can invoke interactively. For example, the user can press Ctrl+E to center paragraphs.