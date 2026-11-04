If you are viewing something in the designer, you can get to the code-behind related to the file in question by any of three methods:

+   * Click the View Code button in Solution Explorer.
+   * Right-click the design surface and select View Code.
+   * Double-click a control in the designer to generate an event for that control and be moved to Code View.

You'll find yourself using all three over time. Note that you can get directly to the code-behind files by clicking the little triangle next to a designer file and then double-clicking the code files nested within.

# ### Autocompleting with IntelliSense

IntelliSense is Microsoft's autocompletion feature, and it's a prominent part of the Code Editor. You find IntelliSense whether you want to or not. In Code View, click inside a class and press Ctrl+spacebar. Everything you are allowed to type there shows up in a big list.

The nice thing is, IntelliSense is context-sensitive. Type `Console` and press the dot (`.`). All available members of Console appear. IntelliSense keeps you honest and prevents having to remember the two-million-odd members of the .NET Framework on a day-by-day basis.

IntelliSense helps with method signatures, too. Continue the line you started earlier by adding `WriteLine` — in other words, type `Console.WriteLine(` — then check out the IntelliSense. It will tell you all the overloads for the member in question. Use the up and down arrows to move between them. It's slick.

# ### Outlining

Visual Studio will auto-outline your code for you. Notice the little box with a minus sign (–) next to every namespace, class, and method in the code editor (see Figure 2-12)? Those are close-up sections of the code for readability. Doesn't seem like much now, but when you have 2,200 lines of code in there, you will be glad.

You can create your own outlining, too. Preceding a section that you want to outline, put `#region` on a new line. After that section, put `#endregion`. This newly defined section — regardless of whether it's at an existing outline point — will get a new outline mark.

If there is a comment added after a `region` statement, it will show in the collapsed outline — as you can see in Figure 2-12.