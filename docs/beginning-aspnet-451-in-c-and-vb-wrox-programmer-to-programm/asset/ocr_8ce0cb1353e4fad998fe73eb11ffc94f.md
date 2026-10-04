# CHAPTER 5 PROGRAMMING YOUR ASP.NET WEB PAGES

Add the App_Code folder to your site, right-click the site's name in the Solution Explorer and choose Add ASP:NET Folder App_Code. Figure 5-4 shows the new folder.

With the App_Code folder in place, you can start adding class files to it. Class files have an extension that matches the programming language you have chosen for the site: .cs for C# or .vb for files containing VB.NET code. Inside these class files you can create classes that contain them methods (functions and subroutines) that are discussed in more detail in the final section of this chapter; for now, focus on the methods in the code and how they are called, rather than on why you need to add the code to a class first.

The next exercise shows you how to use the App_Code folder to optimize the calculator you created in an earlier Try It Out.

![](bbox=[0.638, 0.107, 0.862, 0.363])

FIGURE 5-4

# TRY OUT Optimizing the Calculator

In this exercise, you create a class that exposes four methods: Add, Subtract, Multiply, and Divide. When the class is set up and is capable of performing the necessary computing actions, you modify your CalculatorDemo.aspx file so it uses your new Calculator class. Although this is a trivial example it shows the amount of code you need to write and the added flexibility you gain by moving your code from the ASPX page to the App_Code folder so it can be reused by other applications, it is comprehensive enough to show you the concept, yet short enough to enable you to understand the code. For now, just focus on how the calculator works and how to call its methods. In the section on object orientation later in this chapter, you see exactly what a class is.

+   1. If you haven't done so, start by adding an App_Code folder to your site by right-clicking the site and choosing Add+ ASP:NET Folder App_Code.

+   2. Right-click this newly created folder and choose Add+ New Item. In the dialog box that follows, select the appropriate programming language, and click Class. Instead of adding Add+ New Item you can also choose Add+ Class, which serves as a shortcut for adding a class file. This shortcut also means list items that you have recently added to the list.

+   3. Type Calculator as the name of the file and click Add (or OK if you use the shortcut method). This creates a class file that in contains a class called Calculator. Note that it's common practice to name classes using Pascal casing, where each word starts with a capital letter.

+   4. Right after the line of code that defines the Calculator class, add the following methods, replacing any code that was already present in the class:

VB.NET

Public Class Calculator

```
Public Function Add(a As Double, b As Double) As Double
Return a + b
```