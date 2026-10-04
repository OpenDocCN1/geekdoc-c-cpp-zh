# CHAPTER 11 JQUERY

Probably the most popular commands are Get-Package and Install-Package. Using GetPackage you list the packages that are currently installed in your site. To see the list, just type the command and hit Enter. If you try this now, you should see the Modernizr and FriendlyUrls packages. Using Get-Package -ListAvailable you can see a complete list of all available packages. Because thousands of them exist (and the list is growing), you want to filter the list using -Filter, like this:

```
Get-Package -ListAvailable -Filter jquery
```

This lists all the packages that have jQuery in your name. Note that filtering isn't case sensitive. To find prerelease versions of packages that haven't been officially released yet, you use the -PreRelease option, like this:

```
Get-Package -ListAvailable -Filter jquery -PreRelease
```

Once you find the package you want to install, use the Install-Package command. As an argument, you need to supply the name of the package. For example, to install jQuery into your website you execute the following command:

```
Install-Package jquery
```

After you hit Enter, the Manager Console downloads the package and installs it in your website exactly the same as the Manage NuGet Packages dialog box.
For a complete overview of all available commands, look the Official NuGet documentation at http://docs.nuget.org. You can find the command-line reference here: http://bit.ly/qOnBS7L.
In the next exercise, you use the Manage NuGet Packages dialog box to install the jQuery library into your website.

# TRY IT OUT Using NuGet to Install Packages

In this exercise you see how to find and install the latest jQuery package using the Manage NuGet Packages dialog box. Using the dialog box is the most intuitive and easiest way, so it's a good place to get started with NuGet. In later parts of this book you also use the Console to install packages.

+   1. Start by opening the Manage NuGet Packages dialog box. You can do that by right-clicking in the Solution Explorer and choosing Manage NuGet Packages. Alternatively, you can choose Tools > NuGet Package Manager > Manage NuGet Packages for Solution. The dialog box shown in Figure 11-1.
2. If it's not already selected, click the Online item in the list on the left.
3. Because jquery is so popular, it should appear in the list with packages that are shown by default. If it's not, or if you want to install another package, use the search box in the top-right corner of the dialog box.
4. Click the jQuery library package in the list. Make sure you choose the jQuery library, or jQuery Validation package, because these serve a different purpose.