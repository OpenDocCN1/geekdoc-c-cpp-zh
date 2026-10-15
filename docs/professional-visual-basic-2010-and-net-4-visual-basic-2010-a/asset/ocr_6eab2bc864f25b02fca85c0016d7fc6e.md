# 28

# COM-Interop

# WHAT YOU WILL LEARN IN THIS CHAPTER

+   > Review of COM
+   > Calling COM from .NET
+   > Interop with ActiveX controls
+   > Configuring .NET assemblies to be called from COM
+   > Introduction to P/Invoke

A vast body of technology surrounds Microsoft’s Component Object Model (COM). Over the years, this model has been the cornerstone of so much Microsoft-related development that we have to take a long, hard look at how to integrate all that technology into the world of .NET.

This chapter begins by taking a brief backward glance at COM, and then compares it with the way that components interact in .NET. It also takes a look at the tools Microsoft provides to help link the two together. Having looked at the theory, you then try it out by building a few example applications. First you take a legacy basic COM object and run it from a Visual Basic 2010 program. Then you repeat the trick with a full-blown ActiveX control. Next, you run some Visual Basic code in the guise of a COM object. Finally, this chapter takes a look at some tools associated with going below the COM layer and into the P/Invoke layer of the operating system.

> The COM-related examples in this chapter are exclusive to a 32-bit environment. Attempting to run these examples on a 64-bit environment will result in runtime errors unless you reset the project settings to specifically target a 32-bit (x86) operating system.

When considering the differences between COM and .NET, keep in mind one thing: COM is, to a large extent, where .NET came from. In addition, with all the time and resources that have been invested in this technology, it is important to consider the best ways to both maintain these investments and integrate them into new investments you make, and over time migrate your components to .NET-based implementations for the transition to 64-bit computing.