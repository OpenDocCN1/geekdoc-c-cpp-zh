+   When writing functions or subroutines, try to minimize the number of lines of code. Usually, with more than 40 or 50 lines of code are a sign of bad design. When you see code, consider the option to move certain parts to their own routine. This makes your code easier to understand, leading to better code with fewer bugs. Even if a method is used only once, keeping a chunk of code in a separate method can significantly increase the readability and organization of your code.

+   When writing comments in your code, try to describe the general purpose of the code instead of explaining obvious statements. For example, this comment (seen many times in real) is completely useless and only adds noise:
```vb
Dim loopCount As Integer = 0 ' Declare loopCount and initialize it to zero
```
Anyone with just a bit of coding experience can see what this code does.

# SUMMARY

Although programming can get really complex, the basic basics that you need to understand are relatively easy to grasp. The fun thing about programming is that you don't have to be an expert to make useful programs. You can start with a simple Hello World example and work from there, each time expanding your view on code a little.

This chapter covered two main topics. First, you got an introduction to programming in .NET using either C# or VB.NET. You saw what data types and variables are and learned about operators, decision making, and loops. You also saw how to write organized code using functions, subs, and namespaces and how to add comments to your code.

The final section of this chapter dealt with object orientation. Though object orientation in itself is a very large subject, the basics are easy to pick up. In this chapter you learned the basic elements of OO programming: classes, methods, properties, and constructors. You also learned a bit about inheritance, the driving force behind object-oriented design.

In the next chapter, which deals with creating consistent-looking web pages, you see inheritance when you create a BasePage class that serves as the parent for the Code Behind classes in the Planet Wrox project.

# EXERCISES

+   1. Considering the fact that the oldest person in the world lived to be 122, what's the best numeric data type to store a person's age? Bonus points if you come up with an even better alternative to store someone's age.

+   2. What does the following code do?

VB.NET
```vb
DeleteButton.Visible = Not DeleteButton.Visible
```

#
```csharp
DeleteButton.Visible = !DeleteButton.Visible;
```