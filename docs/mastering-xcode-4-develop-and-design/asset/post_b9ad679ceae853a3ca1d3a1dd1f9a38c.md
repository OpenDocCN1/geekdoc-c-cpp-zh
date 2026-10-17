
## CREATING A TEST PROJECT

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_26_0.png)

Let’s create a test project with which to explore. To do this, choose the Application category under the Mac OS X section and then click the Cocoa Application template. Click Next to continue. Xcode will respond by asking you for some additional information to customize your project, as shown in **Figure 2.3**.

The Product Name field is where you would put your application’s name in most cases. Let’s call our product TestApp in the interest of clarity. This not only determines the name of your project file and its enclosing folder but the name of your built product (your application, plug-in, library, and so on).

The Company Identifier field is just as important as your product name. This identifier is used to create your bundle identifier. The bundle identifier, in turn, can be used as a unique identifier for your application’s preferences file, its document files, its associated Spotlight importer, and many other things. Apple encourages developers to use a reverse-ordered ICANN domain name. Assuming your domain is *yourcompany.com*, your company identifier would be *com.yourcompany*. Xcode fills in your app’s name (substituting illegal characters as needed) to form your project’s bundle identifier (displayed below the Company Identifier field).

Although only the Product Name field is required, you should always provide a suitable company identifier. The identifier doesn’t necessarily have to correspond to an existing domain, but it should be unique.

The App Store Category pop-up lets you select a general category under which your application would fall if you choose to deploy to the Mac App Store. Since you won’t be submitting TestApp to the App Store, you can leave that set to None, its default.

The next three options (Create Document-Based Application, Document Class, and Document Extension) let you use a document-based application template. A plain Cocoa application (Create Document-Based Application deselected) is intended for applications that do not work with individual files as documents; a document-based Cocoa application uses the Cocoa document architecture to open and manipulate document files. For simplicity, TestApp will not be document-based, so leave that option deselected.

The Use Core Data option adds support for Cocoa’s object graph management and persistence framework, called Core Data. Select this option so you can explore the Data Model Editor in Chapter 10.

The Include Unit Tests option will add support for unit tests to your project. Select this option to include unit tests, which you’ll explore in Chapter 18.

The Include Spotlight Importer option adds a Spotlight importer plug-in as a dependent build target to your project’s application target. When you add the necessary code, Spotlight—the Mac OS X search facility—will use the importer to add the data you provide to its search index automatically. Leave this deselected, and leave Spotlight importer plug-in programming for another book.

Different project and option choices can cause different fields to appear when creating a new project. Consult the Xcode documentation (covered in Chapter 4) for further details about these options.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_28_0.png)

Once you’ve filled in the requested information, click Next to continue. Xcode will present a Save As dialog box. Select the option to create a local Git repository for this project. You’ll explore Xcode’s Git (and Subversion) support in Chapter 21. Choose a convenient location (such as your desktop), and click Save. You should now have a basic Xcode project ready to go, as shown in **Figure 2.4**.

## PROJECT MODERNIZATION

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_29_0.png)

**Figure 2.5** Warnings of outdated project settings

For those who weren’t born (as Mac or iOS developers) yesterday, Xcode introduces the concept of “project modernization.” As much fun as it is to create brand new projects full of new possibilities, many of us have existing projects that were created in earlier versions of Xcode.

These preexisting projects often contain settings that are not compatible with modern versions of Xcode. Fortunately, Xcode not only finds these problems but offers to fix them as well. It even lets you pick the fixes to apply, since its idea of “fixing” may not necessarily agree with yours.

### MODERNIZING A PROJECT

When opening projects that were created with previous versions of Xcode, you might notice some warnings appear in the Issue navigator (**Figure 2.5**), informing you of issues that need cleaning up.

> **NOTES:** Project modernization was introduced in Xcode version 4.1 and is not available in 4.0.
>
> The Issue navigator is explored in Chapter 3.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_29_1.png)

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_30_0.png)

Selecting the issue (or choosing Editor > Check for Outdated Settings from the main menu) will display a Build Settings sheet (**Figure 2.6**) summarizing the changes that Xcode thinks you should make. Deselect the check box to the left of any settings you think Xcode ought to ignore.

To perform the selected changes, click Perform Changes. To cancel without performing any changes, click Cancel. To ignore the selected issues, select Don’t Perform Changes. The separate Perform Changes and Don’t Perform Changes buttons let you accept some updates and then come back and instruct Xcode to ignore others.

Remember that you can always check for outdated settings at any time by choosing Editor > Check for Outdated Settings from the main menu.

## BUILDING AND RUNNING AN APPLICATION

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_31_0.png)

**Figure 2.7** The new Cocoa application

At this point you have a fully functional—if uninteresting—Cocoa application project that is ready to be built and run. To see your application, click the Run button in the project window toolbar (or choose Product > Run “TestApp” from the main menu). Xcode will build the project from scratch (because this is the first time it’s been built) and then launch it. After a short time, you’ll see your application’s empty window (**Figure 2.7**). It’s not particularly exciting at the moment, but it is a functioning application at this point, even without customization.

The Run button doesn’t just trigger a build and run. You can click and hold the button to reveal a menu of other actions similar to those found under the Product menu. These actions include Test, Profile, and Analyze. Each of these will build the project automatically if it needs building before performing the requested action. These other actions are covered in later chapters.

## WRAPPING UP

TestApp isn’t very interesting in its current state, but it is a fully functional application with a main menu, a window, and even an About panel. You now know how to create, build, and run a basic template application. In the next chapter, you’ll explore Xcode’s user interface using the project you just created.

In the previous chapter, you created a Cocoa application project called TestApp. In this chapter, you’ll explore the anatomy of this project and familiarize yourself with Xcode’s user interface.

Earlier versions of Xcode allowed users to select a multiple-window interface, but the default was single-window (where most views related to the open project were contained within the same window). Single-window mode wasn’t quite single-window mode, however; a number of auxiliary windows could appear. In Xcode 4, Apple has taken the all-in-one-window design approach much further.

If it’s not open already, open the TestApp project you created in Chapter 2.

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_33_0.png)

## THE WORKSPACE WINDOW

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_34_0.png)

**Figure 3.1** The workspace window

An Xcode project consists of a collection of source files (such as Objective-C files, Interface Builder nibs, and Core Data managed object models), resources (such as images and rich text files), and the Xcode project file, in which the various settings and build rules are maintained. It is helpful to think of an Xcode project as a collection of sources and resources with a project file to bind them together. Xcode 4 goes a step further and allows you to combine multiple related projects into a single *workspace* (see *Chapter 16*). The main window for a given project or workspace is called the *workspace window* (**Figure 3.1**).

The workspace window is divided into multiple areas, which you’ll examine in detail in this chapter. Almost everything related to your workspace is contained within these areas, whose responsibilities include organization, navigation, editing, inspection, and debugging.
