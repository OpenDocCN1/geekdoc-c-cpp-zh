used to it). The first view in the Options panel is the General view. Here you can change the default options for statement completion, various behavior settings, and what the Code Editor should display aside from the code.

After you click the little triangle next to the C# node, you see the General panel (which is the default view) and then the other panels you can use:

+   - **Tabs:** This section is for people who are obsessive about the tabbing of their source code. The Tabs panel determines how many spaces make up a tab, and whether Visual Studio should insert them automatically.
+   - **Advanced:** This section should probably be called *Miscellaneous*. Everything that doesn't fit into other categories is here. In this section, handling comments, interface implementation, and refactoring details all have a checkbox that basically says "If you don't like it when Visual Studio does this, click here."
+   - **Formatting:** Formatting in C# is very in-depth. Generally, C# coders are a little persnickety about the look of their code. Visual Studio does a lot of work to help make your code look the way you want it, but you have to tell it what to do. Options for formatting include:
+     - Automatic formatting
+     - Indentation
+     - Newlines
+     - Spacing
+     - Wrapping
+   - **IntelliSense:** The most interesting field is the list of characters that "commit" an IntelliSense selection. By typing one of these characters, you select the highlighted IntelliSense member. Usually, I just use space or dot (.) but there are many more options, and I had no idea!

# Neat stuff

I provide a canonical list of the options that I always forget are in here, but that I have to use frequently. Right now, they probably won't make a lot of sense, but you may remember them when you need them later.

+   - To implement a new source control provider, first install the package (for instance, Turtle for CodePlex's SVN implementation, or Team System) and then go to Source Control in Options to pick the one you want to use. Just one at a time!
+   - Many people recommend that you store your projects in a short file path, like c:\Projects. You can change where you store projects in the Projects and Solutions section in the options dialog box.