In this chapter, we’ll use Interface Builder and off-the-shelf components to build our browser. We’ll pick a couple of buttons, a text field, and a special component for displaying web pages from a library. We’ll drag these components onto our window, arrange them the way we want them to look, and make sure they visually behave right when we shrink or stretch the window. We’ll then use Interface Builder to enable the behavior we want. Once we get everything working the best we can for now, we’ll take a quick look behind the scenes at some of the backstage magic.

# 2.1 Creating Your Project in Xcode

As we bounce back and forth between IB¹ and Xcode in these first few chapters, you’ll get a feel for what each is for. Mostly, you’ll use Xcode as an IDE to work on your code, your data model, and your project. The work you do in Xcode will feel familiar to you if you use other IDEs.

As you might expect, you’ll create your GUI using Interface Builder. You’ll also use Interface Builder to connect the elements of the GUI to data sources, to other GUI elements, and to methods described in code. You’re going to spend almost all of your time in this first example using Interface Builder.

Even though you won’t write any code for this SimpleBrowser example, you’ll need to create the project from Xcode. Start Xcode, and create a new project using either ⌘ N or File > New Project.²

You’ll be presented with a variety of options for project templates that you can use to develop applications for the iPhone or for Mac OS X. Choose Mac OS X > Application > Cocoa Application. Leave the checkboxes unselected for creating a document-based app or for using Core Data. Click the Choose button or just press ↵.

I have saved the project as SimpleBrowser in ~/Dev/UsingWhatsThere/. You can choose another name or location if you prefer.

+   1. This is short for Interface Builder and is pronounced “I.B.” but written IB.
+   2. You’ll find Xcode in the /Developer/Applications directory. You will use it enough that you should drag it to the Dock to create a shortcut. Also, remember you can always use Spotlight by clicking the magnifying glass in the far right of the menu bar.