
![](img/36e48639a06772bcb0fa1ea2525b33a3_1130_0.png)

**FIGURE A-8** Text Editor display option

You also specify whether you have **Statement completion** set to **Auto list members** and/or have **Statement completion** with **Parameter information** displayed from the **Text Editor, C#, General** option. When you select **Display Line numbers**, the line numbers are displayed to the left of the source code in the IDE.

The **Tabs** node, which is immediately below the **General** option, enables you to specify the amount of space inserted when a tab or indent is set and whether tabs or spaces are inserted for tabs. From this option, you can also set **Smart indenting** so that it automatically indents the next line, if a statement doesn't fit on a single line. Smart indenting does not always work the way you think it should. As the name implies, it tries to be smart and sometimes you have to override it.

The **Formatting** option under the **Text Editor** expands to reveal a number of features grouped under **General**, **Indentation**, **New Lines**, **Spacing**, and **Wrapping**. As shown in Figure A-9, from the **Text Editor, C#, Formatting, New Lines** option you can decide whether you prefer to place your braces on a new line for types, methods, and control blocks. This is how braces have been displayed in this book.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1131_0.png)

**FIGURE A-9** Formatting settings for C# text editing

As illustrated in Figure A-9, this is where you indicate whether keywords like `else`, `catch`, and `finally` should appear on a separate line. When you make those selections, IntelliSense places the keywords and braces on a separate line and helps with proper indentation.

Selecting **Indent case contents**, **Indent case labels**, and **Indent block contents** causes the indentation to occur automatically and can really increase your productivity. You select these settings under the **Indentation** option for **Formatting** within the **C# Text Editor** node.

Explore the **Spacing** options under the **Text Editor, C#, Formatting** node. You set spacing for method declarations, method calls, casts, delimiters, and binary operators. You determine whether to have a space inserted between the name and open parenthesis or inside empty square brackets. Some of these settings are shown in Figure A-10.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1132_0.png)

**FIGURE A-10** Space settings for C# text editing

You also **Set spacing for operators** under the **Text Editor, C#, Formatting, Spacing** node. This is the last option shown in Figure A-10. Here you can specify whether you want Visual Studio to automatically insert spaces before and after arithmetic operators, like + and =. The selection **Insert space before and after binary operators** was used for examples in this book.

### Debugging

A number of settings can be changed under the **Debugging** folder node. You should review the options that can be set. They include features such as **Ask before deleting all breakpoints**, **Break all processes when one process breaks**, and **Enable breakpoint filters**.

The **Enable Edit and Continue** under the **Edit and Continue** option lets you edit the code without ending the debug session. This allows you to change your source code while your program is still running, but in break mode.

### HTML Designer

Selections made using this node impact your development environment when you are designing Web sites. If you prefer to start your work on a Web site by first seeing the page where items can be dragged and dropped, select **Start pages in: Design View**. You make this selection on the **General** node for the **HTML Designer** or by just selecting **HTML Designer** as illustrated in Figure A-11. The other options for the **Start pages in** are **Source View** and **Split View**.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1133_0.png)

**FIGURE A-11** HTML Designer

You determine how much of the screen is used for Design versus Source when you select **Split View**. You can have the majority of your screen show the design of your page with only a few lines revealing HTML if you prefer. As shown in Figure A-11, you can **Split view vertically** or take the default, which places the HTML tags above the design pane.

The **CSS Styling** node for the **HTML Designer**, shown on the left pane in Figure A-11, is used to indicate whether to **Change positioning to absolute** for controls added using Toolbox, paste, or drag and drop. Here you also indicate whether to **Use <strong> and <em>** for bold and italic text.

The **Ruler and Grid** option under the **HTML Designer** node has options for grid size. You can specify the **Ruler and Grid units** of pixels, inches, centimeters, or points. Once that is determined, you can enter measurements for the **Display Grid** and **Snapping Grid** using that unit type. You can also specify the **Line style** and **Line color** from this dialog box.

### Windows Forms Designer

Expanding the **Layout Settings** under the **Windows Forms Designer**, **General** node reveals options for **Width** and **Height** for the Default Grid Cell Size. The **Layout Mode** has value options of **SnapLines** or **SnapToGrid**. You also specify whether to show the grid and/or to snap objects to the grid when they are placed on the form from the **Show Grid** and **Snap To Grid** options. Positioning elements on the form can be made easier if

There are lots of options. Spend some time experimenting with them. Change the settings and go into the editor and see what works best for you.

### Choose Toolbox Items

The Toolbox used with Windows and Web applications can be customized. You can remove items or add additional widgets to the dialog box. When Visual Studio is set up, it installs in the Toolbox the most regularly used controls. If there are controls you hardly use, you can remove them from the list. To remove a control, right-click on the control in the Toolbox and select Delete. Besides the objects currently shown in the Toolbox, other controls are left out but are still available. To add one or more of these left out controls, select Choose Toolbox Items... from the TOOLS menu or right-click anywhere in the Toolbox and click **Choose Items...**. The dialog box shown in Figure A-13 is revealed.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1135_0.png)

**FIGURE A-13** Add Toolbox Items

The Choose Toolbox Items dialog box displays tabbed panes listing components that are installed on your local computer. Select the ones you want to appear in the Toolbox. When you choose OK, any items checked that are not already in the Toolbox will be added, and any items whose checkboxes have been cleared will be removed from the Toolbox.

### Customize the Toolbars

From the **TOOLS, Customize** option you can select which **Toolbars** are displayed in the IDE. Using this option, you not only select the names of the toolbars, but you can also specify which **Commands** are to be included within each toolbar. For example, if you choose to display the **Standard** toolbar, you see icons including **Navigate Backward**, **Navigate Forward**, **New Project**, **Open File**, **Save Selected Items**, **Save All**, **Multi-Level Undo**, and **Multi-Level Redo**. To add icons to a toolbar, from the **Commands** tab select **Add Command**. You can move the icon to the position where you want it to appear. The **Standard** toolbar was customized by adding the **Help** category to the toolbar, as shown in Figure A-14.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1136_0.png)

**FIGURE A-14** Customizing the IDE

You remove icons in the same manner. As shown in Figure A-14, there is also an option to **Delete** commands from toolbars.

After using the **TOOLS, Options** and **TOOLS, Customize** menus, you will want to determine which windows you want open during design. As a minimum you should have available the **Solution Explorer** and **Properties** windows. During Windows and Web development, the **Class View** window and **Toolbox** should be added. For applications involving data connections, the **Data Sources** and **Server Explorer** should be added. Spend some time customizing the workspace to best meet your needs. You will find that it saves you much time during development and makes you more productive.
