5. Click the Install button. A dialog box pops up lists the actions that are executed to install the package. That dialog box has disappeared, click the Close button to dismiss the Manage Nuget Packages dialog box.

That's it. You just installed jQuery using NuGet.

# How It Works

To see how it works, take a look at the Scripts folder in your Solution Explorer. You will see an item called jquery-2.0.3.js, shown in Figure 11-3. Remember, a new version has been released since this book was written so your version numbers may be different. During installation, NuGet added four jQuery-JavaScript scripts to your Scripts folder (which would have created if it didn't exist). In addition, keep track of the installed packages in a file config in the root of your project to store a local copy of the downloaded packages. Depending on your settings, this location could differ, but most it's located in a folder named after your site in Documents\Visual Studio 2013\Projects.

These .js files serve a different purpose. The jquery-2.0.3.js contains the core jQuery in an uncompressed format. This means you can read it and use it for debugging in cases where you need to see what code the library executes. The file jquery-2.0.3.intellense.js contains the documentation for the jQuery library that is used in the IntelliSense lists and documentation pop-ups. You see how this works later in the chapter. The file jquery-2.0.3.min.js is the core library in a compressed format. This has the smallest size and is the quickest to download. Finally, the .map file is only used when you want to debug the jQuery library itself because it provides a mapping between the code in the minified and the code in the uncompressed, compressed file.

![](bbox=[0.693, 0.301, 0.952, 0.6])

FIGURE 11-3

Now that the jQuery library has been added to the website, the next step is determining where to use it. The jQuery library adds to the size of your web pages, so it should be a deliberate choice whether or not to include it in your site.

# Choosing the Location for Your jQuery Reference

To include jQuery in your website, you have a couple of options:

+   - Add a reference to the jQuery library in just the web pages or use controls that require it.
- Add a reference to the jQuery library in the master page of your site so it's available in all pages.

Both methods have their advantages and disadvantages. Adding a reference to the jQuery library in the pages that it helps keeps the size of your pages down a bit. When your users browse only to pages without jQuery, they'll never have to download the library file, saving them