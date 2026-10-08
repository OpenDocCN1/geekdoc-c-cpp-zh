
# Chapter 2 Introduction to Visual Studio and Visual Programming

tions for the property. Click the ellipsis button to display the Font dialog (Fig. 2.27).

![](img/57baed2319be0bb1b5f98674846f2711_92_0.png)

Fig. 2.26 | Properties window displaying the Label1's property.

![](img/57baed2319be0bb1b5f98674846f2711_92_1.png)

Fig. 2.27 | Font dialog for selecting fonts, styles and sizes.

- 2. You can select the font name (the options may be different, depending on your system), font style (Regular, Italic, Bold, etc.) and font size (16, 18, 20, etc.) in this dialog. The Sample text shows the selected settings. Under Font, select Segoe UI, Microsoft's renowned for user interfaces. In Size, select 24 points and click OK.
- 3. If the Label's text does not fit on a single line, it wraps to the next line. Resize the Label so that the text "Welcome to" appear on the Label's first line and the text "C Programming!" appear on the second line.
- 4. Re-center the Label horizontally.

**Step 9: Aligning the Label's Text**

Select the Label's TextAlign property, which determines how the text is aligned within the Label. A three-by-three grid of buttons representing alignment choices is displayed (Fig. 2.28). The position of each button corresponds to where the text appears in the Label. For this app, set the TextAlign property to MiddleCenter in the three-by-three grid—this selection centers the text horizontally and vertically within the Label. The TextAlign values, such as TopLeft, TopRight, and BottomCenter, can be used to position the text anywhere within a Label. Certain alignment values may require that you resize the Label to fit the text better.

| Properties | | |
|---|---|---|
| label1 System.Windows.Forms.Label | alignment options |
| | TopLeft | |
| | UseMnemonic | |
| UseWaitCursor | Middle-center alignment option |
| Behavior | | |
| AllowDrop | | |
| AutoEllipse | | |
| | Determines the position of the text within the label. | |

**Fig. 2.28** | Centering the Label's text.

**Step 10: Adding a PictureBox to the Form** The PictureBox control displays images. Locate the PictureBox in the Toolbox (Fig. 2.15) and double click to add it to the Form—each PictureBox you add to the Form is an object of class PictureBox from the .NET Framework Class Library. When the PictureBox appears, move it underneath the Label, either by dragging it or by using the arrow keys (Fig. 2.29).

![](img/57baed2319be0bb1b5f98674846f2711_93_0.png)

**Fig. 2.29** | Inserting and aligning a PictureBox.

**Step 11: Inserting an Image** Click the PictureBox to display its properties in the Properties window (Fig. 2.30), then:

- 1. Locate and select the Image property, which displays a preview of the selected image or (none) if no image is selected.
- 2. Click the ellipsis button to display the Select Resource dialog (Fig. 2.31), which is used to import files, such as images, for use in an app.

![](img/57baed2319be0bb1b5f98674846f2711_94_0.png)

**Fig. 2.30 | Image property of the PictureBox.**

![](img/57baed2319be0bb1b5f98674846f2711_94_1.png)

**Fig. 2.31 | Select Resource dialog to select an image for the PictureBox.**

- 3. Click the Import... button to browse for an image, select the image file and click OK to add it to your project. We used .png from this chapter's examples. Supported image formats include PNG (Portable Network Graphics), GIF (Graphic Interchange Format), JPEG (Joint Photographic Experts Group) and BMP (Windows). Depending on image's size, it's possible that only a portion of the image will be previewed in the Select Resource dialog—you can resize the dialog to see more of the image (Fig. 2.32). Click OK to use the image.
- 4. To scale the image to fit in the PictureBox, change the SizeMode property to StretchImage (Fig. 2.33). Resize the PictureBox, making it larger (Fig. 2.34), then re-center the PictureBox horizontally.

**Step 12: Saving the Project**
Select File > Save All to save the entire solution. The solution file (which has the extension .sln) contains the name and location of your project, the project file (which has the extension .csproj) contains the names and locations of all the files in the project. If you want to reopen your project at a later time, simply opens its .sln file.

![](img/57baed2319be0bb1b5f98674846f2711_95_0.png)

Fig. 2.32 | Select Resource dialog displaying a preview of selected image.

| Properties | | | |
|---|---|---|---|
| pictureBox1 | System.Windows.Forms.PictureBox | | |
| Enabled | True | | |
| SizeMode | StretchImage | | |
| Visible | True | | |
| SizeMode | | Controls how the PictureBox will handle image placement and control sizing. | |

Fig. 2.33 | Scaling an image to the size of the PictureBox.

![](img/57baed2319be0bb1b5f98674846f2711_95_1.png)

Fig. 2.34 | PictureBox displaying an image.

Step 13: Running the Project
Recall that to this point we have been working in the IDE design mode (that is, the app being created is not executing). in run mode, the app is executing, and you can interact with only a few IDE—features that are not available (gray out). Select Debug > Starting Debugging to execute the app (or press the F5 key). The IDE enters run mode and displays “Running” next to the app's name in the IDE's title bar.
Figure 2.35 shows the running app, which appears in its own window outside the IDE.

![](img/57baed2319be0bb1b5f98674846f2711_96_0.png)

Fig. 2.35 | IDE in run mode, with the running app in the foreground.

Step 14: Terminating the App
You can terminate the app by clicking its close box X in the top-right corner of the running app's window. This action stops the app's execution and returns the IDE to design mode. You can also select Debug > Stop Debugging to terminate the app.

## 2.7 Wrap-Up

In this chapter, we introduced key features of the Visual Studio IDE. You visually designed a working C# app without writing any code. C# app development is a mixture of two styles—visual app development allows you to develop GUIs easily and avoid tedious GUI programming and “conventional” programming (which we introduce in Chapter 3) allows you to specify the behavior of your apps.

You created a C# Windows Forms app with one Form. You worked with the IDE's Solution Explorer, Toolbox and Properties windows, which are essential to developing C# apps. We also demonstrated context-sensitive help, which displays topics related to controls or text.
You used visual development to design your C# app by adding a Label and a Picture onto a Form. You used the Properties window to set a Form's Text and BackColor properties. You learned that controls display text and that PictureBoxes display images. You displayed text in a Label and added an image to a PictureBox. You also worked with the Label's AutoSize, TextAlign and Font properties and the Picture's Image and SizeMode properties.

## 2.8 Web Resources

In the next chapter, we discuss "nonvisual," or "conventional," programming—you'll create your apps with C# code that you write, instead of having Visual Studio the You'll learn memory concepts and write code that displays information on the screen, receives inputs from the user, performs arithmetic operations and makes decisions.

### 2.8 Web Resources

Please take a moment to visit each of these sites.
- https://www.visualstudio.com/ - The home page for Visual Studio. The site includes news, downloads and other resources.
- https://social.msn.microsoft.com/Forums/en-US/home?forum=cshareneral - This site provides access to the Microsoft C# forums, which you can use to get your C# language and IDE questions answered.
- https://msn.microsoft.com/magazine/default.aspx - This is the Microsoft Developer Network Magazine site. This site provides articles and code on many C# and .NET development. There is also an archive of past issues.
- http://stackoverflow.com/ - In addition to the Microsoft forums, StackOverflow is an excellent site for getting your programming questions answered.

Summary

2.1 Introduction
Visual Studio is Microsoft's Integrated Development Environment (IDE) for creating, running and debugging apps written in a variety of .NET programming languages. Creating apps by dragging and dropping predefined building blocks into place is called visual app development.

2.2 Overview of the Visual Studio Community 2015 IDE
The Start Page contains links to Visual Studio IDE resources and web-based resources.
A project is a group of related files that compose a app. Visual Studio organizes apps into projects and solutions. A solution may contain one or more projects.
Dialogs are windows that facilitate user-computer communication.
Visual Studio provides templates for the project you can create.
A Form represents the main window of the Windows Forms app that you're creating.
Collectively, the Form and controls constitute the app's graphical user interface (GUI), which is the visual part of the app with which the user interacts.

2.3 Menu Bar and Toolbar
Commands for managing the IDE and for developing, maintaining and executing apps are contained in the menus, which are located on the menu bar.
