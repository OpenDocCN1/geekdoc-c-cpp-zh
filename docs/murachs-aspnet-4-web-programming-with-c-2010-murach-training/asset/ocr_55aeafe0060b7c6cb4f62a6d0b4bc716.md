# Perspective

The purpose of this chapter has been to get you started with the development of multi-page web applications. Now, if this chapter has worked, you should be able to develop simple multi-page applications of your own. Yes, there’s a lot more to learn, but you should be off to a good start.

Frankly, though, much of the C# code in the Shopping Cart application is difficult, even in a simple application like this one. So if your experience with C# is limited, you may have trouble understanding some of the code. And you may have trouble writing the same type of code for your new applications.

If that’s the case, we recommend that you get our latest C# book. It will quickly get you up to speed with the C# language. It will show you how to use dozens of the .NET classes, like the List<T> class. It will show you how to develop object-oriented Windows applications. It is a terrific on-the-job reference. And it is the perfect companion to this book, which assumes that you already know C#.

# Terms

+   - class library
+   - master form
+   - jQuery
+   - HTTP redirect message
+   - cross-page posting
+   - absolute URL
+   - relative URL
+   - data source
+   - session state
+   - session state object
+   - cookie

# Exercise 3-1 Build the Shopping Cart application

This exercise guides you through the process of building a Shopping Cart application similar to the one that’s presented in this chapter. This is good practice if you’re relatively new to Visual Studio and ASP.NET 4, and you’ll learn a lot by doing it. To help you get started fast, the images, database, and classes needed by the application are provided for you.

# Start the web site

+   1. Start an empty file-system web site named Ch03Cart in the C:\aspnet4_cs directory.
+   2. Add a folder named App_Data to the web site as described in figure 2-4. Then, add the existing Access database named Halloween.mdb to this folder. You can find this file in the C:\aspnet4_cs\Ch01Cart\App_Data directory.
+   3. Add a folder named App_Code to the web site. Then, add an existing class named Product to this folder as described in figure 3-4. You can find the file for this class in the App_Code folder of the C:\aspnet4_cs\Ch01Cart directory.