# Data Files

Data files are used to store data that can be used in your site and in other applications. The group consists of the XML files, database files, and files related to working with data.

| FILE TYPE | EXTENSION | DESCRIPTION |
|---|---|---|
| XML File | .xml | Used to store data in XML format. In addition to plain XML files, ASP.NET supports a few more XML-based files, two of which you briefly saw before: Web.config and the site map. |
| SQL Server Database | .mdf | Files with an .mdf extension are databases that are used by Microsoft SQL Server. Databases are discussed in Chapter 12 and later. |
| ADO.NET Entity Data Model | .edmx | Used to access databases declaratively, without the need to write a lot of repetitive code. Technically, this is not a data file, because it does not contain the actual data. However, because it is tied to the database so closely, it makes sense to group it under this header. You learn more about the ADO.NET Entity Framework in Chapter 14. |

As you saw in the previous Try It Out, adding a new file of any of these types is really easy. It's just as easy to add existing files to the site.

# Adding Existing Files

Not every file you create in your website has to be brand new. In some cases it makes sense to reuse files from other projects. For example, you may want to reuse a logo or a CSS file across multiple sites. You can easily add existing files by right-clicking the website in the Solution Explorer and choosing Add ⇦ Add Existing Item. In the dialog box that appears, you can browse for the files, and optionally select multiple files by holding down the Ctrl key. Finally, when you click Add, the files are added to the website. You can also use copy and paste to copy files from a folder on your local disk to a website in VS. Simply highlight the files in Windows Explorer, press Ctrl+C to copy the files, switch to VS, click the website in the Solution Explorer (or on a subfolder of your site), and press Ctrl+V. The files are then copied into your website's folder.

However, there is an even easier way to add files to the site, which can be a great time saver when you need to add multiple existing files and folders to your site: drag and drop. The following Try It Out shows you how this works.

# TRY IT OUT Adding Existing Files to Your Site

+   1. In Windows, minimize all open applications, right-click your desktop, and choose New ⇦ Text Document. If you don’t see this option, simply create a new text document using Notepad and save it on your desktop.