# Organizing files

You have two choices when organizing your Web site. You can build a few projects to manage your files, or you can build folders into the Web project and put your files there. My usual methodology is to build separate projects for the class files and folders for the Web-related files. This way, if you want to reuse the classes for a Windows Mobile application, you can easily just reference the class file project.

Web files should be in folders in the Web application. Note that this can have some implications for referencing files. If your project isn't the root of a Web server, you might have to carefully consider how to reference files.

![](bbox=[0.12, 0.42, 0.22, 0.53])

If you are deploying your Web site to a domain, like www.mynewWebsite.com, you can use a ./ to refer to files, like this:

```
<img src="./images/myImage.png">
```

If you aren't deploying to a domain — for instance, if you are making an application that lives in a folder of a site, such as www.someoneelsesite.com/myApplication, you can't use ./ because you don't know how far away the root of the application is, or what the directory really is.

ASP.NET can handle this problem for you. A construct in ASP.NET is implemented with the tilde (~), but it works only in ASP.NET controls. That means that the img HTML tag won't work with a tilde; you have to use the asp:Image control, like this:

```
<asp:Image ID="Image1" runat="server" ImageUrl="~/images/myImage.png" />
```

For organization, I have a pattern. It may or may not work for you. Please feel free to make your own. Mine breaks down like this:

+   - I put my class libraries in a separate project. Usually, I have a business logic layer (or controller) in a second project, and a data access layer (or model) in a third project.
+   - I add a Bits folder, and in that, I put folders for, well, all the bits.
+     - Style sheets
+     - Images
+     - JavaScript files
+     - Whatever else
+   - I then make a root level folder for every section of the site. If I have three top level menu items in my site, I have three folders. If I just have application files, and don't have a regular menu structure, everything will be in the root.