
## Appendix A
### How to install
and use the software
and downloadable files

To develop ASP.NET 4 applications, you need to have Visual Studio 2010 or Visual Web Developer 2010 Express Edition installed on your PC. Both of these products include a development web server that you can use to run your applications. However, because of the limitations of this server, you’ll also want to test your applications using IIS. The easiest way to do that is to install IIS on your own PC.

If you’re going to develop applications that use databases that are stored on your own PC rather than on a remote server, you also need to install SQL Server on your PC. The easiest way to do that is to install SQL Server 2008 Express Edition. In fact, this edition of SQL Server is installed by default when you install most editions of Visual Studio 2010.

This appendix shows you how to install both Visual Studio and IIS. In addition, it shows you how to install SQL Server 2008 Express Edition and how to create the SQL Server database that’s used in this book. But first, it describes the files for this book that are available for download from our web site and shows you how to download, install, and use them. We recommend you read these topics before you start developing your first web application so you can be sure that you have all the software and files you need.

- How to download and install the files for this book .................................... 778
- How to install IIS under Windows 7 or Windows Vista ................................ 780
- How to install IIS under Windows XP ................................................... 782
- How to install Visual Studio 2010 ...................................................... 784
- How to install and use SQL Server 2008 Express ....................................... 786
- How to create the Halloween database .................................................. 788
- How to use the downloaded web applications ........................................... 790

## How to download and install the files for this book

Throughout this book, you’ll see complete applications that illustrate the material presented in each chapter. To help you understand how these applications work, you can download the source code and databases for these applications from our web site at www.murach.com. Then, you can open and run them in Visual Studio. These files come in a single download, as summarized in figure A-1. This figure also describes how you download and install these files.

When you download the single install file and execute it, it will install all of the files for this book in the Murach\aspnet4_cs directory on your C drive. Within this directory, you’ll find a directory named book_applications that contains all the applications in this book. You can open and run these applications in Visual Studio as file-system applications as described in figure A-7. The exceptions are the applications for chapters 8 and 21, which must be run under IIS because they use application state, and the application for chapter 18, which must be run under IIS because it requires a digital secure certificate. The procedure for running a file-system web site under IIS is also presented in figure A-7. For more information on application state, see chapter 8. And for more information on digital secure certificates, see chapter 18.

The download also includes an Access version of the Halloween database that’s used by some of the applications in the first two sections of this book. Since the Access database is small, we’ve included it in the App_Data folder of each application that uses it so you can run these applications without any trouble.

To use the SQL Server version of the Halloween database, you’ll need to use the create_database.bat and create_database.sql files in the C:\Murach\database directory to create the database. You may also need to use some of the other files in this directory to grant ASP.NET access to the database. You’ll learn more about all of these files in figure A-6.

To help you practice the skills you’ll learn in the first three sections of this book, we’ve included exercises at the end of these chapters. We also provide starting points for many of these exercises in the C:\Murach\aspnet4_cs\exercise_starts directory. When you execute the setup file, the contents of this directory are copied to the C:\aspnet4_cs directory (creating this directory if necessary). This makes it easy to locate the exercise starts as you work through the exercises.

## What the downloadable application file for this book contains

- The source code for all of the applications presented in the book
- Access and SQL Server Express versions of the Halloween database used in these applications
- Files you can use to work with the SQL Server Express version of the Halloween database
- The starting points for the exercises in this book

## How to download and install the files for this book

- 1. Go to www.murach.com, and go to the page for *Murach’s ASP.NET 4 Web Programming with C# 2010*.
- 2. Click on the link for “FREE download of the book applications.” Then, download “All book files.” This will download one file named a4cs_allfiles.exe to your C drive.
- 3. Use Windows Explorer to find the downloaded file on your C drive. Then, double-click on this file and respond to the dialog boxes that follow. This installs the files in directories that start with C:\Murach\aspnet4_cs.

## How your system is prepared for doing the exercises

- Some of the exercises have you start from existing applications. The source code for these applications is in the C:\Murach\aspnet4_cs\exercise_starts directory. After the setup file installs the files in the download, it runs a batch file named exercise_starts_setup.bat that copies the contents of the exercise_starts directory to the C:\aspnet4_cs directory. Then, you can find all of the starting points for the exercises in directories like C:\aspnet4_cs\Ch01Cart and C:\aspnet4_cs\Ch04Cart.

## How to prepare your system for using the SQL Server database

- To use the database that comes with this book on your PC, you need to make sure that SQL Server 2008 Express is installed as described in figure A-5. Then, you need to run the batch file we provide to create the database and attach it to SQL Server Express as described in figure A-6.

## Note

- The Access version of the Halloween database is included in the App_Data folder of each application that uses it.

## How to install IIS under Windows 7 or Windows Vista

When you run an ASP.NET web application from Visual Studio, it runs under the built-in development server by default. Because of that, you don’t have to have IIS installed to develop the applications in this book or to run the applications that you download from our web site (with the exceptions noted in the previous topic). Keep in mind, however, that the built-in server has some limitations, which you’ll learn about in chapter 4. Because of that, you’ll want to install IIS so that you can thoroughly test the applications you develop. (Note that the versions of IIS that come with the Home Basic Edition and the Starter Edition of Windows Vista and Windows 7 can’t be configured for ASP.NET development. Because of that, you’ll have to use the development server that comes with ASP.NET to test your applications, or you’ll need to have access to a separate web server.)

Figure A-2 shows how to install IIS under Windows 7 or Windows Vista. To start, you display the Windows Features dialog box as described here. This dialog box lists all the available Windows features. If all of the features of a component are installed, the check box in front of the component will have a check mark in it. If only some of the features are installed, the check box for the component will be shaded.

To install the default features of IIS, you simply check its box and then click the OK button. If you want to install features other than the defaults, you can expand the Internet Information Services node and any of its subordinate nodes to select the features you want. By default, the features listed in step 3 of this figure should be selected. However, in some cases they aren’t, so you need to select them. Similarly, if you want to use IIS as an FTP server so you can develop applications over the Internet, you need to select the FTP Server feature as described in step 4.

Note that the versions of IIS that come with Windows Vista (IIS 7.0) and Windows 7 (IIS 7.5) don’t include FrontPage Server Extensions (FPSE). Because of that, you can’t work with web sites on a remote server. Since the release of IIS 7.0, however, an edition of FPSE that works with IIS 7.0 and later has become available. You can download this product from the IIS web site as described in this figure.
