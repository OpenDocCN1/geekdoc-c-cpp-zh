Surround snippets are designed to solve that problem. They are normal snippets with a bit of logic in them that says "This part goes above the selection, and this part goes below the selection." If you want to handle errors for a section, you highlight that section, and the snippet will put the try before the selection and the catch at the end. To use a surround snippet, follow these steps:

+   1. Highlight some code in the Code Designer.
+   2. Press Ctrl+K,S to open the snippets menu.
+   3. Select the appropriate snippet from the menu. You can choose the snippet that is right for whatever you are coding. Try prop for a property getter and setter.
+   4. Set the various variables that Visual Studio prompts you.

The snippet will appear appropriately above and below the selected text.

For instance, if I had this chunk of code:

```
for (int loopcounter = 1; loopcounter <= 10; loopcounter++)
{
    Console.WriteLine(string.Format("The number is {0}.",
    loopcounter));
}
```

and I felt that I needed a try ... catch block around it, I could highlight that code and do the preceding steps. If I select try from the menu, I will get this:

```
try
{
    for (int loopcounter = 1; loopcounter <= 10;
    loopcounter++)
    {
        Console.WriteLine(string.Format("The number is {0}.",
        loopcounter));
    }
catch (Exception)
{
    throw;
}
```

Exception is highlighted in green; I can tab to that and add the exception type I am expecting. It's a slick system.

# Making snippets

Snippets are XML files that follow a format understood by Visual Studio. They include a Header and Snippet element. The Header includes a title.