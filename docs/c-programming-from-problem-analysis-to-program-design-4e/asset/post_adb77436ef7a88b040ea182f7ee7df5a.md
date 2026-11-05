
- 8. Create a Web site that retrieves and displays the current department chairs from a database. The StudentDataBase.accdb Access database used with examples in this book includes a major table that stores the major id, major name, department chair, and the department phone number. Create a Web site that references this table, or a database table that you create with similar fields. Display on the Web site the name of the major and the chair for the department. Enhance the site by changing background and foreground colors of the page and the grid storing the data.
- 9. Create a smart device currency converter application. Select two markets, such as U.S. dollar and the Euro. Research the current equivalents and use those values for your calculations. Include an image control and a control that enables the user to input a value. Display the formatted value entered along with its converted counterpart and the exchange rate.
- 10. Create a smart device application that allows users to input their names, year of birth, and student IDs. Create and display a new security hash value. The new value should consist of the first initial of their names followed by the identification number and the last two digits of their birth year. Append onto the end of those values the total number of characters in their names. For example, if the name Sofya ElKomaria, birth year 1994, and the ID 12467 is entered, the new identification number would be S124679416. Create an attractive screen with an image control in the background.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1122_0.png)

## APPENDIX A

## VISUAL STUDIO CONFIGURATION

Header Sculand / Shutterstock.com

### Customizing the Development Environment

When Visual Studio is launched, it opens the current default **Start Page**. As shown in Figure A-1, you have options of **New Project…** or **Open Project…** from the **Start Page**. Also included on this page are **Get Started** and **Latest News** tabs. From the **Get Started** tab, in the center pane, you will find a number of selections providing Guidance and resources. If you have an Internet connection, you can subscribe to an RSS feed that provides the latest updates and information about Visual Studio and C# from the **Latest News** tab.

You can choose to have this page opened each time you run Visual Studio or, as illustrated in the figure, you can deselect the checkbox in the extreme left corner and not **Show page on startup**. You can begin customizing your environment even at that point. You can also check the **Close page after project load** if you do not want to see the **Start Page** listed as one of the available tabs while you are working on your project.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1123_0.png)

**FIGURE A-1** Visual Studio Start Page

You have an option to pin an important project right on the Start Page so it will always be there. The pushpin is revealed when you move your mouse over the project in the Recent projects area. The FileAccessApp and PresentationGUI are pinned in Figure A-1. Ten projects are shown under the Recent projects area on the left pane in the figure. This number can be changed as described below.

You use the **Options** from the **TOOLS** menu as shown in Figure A-2 to make the most useful changes.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1124_0.png)

**FIGURE A-2** Using TOOLS, Options to configure Visual Studio

> **NOTE**
> 
> Depending on how the system you are using is configured, the options on your menu may vary slightly from the one displayed in Figure A-2.

### Environment

After you select **Options**, the first folder node shown is **Environment**. When you select **Environment**, the right pane of the dialog box changes to reveal options as shown in Figure A-3.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1125_0.png)

**FIGURE A-3** Environment General options

As shown in Figure A-3, the **Environment** node enables you to select either a **Light** or **Dark Color theme**. You can also indicate how many items should display under the **WINDOW** menu option. You can specify from 1 to 24. The default is **10**. If you have more files open than the number you select, older filenames just fall off the list, which is also the case for the second option under the **Recent** area. The default for **items shown in recently used lists** is also 10. This value impacts the **FILE** menu option and also the Start Page list. Using the **Recent Files** or **Recent Projects and Solutions** option from the **FILE** menu saves time when you are working with the same project over a long period. It eliminates the need to browse to the same location where the project is stored every time you want to reopen the file. Pinning the project to the list, as was described above, is also useful if you have a project that gets worked on often to keep it from falling off the list.

When you select the **Environment** node from the **Options** dialog box, the **General** tab options are displayed. From the **Environment, General** node dialog box, you also specify whether the status bar is displayed and indicate whether the **Close button impacts the active window only**. These options are all available when **General** is revealed or by selecting the **Environment** node.

From the **Environment, Fonts and Colors** node, you can change the size and type of the font for almost every item that appears in Visual Studio, including dialog boxes, windows, and text editor's text. It is useful to increase the font size if you are performing paired programming (working as a team of two) at a computer station or if you want to project your source code to a screen for others to view. As shown in Figure A-4, you have the capability of changing the display item's background or foreground.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1126_0.png)

**FIGURE A-4** Setting the fonts and colors

If you review the list of items available to change in the dropdown list of the Display Items control shown on the center pane in Figure A-4, you will find there are over 100 items listed just for the Text Editor.

The Environment, Startup node, shown on the left pane in Figure A-4, lets you determine what is opened when you first start Visual Studio. You can select options such as Show Start Page, Open Home Page, Load last loaded solution, Show Open Project dialog box, Show New Project dialog box, or Show empty environment. You might also want to make changes at the Environment, Web Browser node, where the URL for your Home page and Search page are set.

Probably best to store all templates in a common location. From the **Projects and Solutions** dialog box, you also indicate whether you want to **Always show Error List if build finishes with errors** or to **Show Output window when build starts**.

If you are working off a network drive, you may want to deselect the option **Warn user when the project location is not trusted**. Otherwise you may get an annoying dialog message every time you test your applications indicating the location is not trusted.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1128_0.png)

**FIGURE A-6** Setting the location for Visual Studio projects

You should definitely configure the Visual Studio **Projects location** setting as shown in Figure A-6. You are encouraged to review and explore the other settings available on the **Environment** and **Projects and Solutions** tabs.

### Text Editor

If you do not like the autocompletion IntelliSense feature of Visual Studio, you can turn features on/off under the **Text Editor**, **C#**, **IntelliSense** option as shown in Figure A-7 or adjust the features to fit your preferences.

![](img/36e48639a06772bcb0fa1ea2525b33a3_1129_0.png)

**FIGURE A-7** Text Editor IntelliSense settings for C#

On the **C# IntelliSense** dialog box, shown in Figure A-7, notice that the second major checkbox option is **Commit by pressing the space bar**. Turning on this feature reduces the number of keystrokes required while you are programming as does turning on the selection from the first checkbox, **Show completion list after a character is typed**.

> **NOTE**
> 
> IntelliSense comes in two modes: Completion and Suggestion. By default you get Completion mode. Completion mode can be annoying if you try to type the name of something that doesn’t exist. IntelliSense tries to help and pops up only available or valid options. Often you will accidentally get items added you didn't want. You can press **CTRL+ALT+SPACEBAR** to switch to IntelliSense Suggestion mode (as opposed to Completion mode). In suggestion mode, IntelliSense is less aggressive. It does not autocomplete member names after you type open parenthesis or equal symbols. Instead, you are able to choose an existing member from a list.

You can set the editor to display **Line numbers**, **Enable single-click URL navigation**, and display the **Navigation bar** from the **Text Editor, C#, General** mode as shown in Figure A-8.
