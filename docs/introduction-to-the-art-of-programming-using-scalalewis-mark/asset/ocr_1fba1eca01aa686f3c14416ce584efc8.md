contents, like the panels and panes, but you should only add objects of the **Menu** type to a **MenuBar**.

The **Menu** objects are created with `new` and should be passed a `String` that you want as the title of the **Menu**. The `contents` of a **Menu** can be of one of five types.

+   * **MenuItem** - This is the most common thing you will put in a **Menu**. You create them with `new` and the easiest approach is to give them an `Action` object. The `Action` object can be made like a **Button** with a `String` and an action that is passed by-name. For example `new MenuItem(Action("Exit")(exit(0)))`.
+   * **Menu** - You can add a **Menu** to a **Menu**. This will appear as a submenu when you run the program.
+   * **CheckMenuItem** - Menus can also have options on them that are selected. To do this use the type **CheckMenuItem**. You make these with `new` and pass in a `String` for the text to display.
+   * **RadioMenuItem** - If you have multiple values and you only want to allow one to be selected use a **RadioMenuItem**. These are made like **CheckMenuItems**. All the **RadioMenuItems** and you want to have grouped together should be added to a single object of the **ButtonGroup** type.
+   * **Separator** - This is a simple component used to space items out to improve appearance and usability.

We can set up a simple menu system for our recipe script by adding the following code inside the `MainFrame` right before we set the `size`.

```
```
menuBar = new MenuBar {
    contents += new Menu("File") {
        contents += new MenuItem(Action("Open")(openFile))
        contents += new MenuItem(Action("Save")(saveFile))
        contents += new Separator
        contents += new MenuItem(Action("Exit")(exit(0)))
    }
    contents += new Menu("Recipe") {
        contents += new MenuItem(Action("Add")(addRecipe))
        contents += new MenuItem(Action("Remove")(removeRecipe))
    }
}
```
```

In order to get this to run, we have to put declarations of the four functions that are called in the script before we make `frame`. For now these can be left completely empty.

```
```
def openFile {
}

def saveFile {
}

def addRecipe {
}

def removeRecipe {
}
```
```