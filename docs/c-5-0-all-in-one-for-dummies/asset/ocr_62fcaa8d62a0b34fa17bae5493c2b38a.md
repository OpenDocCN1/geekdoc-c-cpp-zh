errors for a section, you highlight that section, and the snippet will put the try before the selection and the catch at the end.

To use a surround snippet, follow these steps:

+   1. Highlight some code in the Code Designer.
+   2. Press Ctrl+K,S to open the snippets menu.
+   3. Select the appropriate snippet from the menu.
+      You can choose the snippet that is right for whatever you are coding.
+      Try prop for a property getter and setter. To open submenus, use Tab.
+      To close, use Shift+Tab.
+   4. Set the various variables that Visual Studio prompts you with.

The snippet will appear appropriately above and below the selected text.

For instance, if I had this chunk of code:

```
for (int loopcounter = 1; loopcounter <= 10; loopcounter++)
{
    Console.WriteLine(string.Format("The number is {0}.", loopcounter));
}
```

and I felt that I needed a try ... catch block around it, I could highlight that code and do the preceding steps. If I select try from the menu, I will get this:

```
try
{
    for (int loopcounter = 1; loopcounter <= 10; loopcounter++)
    {
        Console.WriteLine(string.Format("The number is {0}.", loopcounter));
    }
}
catch (Exception)
{
    throw;
}
```

the exception is highlighted in green; I can tab to that and add the exception type I am expecting. It's a slick system.

# Making snippets

Snippets are XML files that follow a format understood by Visual Studio. They include a Header and Snippet element. The Header includes a title, which is how the snippet is referred to. The Snippet element, where all the work is done, includes a Code element, which has the code to be inserted.

The best way to make a new snippet is to modify an existing one. Snippets can be found in your Visual Studio install directory, which should be C:\Program Files (x86)\Microsoft Visual Studio 11.0\VC\Snippets\1033 if you are on a 64-bit operating system (otherwise you can drop the x86).