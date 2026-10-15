
## Customizing the Text Editor

In addition to being able to customize the overall environment provided by Visual Studio, you can customize several specific elements related to your development environment. More so than in any previous version, the capability to modify the environment has been enhanced. With Visual Studio 2010, the user interface components have been rewritten using WPF so that the entire display provides a much more graphical environment and better designer support.

Both Visual Studio 2010 and Visual Basic 2010 Express Edition have a rich set of customizations related to a variety of different environment and developer settings. Admittedly, Visual Studio 2010’s feature set offers a larger number of options for editing, but rest assured that the Express Edition contains many more options for editing than most people expect. For example, common to both IDEs is a text editor that allows for customization. If you’ve ever had to show code to an audience — for example, in a group code review — the capability to adjust things such as font size and other similar options is great.

To leverage Visual Studio’s settings, select Tools Options to open the Options dialog, shown in Figure 1-16. Within the dialog, make sure the Show all settings check box is selected. Next, select the Text Editor folder, and then the All Languages folder. This section enables you to make changes to the text editor that are applied across every supported development language. Additionally, you can select the Basic folder to make changes that are specific to how the text editor behaves when you edit VB source code.

![](img/d99870e80390742f93963da7be0b2e61_53_0.png)

FIGURE 1-16

From this dialog, it is possible to modify the number of spaces that each tab will insert into your source code and to manage several other elements of your editing environment. Within this dialog you see settings that are common for all text editing environments, as well as the ability to customize specific settings for specific languages. For example the section specific to Visual Basic includes settings that allow for word wrapping and line numbers. One little-known but useful capability of the text editor is line numbering. Checking the Line numbers check box will cause the editor to number all lines, which provides an easy way to unambiguously reference lines of code.

Visual Studio also provides a visual indicator so you can track your changes as you edit. Enabling the Track changes setting under the Text Editor options causes Visual Studio to provide a colored indicator in places where you have modified a file. This indicator appears as a colored bar at the left margin of your display. It shows which portions of a source file have been recently edited and whether those changes have been saved to disk.

## IntelliSense, Code Expansion, and Code Snippets

One of the reasons why Microsoft Visual Studio is such a popular development environment is because it was designed to support developer productivity. That sounds really good, but let’s back it up. People who are unfamiliar with Visual Studio might just assume that “productivity” refers to organizing and starting projects. Certainly, as shown by the project templates and project settings discussed so far, this is true, but those features don’t speed your development after you’ve created the project.

This section covers three features that target your productivity while writing code. They are of differing value and are specific to Visual Studio. The first, IntelliSense, has always been a popular feature of Microsoft tools and applications. The second feature, code expansion, is another popular feature available since Visual Studio 2005: It enables you to type a keyword, such as “select,” and then press the Tab key to automatically insert a generic select-case code block, which you can then customize. Finally, going beyond this, you can use the right mouse button and insert a code snippet at the location of your mouse click. As you can tell, each of these builds on the developer productivity capabilities of Visual Studio.

### IntelliSense

IntelliSense has been enhanced in Visual Studio 2010. Early versions of IntelliSense required you to first identify a class or property in order to make uses of the IntelliSense feature. Beginning with Visual Studio 2008, IntelliSense is activated with the first letter you type, so you can quickly identify classes, commands, and keywords that you need. This capability continues with Visual Studio 2010, but the IDE team worked hard to enhance IntelliSense performance so that it won’t sometimes feel like the IDE is trying to keep up with your typing.

Once you’ve selected a class or keyword, IntelliSense continues, enabling you to not only work with the methods of a class, but also automatically display the list of possible values associated with an enumerated list of properties when one has been defined. IntelliSense also provides a ToolTip-like list of parameter definitions when you are making a method call.

Figure 1-17 illustrates how IntelliSense becomes available with the first character you type. Note that the drop-down window has two tabs on the bottom; one is optimized for the items that you are likely to want, while the other shows you everything that is available. In addition, IntelliSense works with multiword commands. For example, if you type Exit and a space, IntelliSense displays a drop-down list of keywords that could follow Exit. Other keywords that offer drop-down lists to present available options include Goto, Implements, Option, and Declare. In most cases, IntelliSense displays more ToolTip information in the environment than in past versions of Visual Studio, and helps developers match up pairs of parentheses, braces, and brackets.

![](img/d99870e80390742f93963da7be0b2e61_54_0.png)

FIGURE 1-17

Finally, note that IntelliSense is based on your editing context. While editing a file, you may reach a point where you are looking for a specific item to show up in IntelliSense but when you repeatedly type slightly different versions, nothing appears. IntelliSense recognizes that you aren’t in a method or you are outside of the scope of a class, so it removes items that are inappropriate for the current location in your source code from the list of items available from IntelliSense.

### Code Expansion

Going beyond IntelliSense is code expansion. Code expansion recognizes that certain keywords are consistently associated with other lines of code. At the most basic level, this occurs when you declare a new Function or Sub: Visual Studio automatically inserts the End Sub or End Function line once you press Enter. Essentially, Visual Studio is expanding the declaration line to include its matching endpoint.

However, true code expansion goes further than this. With true code expansion, you can type a keyword such as For, ForEach, Select, or any of a number of Visual Basic keywords. If you then use the Tab key, Visual Studio will attempt to recognize that keyword and insert the block of code that you would otherwise need to remember and type yourself. For example, instead of needing to remember how to format the control values of a Select statement, you can just type this first part of the command and then press Tab to get the following code block:

```
Select Case VariableName
  Case 1
  Case 2
  Case Else
End Select
```

Unfortunately, this is a case where just showing you the code isn’t enough. That’s because the code that is inserted has active regions within it that represent key items you will customize. Thus, Figure 1-18 provides a better representation of what is inserted when you expand the Select keyword into a full Select Case statement.

![](img/d99870e80390742f93963da7be0b2e61_55_0.png)

FIGURE 1-18

When the block is inserted, the editor automatically positions your cursor in the first highlighted block — VariableName. When you start typing the name of the variable that applies, the editor automatically clears that
