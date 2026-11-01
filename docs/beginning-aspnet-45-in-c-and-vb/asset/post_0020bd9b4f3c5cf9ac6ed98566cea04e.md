
> **COMMON MISTAKES** Don't mistakenly create a new Web Application Project using File ▸ New Project, because this project template is not compatible with the exercises in this book.

- 3. In the target framework drop-down list at the top of the screen, select .NET Framework 4.5.
- 4. In the Installed Templates area on the left, choose between Visual Basic and Visual C#. All the examples in this book are shown in both programming languages, so you can choose the one you like best.
- 5. In the area in the middle select ASP.NET Empty Web Site.
- 6. In the Web Location drop-down list, make sure that File System is selected. The other two options (HTTP and FTP) enable you to open a site running on IIS (either on your local machine or on a remote server using the so-called Microsoft FrontPage Server Extensions) and open a site from an FTP server, respectively.
- 7. Click the Browse button next to the location text box, browse to C:\BegASPNET\Site (the folder you created in the first part of this exercise), and click Open.

Your final screen should look like the one in Figure 2-2, except that you may have chosen Visual C# instead of Visual Basic.

![](img/eadab2ccd79b253c01a3fdff2321202d_83_0.png)

FIGURE 2-2

- 8. Click OK and VS creates the new site for you.

## How It Works

As soon as you click OK, VS creates a new, empty website for you. This new website contains nothing but a configuration file (called Web.config). In the Solution Explorer, your website now looks like Figure 2-3. If you don't see the top-level Solution node, choose Tools > Options in VS, and in the Projects and Solutions category select Always Show Solution.

![](img/eadab2ccd79b253c01a3fdff2321202d_84_0.png)

Because a website based on the Empty Web Site template is just a simple Windows folder that VS looks at, the actual folder on disk contains the same file. No additional files are used to create the site, as shown in Figure 2-4, which shows File Explorer displaying the files in the folder C:\BegASPNET\Site.

![](img/eadab2ccd79b253c01a3fdff2321202d_84_1.png)

If you don't see the .config extension of the web file, don't worry. You see how to view file extensions in a later exercise.

As you progress through this book, you'll add new files and folders to the site. These additional files and folders show up in the Solution Explorer and will appear in the Windows folder at C:\BegASPNET\Site as well.

Opening websites based on the Web Site Project template is very similar to creating new ones. In the next section, you get a quick overview of opening existing sites in VS.

## Opening Existing Websites

Just as with creating new sites, opening an existing site in VS gives you a few options with regard to the source location of the website. You can choose to open a site from the local filesystem, from a local IIS web server, from a remote server using FTP, from a remote site using the Microsoft FrontPage Server Extensions, or from a central Source Control system such as Microsoft's Team Foundation Server. Figure 2-5 shows the Open Web Site dialog box in VS.

| FILE TYPE | EXTENSION | DESCRIPTION |
|---|---|---|
| Web Form | .aspx | The workhorse of any ASP.NET website; represents the pages that your users view in their browsers. |
| Master Page | .master | Enables you to define the global structure and the look and feel of a website. You see how it can be used in Chapter 6. |
| Web User Control | .ascx | Contains page fragments that can be reused in multiple pages in your site. Chapter 8 is entirely devoted to user controls. |
| HTML Page | .htm/.html | Can be used to display static HTML in your website. |
| Style Sheet | .css | Contains CSS code that enables you to style and format your website. You learn more about CSS in Chapter 3. |
| Web Configuration File | .config | Contains global configuration information that is used throughout the site. You see how to use the Web.config later in this book, starting with Chapter 4. |
| Site Map | .sitemap | Contains a hierarchical representation of files in your site in an XML format. The site map is used for navigation and is discussed in Chapter 7. |
| JavaScript File | .js | Contains JavaScript that can be executed in the client's browser. |
| Skin File | .skin | Contains design information for controls in your website. Skins are discussed in Chapter 6. |

The next Try It Out exercise shows you how to add a new master page to the site, which is used throughout the book.

### TRY IT OUT Adding Files to Your Site

- 1. If it is not still open, open the Planet Wrox website you created earlier by choosing File ▸ Open Web Site. Make sure that you open the site from the filesystem, locate the folder that contains your site (C:\BegASPNET\Site), and click the Open button.
- 2. In the Solution Explorer, right-click your site and choose Add ▸ New Folder.

> **COMMON MISTAKES** Make sure you click the actual site and not the Web.config file or the Solution node at the top (see Figure 2-3) or you won't get the correct menu item.

## Data Files

Data files are used to store data that can be used in your site and in other applications. The group consists of the XML files, database files, and files related to working with data.

| FILE TYPE | EXTENSION | DESCRIPTION |
|---|---|---|
| XML File | .xml | Used to store data in XML format. In addition to plain XML files, ASP.NET supports a few more XML-based files, two of which you briefly saw before: Web.config and the site map. |
| SQL Server Database | .mdf | Files with an .mdf extension are databases that are used by Microsoft SQL Server. Databases are discussed in Chapter 12 and later. |
| ADO.NET Entity Data Model | .edmx | Used to access databases declaratively, without the need to write a lot of repetitive code. Technically, this is not a data file, because it does not contain the actual data. However, because it is tied to the database so closely, it makes sense to group it under this header. You learn more about the ADO.NET Entity Framework in Chapter 14. |

As you saw in the previous Try It Out, adding a new file of any of these types is really easy. It's just as easy to add existing files to the site.

## Adding Existing Files

Not every file you create in your website has to be brand new. In some cases it makes sense to reuse files from other projects. For example, you may want to reuse a logo or a CSS file across multiple sites. You can easily add existing files by right-clicking the website in the Solution Explorer and choosing Add ▸ Add Existing Item. In the dialog box that appears, you can browse for the files, and optionally select multiple files by holding down the Ctrl key. Finally, when you click Add, the files are added to the website. You can also use copy and paste to copy files from a folder on your local disk to a website in VS. Simply highlight the files in Windows Explorer, press Ctrl+C to copy the files, switch to VS, click the website in the Solution Explorer (or on a subfolder of your site), and press Ctrl+V. The files are then copied into your website's folder.

However, there is an even easier way to add files to the site, which can be a great time saver when you need to add multiple existing files and folders to your site: drag and drop. The following Try It Out shows you how this works.

### TRY IT OUT Adding Existing Files to Your Site

- 1. In Windows, minimize all open applications, right-click your desktop, and choose New ▸ Text Document. If you don’t see this option, simply create a new text document using Notepad and save it on your desktop.
- 2. Rename the file `Styles.css`. Make sure the `.txt` extension is replaced by `.css`. If you don't see the initial `.txt` extension and the icon of the file doesn't change from a text file to a CSS file (by default this is the same icon as a text file with a gear symbol on top of it, but you may have software installed that changed the icon for CSS files), Windows is configured to hide extensions for known file types. If that's the case, open up Windows Explorer in Windows 7, click the Organize button, and then choose Folder and Search Options. Switch to the View tab and deselect the option labeled Hide Extensions for Known File Types. For Windows 8 you find the option called File Name Extensions on the View tab of the Ribbon bar of the File Explorer, shown in Figure 2-4. You now may need to change the name of the file from `Styles.css.txt` to `Styles.css`.

When you change the file extension from `.txt` to `.css`, Windows may give you a warning that the file becomes unusable if you proceed. You can safely answer Yes to this question to continue.

- 3. Rearrange VS so you can see part of the desktop with the CSS file as well. You can use the Restore Down button next to the Close button on the Windows title bar of VS to get it out of full screen mode.
- 4. Click the CSS file on the desktop and, while holding down the mouse button, drag the file into the Solution Explorer. Make sure you drag the file into the Solution Explorer and not into other parts of VS, or the file won't be added. For example, when you drag it into the Document Window, VS simply opens the file for you, but doesn't add it to the site.
- 5. When you release the mouse while over the website node or an existing file in the Solution Explorer, the CSS file is added to your site.

> **NOTE** If you are using Windows 7 and run VS as an administrator, this might not work because Windows doesn't allow the Windows Explorer and VS to communicate. In that case, add existing files using the Add Existing Item menu discussed earlier or use copy and paste.

## How It Works

Although this seems to be a simple exercise that uses basic Windows skills, it serves to show that VS creates a `copy` of the file when it adds it to the site. So, the original `Styles.css` file on the desktop is not affected when you make changes to the copy in VS. This way, it's easy to drag and drop files from existing websites into your new one without affecting the originals. The same applies to files you add using the Add Existing Item dialog box in VS.

If you have added files to your website's folder outside of VS, they may not show up right away. You can get a fresh copy of the file list by clicking the Refresh button on the Solution Explorer's toolbar.
