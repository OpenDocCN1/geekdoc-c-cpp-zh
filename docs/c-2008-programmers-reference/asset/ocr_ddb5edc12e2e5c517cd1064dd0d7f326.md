# Chapter 15: Assemblies and Versioning

![](bbox=[0.35, 0.12, 0.68, 0.42])

Figure 15-6

The MathUtil.dll assembly will now be added to the project. Observe that the Copy Local property for the MathUtil.dll assembly is set to True (see Figure 15-7). This means that a copy of the assembly will be placed in the project’s output directory (that is, the bin\Debug folder).

![](bbox=[0.3, 0.64, 0.78, 0.86])

Figure 15-7

> When you add a reference to one of the classes in the .NET class library, the Copy Local property for the added assembly will be set to False. That's because the .NET assembly is in the Global Assembly Cache (GAC), and all computers with the .NET Framework installed have the GAC. The GAC is discussed later in this chapter.