# # Chapter 10: Can I Use Your Namespace in the Library?

In This Chapter

+   - Dealing with separately compiled assemblies

+   - Writing a class library

+   - More access-control keywords: protected, internal, protected internal

+   - Working with namespaces

> > # gives you a variety of ways to break code into meaningful, workable units.

You can use a *method* to divide a long string of code into separate, maintainable units. Use the *class structure* to group data and methods in meaningful ways to further reduce the complexity of the program. Programs are complex already, and we simple humans become confused easily, so we need all the help we can get.

C# provides another level of grouping: You can group classes into a separate library. Beyond writing your own libraries, you can use anybody's libraries in your programs. These programs contain multiple modules as *namespaces*. I describe libraries and assemblies in this chapter.

Meanwhile, the access-control story in Chapter 5 of this minib leaves a few loose ends — the protected, internal, and internal keywords is slightly complicated further by the use of namespaces, another way to group similar classes and allow the use of duplicate names in two parts of a program. I cover namespaces in this chapter as well.

The program examples mentioned in this chapter are part of the chapter download. You can also download them separately on the Example Code page of the Web site at csharp102.info or csharpforddummies.net.

![](bbox=[0.128, 0.763, 0.203, 0.832])