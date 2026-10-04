

3. Type MasterPages as the name of the folder and press Enter. Right-click this new folder and choose Add New Item. Alternatively, you can choose New File or Website Add New Item from Visual Studio's main menu, or you can click the new folder in the Solution Explorer to focus on it and then press Ctrl+Shift+A.

4. In the dialog box that appears, click Master Page and type Frontend as the name. Visual Studio will add the .master extension when you add it. Verify that under Installed Templates you have selected the language you want to use for this site and that Code in Separate File in the bottom-right corner is checked. Finally, click the Add button. The master page is added to the site, and is opened automatically for you in the Document Window.

## How It Works

This simple exercise showed you how to add a new item to your website. Although at this stage the site isn't very exciting yet, the file you added is the basis for the rest of the book. The next sections briefly look at the remainder of the file types.

## Code Files

Adding code files to the site is identical to how you add web files. The following table describes the types of code files.

| FILE TYPE | EXTENSION | DESCRIPTION |
|---|---|---|
| WCF Service | .svc | Can be called by other systems, including browsers, and can contain code that can be executed on your server. WCF services are covered in Chapter 10. |
| Class | .cs / .vb | Can contain code to program your website. Note that Code Behind files (discussed later) also have this extension because they are essentially classes. .cs files use the .cs extension and Visual Basic .vb files. |
| Global Application Class | .asax | Can contain code that is fired in response to interesting things that happen in your site, such as the start of the application or when an error occurs somewhere in the site. See how to use this file in Chapter 7 and later. |

Besides the Code Files category, there is one more group of files worth looking into: Data Files.

## Data Files

Data files are used to store data that can be used in your site and in other applications. The group consists of the XML files, database files, and files related to working with data.

## CHAPTER 2 BUILDING AN ASP.NET WEBSITE

| FILE TYPE | EXTENSION | DESCRIPTION |
| --- | --- | --- |
| XML File | .xml | Used to store data in XML format. In addition to plain XML files, ASP.NET supports a few more XML-based files, of which you will briefly saw before: Web.config and the site map. |
| SQL Server Database | .mdf | Files with an .mdf extension are databases that are used by Microsoft SQL Server. Databases are discussed in Chapter 12 and later. |
| ADO.NET Entity Data Model | .edmx | Used to access databases declaratively, without the need to write a lot of repetitive code. Technically, this is not a data file, because it does not contain the actual data. However, because it is tied to the database so closely, it makes sense to group it under this header. You learn more about the ADO.NET Entity Framework in Chapter 14. |

In the previous Try Out, adding a new file of these types is really easy. It's as easy as add existing files to the site.

## Adding Existing Files

Not every file you create in your website has to be brand new. In some cases it makes sense to reuse files from other projects. For example, you might want to reuse a logo or a CSS file across multiple sites. You can easily add existing files by right-clicking the website in the Solution Explorer and choosing Add Existing Item. In the dialog box that appears, you can browse for the files, and optionally select multiple files by holding down the Ctrl key. Finally, when you click Add, the files are added to the website. You can also copy and paste files from a folder on your disk to a website in VS. Simply highlight the files in File Explorer, Ctrl+C to copy the files, switch to VS, click the Solution Explorer (or a subfolder of your site), and press Ctrl+V. The files are then copied into your website's folder.

However, there is an even easier way to add files to the site, which can be a great time saver when you need to add multiple existing files to your site: drag and drop. The following Try Out shows how this works.

## TRY OUT Adding Existing Files to Your Site

- 1. In Windows, minimize all applications, right-click your desktop, and choose New -> Text Document. If you don't see this option, simply create a new text document using Notepad and save it on your desktop.
- 2. Rename the file to styles.css. Make sure the .txt extension is replaced by .css. If you don't see the initial .txt extension and the icon of the file doesn't change from a txt to a CSS file (by default this is the same icon as a file with a gear symbol on it, but you may have software installed that changed the icon for CSS files), Windows is configured to hide extensions for known file types. If that's the case, open Windows Explorer in Windows 7, click the Organize button, and then choose Folder and Search Options. Switch to the View tab and deselect the option labeled Hide Extensions for Known File Types. For Windows 8 you find the option called Name Extensions on the View tab of the Ribbon of the File Explorer, as shown in Figure 2-4. You may now need to change the name of the file from styles.txt to styles.css.

When you change the file extension from .txt to .css, Windows may give you a warning that the file becomes unusable if you proceed. You can safely answer Yes to this question to continue.

- 3. Rearrange VS so you can see part of the desktop with the CSS file as well. When you use the Restore Down button next to the Click button on the Windows title bar of VS to get it out of full screen mode.

- 4. Click the CSS file on the desktop and, while holding the mouse button, drag the file into the Solution Explorer and not into other parts of VS, or the file won't be added. For example, when you drag it into the Document Window, VS simply opens the file for you, but it doesn't add it.

- 5. When you release the mouse wheel over your website or an existing file in the Solution Explorer, the CSS file is added to your site.

> NOTE If you are using Windows 7 and VS as an administrator, this might not work because Windows doesn't allow the Windows Explorer and VS to communicate. In that case, add existing files using the Add Existing Item menu or use copy and paste.

## How It Works

Although this seems to be a simple exercise that uses basic Windows skills, it serves to show that VS creates a copy of the file when it adds it to the site. The original, styles.css file on the desktop is not affected when you make changes to the copy in VS. This way, it's easy to drag and drop files from existing websites into your new one without affecting the originals. The same applies to files you add using the Adding Item dialog box in VS.

If you have added files to your website's folder outside of VS, they may not show up right away. You can get a fresh copy of the file list by clicking the Refresh button on Solution Explorer's toolbar.

## Organizing Your Site

Because many of the files that make up your site, it's often a good idea to group them by function in separate folders. For example, all style files could go in a folder called Styles, .js files containing JavaScript could in Scripts, user controls could in a Controls folder, and master pages could be stored in a folder called MasterPages. This is a matter of preference, but structured and well-organized sites are easier to manage and understand. The next Try It Out explains how you can move files around into new folders to organize your site.

## CHAPTER 2 BUILDING AN ASP.NET WEBSITE

## TRY OUT Organizing Your Website

- 1. Right-click the Planet Wrote site in the Solution Explorer and choose Add New Folder.

- 2. Type styles as the new folder name and press Enter.

- 3. Create another folder, called Controls. These two folders are used in the remainder of this book.

- 4. Drag the styles.css file that you added and drop it into the styles folder.

If everything went well, your Solution Explorer should look like Figure 2-7.

If your Solution Explorer looks different from the one shown in Figure 2-7, with the same folder structure and files in it, Future Try It Out exercises in this book assume you have the correct folders and files in your website.

## How It Works

Structure and organization are important to keep your sites manageable. Although you may be tempted to add all of your files to the root of your project, it's better not to do so. With a very small site, you may notice no difference, but as your site begins to grow, you will eventually find it becomes harder to manage when it lacks structure. Placing related files in separate folders is the first step to organizing your site. Storing files of the same type in a single folder is the only way to optimize your site. In later chapters, you see that separate folders are also used to group files with similar functionality. For example, all files that are accessible only by an administrator of the site are grouped in a folder called Management.

The drag-and-drop features of VS make it easy to reorganize your site. Simply pick one file or multiple files and drop them in their new location. If you continue to apply these kinds of organization practices while expanding your site, you will find that four or six months from now, won't have any problems locating the file you need.

## Special File Types

Some of the listed files in the previous section require that you put them in a special folder instead of the proposed organizational structure. The IDE warns when you try to add a file outside of its special folder, and offers to create the folder and the file for them. For example, when you try to add a class file (with a .vb or .cs extension), you get the warning shown in Figure 2-8.

![](img/9e033e3b9560597824f8b22941d6d8bb_83_0.png)

FIGURE 2-7

![](img/9e033e3b9560597824f8b22941d6d8bb_83_1.png)

FIGURE 2-8

When you get this dialog box, always click Yes. Otherwise, your function won't work correctly. You get similar dialog boxes for other file types, including skin and database files. Now that you have a good understanding of the different types of files that make up your website, .aspx files, also known as Web Forms. It's time to look at one of them in much more detail:

