
![](img/e33ae760e23d89eac66541252ad65de8_1037_0.png)

Figure A-9   Formatting settings for C# text editing

Selecting **Indent case contents**, **Indent case labels**, and **Indent block contents** causes the indention to occur automatically and can really increase your productivity. You set these settings under the **Indentation** node for **Formatting** under the **Text Editor**. Explore the **Spacing** options under the **Text Editor, C#, Formatting** node. You set spacing for method declarations, method calls, casts, delimiters, and binary operators. You determine whether to have a space inserted between the name and open parenthesis or inside empty square brackets. Some of these settings are shown in Figure A-10.

![](img/e33ae760e23d89eac66541252ad65de8_1038_0.png)

Figure A-10   Space settings for C# text editing

## Debugging

A number of settings can be changed under the **Debugging** folder node. You should review the options that can be set. They include features such as **Ask before deleting all break-points**, **Break all processes when one process breaks**, and **Enable breakpoint filters**.

Select **Enable edit and continue** under the **Edit and Continue** option. This allows you to change your source code while your program is still running, but in break mode. You can edit the code without ending the debug session.

## HTML Designer

Selections made using this node impact your development environment when you are designing Web sites. If you prefer to start your work on a Web site by first seeing the page where items can be dragged and dropped, select **Design View**. You make this selection on the **General** node for the **HTML Designer**. The other option for the **Start Page**, which was used for examples in this book, is **Source View**. The **CSS Styling** node for the **HTML Designer** is used to indicate whether controls should be placed on the page in relative, absolute, or static mode. You may want to select the option of **Change Positioning to absolute for controls added using the Toolbox, paste, or drag and drop**.

The **Ruler** and **Grid** option under the HTML Designer has options for grid size. You can specify the **Ruler** and **Grid** units of pixels, inches, centimeters, or points. Once that is determined, you can enter measurements for the **Display Grid** and **Snap Grid** using that unit type. You can also specify the **Line style** and **Line color** from this dialog box.

## Windows Forms Designer

Expanding the **Layout Settings** reveals options for **Width** and **Height** of the **GridSize**, **LayoutMode**, **ShowGrid**, and **SnapToGrid**. Positioning elements on the form can be made easier if you select **SnapLines** in the **LayoutMode**. Colored lines appear on the form as you move or resize elements. This allows you to snap the element to vertical or horizontal lines so that you can align them consistently. This is illustrated in Figure A–11.

![](img/e33ae760e23d89eac66541252ad65de8_1039_0.png)

**Figure A–11**　Windows Forms Designer

## Other Options Settings

Explore the other options on the **Tools, Options** menu. **Test Tools** and **Office Tools** have a number of interesting settings. You will also want to explore the **Database Tools**. From there you can specify the **SQL Server Instance Name** that you will use for your **Data Connections**. You can indicate which **Panes are shown by default (Diagram, Criteria, SQL, or Results)** with the **Query and View Designer**. You can specify the **Default Query type**. It is initially set to the **Select** query. You can change that to an **Insert, Delete**, or even a **Make Table** query.

There are lots of options. Spend some time experimenting with them. Change the settings and go into the editor and see what works best for you.

## Customize the Toolbars

From the **Tools, Customize** option you can select which toolbars are displayed in the IDE. Using this option, you not only select the names of the toolbars, but you can also specify which **commands** are to be included within each toolbar. For example, if you choose to display the **Standard** toolbar, you see icons including **New Project, Add Item, Open file, Save Selected Items, Cut, Copy, and Paste**. To add icons to a toolbar, from the **Commands** tab select **Add Command**. You can move the icon to the position where you want it to appear. The **Standard** toolbar was customized by adding the **Help** category to the toolbar, as shown in Figure A-12.

![](img/e33ae760e23d89eac66541252ad65de8_1040_0.png)

Figure A-12  Customizing the IDE

You remove icons in the same manner as shown in Figure A-12.

After using the **Tools, Options** and **Tools, Customize** menus, you will want to determine which windows you want open during design. As a minimum you should have available the **Solutions Explorer** and **Properties** windows. During Windows and Web development, the **Class View** window and **Toolbox** should be added. For applications involving data connections, the **Data Sources** and **Server Explorer** should be added. Spend some time customizing the work space to best meet your needs.

## Appendix B

## Code Editor Tools

You will write many types of program statements repeatedly. For example, you write **while**, **do**, **for**, **if**, **switch**, **try...catch...finally**, and **foreach** statements. Every time you use these statements, you type curly braces to show the beginning and end of the block, and you spend time formatting to make sure they are syntactically correct and consistently placed in your program. One of the more exciting new Visual Studio features in the Code Editor automates their inclusion. This is done through using code snippets.

Another time-saving feature is **refactoring**. If you find that you want to take a segment of code and place it in a method, you can do so using a copy-and-paste approach, or you can use the refactoring tools to restructure your source code. The tools automatically promote local variables to parameters and convert blocks of code into a method. Both of these features are discussed in this appendix.

Class diagrams showing the data members, methods, and relationships between classes can be generated automatically with Visual Studio. You can add blank class diagrams and then add members to the structure or have Visual Studio create diagrams from existing code. This appendix also illustrates the use of Class diagrams.

### Code Snippets

**Code snippets** are templates that you can use to insert code. They can help speed up the entry of common code constructs and make you more productive. When you insert a code snippet, a template is inserted into your program that enables you to fill in unique entries. You can use the built-in snippets or create your own. Snippets are stored as XML files that you can edit and customize. Snippets are grouped into the categories of **ASP.NET MVC**, **NetFX30**, **Office Development**, **Other**, **Test**, and **Visual C#**.

The code snippet aliases are included in the list of available entries. Pressing the Tab key twice after selecting the `forr` alias inserts the code snippet text, as shown in Figure B-3.

![](img/e33ae760e23d89eac66541252ad65de8_1044_0.png)

Figure B-3 — Code snippet inserted into text

Notice that the code snippet shown in Figure B-3 inserted the text at the cursor position and created an empty `for` loop. At this point, the editable fields in the code snippet are highlighted and the first editable field is selected automatically. The editable fields for the `for` statement are the initializer variable (i by default) and the length expression (length by default). You can type a new value for the field or press the Tab key to cycle through the editable fields. Clicking on a field places the cursor in the field, and double-clicking on a field selects it. You can change the fields to reflect the identifiers you use in your program.

Code snippets are simply XML files; you can easily create your own. The file ends with a `.snippet` filename extension. As you find yourself typing the same segment of code for multiple applications, you are encouraged to explore the MSDN documentation to learn more about creating your own shortcuts.

## REFACTORING

Refactoring lets you improve on your code by modifying the internal structure without changing the logic or the external behavior of your program. Sometimes methods grow to include more than one major theme. Sometimes you can look at your code and see that a method is doing too much. The **Extract Method** option provides an easy way to create a new method from a segment of code.

## Extract Method

The `Main()` method shown in Figure B-4, both does the calculation and displays the results.
