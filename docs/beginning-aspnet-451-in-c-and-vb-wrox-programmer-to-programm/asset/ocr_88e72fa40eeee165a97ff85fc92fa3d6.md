# CHAPTER 2 BUILDING AN ASP.NET WEBSITE

# TRY OUT Organizing Your Website

+   1. Right-click the Planet Wrote site in the Solution Explorer and choose Add New Folder.

+   2. Type styles as the new folder name and press Enter.

+   3. Create another folder, called Controls. These two folders are used in the remainder of this book.

+   4. Drag the styles.css file that you added and drop it into the styles folder.

If everything went well, your Solution Explorer should look like Figure 2-7.

If your Solution Explorer looks different from the one shown in Figure 2-7, with the same folder structure and files in it, Future Try It Out exercises in this book assume you have the correct folders and files in your website.

# How It Works

Structure and organization are important to keep your sites manageable. Although you may be tempted to add all of your files to the root of your project, it's better not to do so. With a very small site, you may notice no difference, but as your site begins to grow, you will eventually find it becomes harder to manage when it lacks structure. Placing related files in separate folders is the first step to organizing your site. Storing files of the same type in a single folder is the only way to optimize your site. In later chapters, you see that separate folders are also used to group files with similar functionality. For example, all files that are accessible only by an administrator of the site are grouped in a folder called Management.

The drag-and-drop features of VS make it easy to reorganize your site. Simply pick one file or multiple files and drop them in their new location. If you continue to apply these kinds of organization practices while expanding your site, you will find that four or six months from now, won't have any problems locating the file you need.

# Special File Types

Some of the listed files in the previous section require that you put them in a special folder instead of the proposed organizational structure. The IDE warns when you try to add a file outside of its special folder, and offers to create the folder and the file for them. For example, when you try to add a class file (with a .vb or .cs extension), you get the warning shown in Figure 2-8.

![](bbox=[0.693, 0.262, 0.873, 0.403])

FIGURE 2-7

![](bbox=[0.493, 0.688, 0.873, 0.808])

FIGURE 2-8

When you get this dialog box, always click Yes. Otherwise, your function won't work correctly. You get similar dialog boxes for other file types, including skin and database files. Now that you have a good understanding of the different types of files that make up your website, .aspx files, also known as Web Forms. It's time to look at one of them in much more detail: