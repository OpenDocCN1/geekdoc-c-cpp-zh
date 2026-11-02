
## Chapter 2: Setting Up Your Computer

### In This Chapter

- Installing Java
- Downloading and installing the Eclipse integrated development environment
- Checking your Eclipse configuration
- Getting the code in this book's examples

This book tells you how to write Java programs, and before you can write Java programs, you need some software. At the very least, you need the software that I describe in Chapter 1 — a Java compiler and a Java Virtual Machine (JVM, for short). You can also use a good integrated development environment (IDE) and some sample code to get you started.

All the software you need for writing Java programs is free. The software comes as three downloads — one from this book's website, another from Oracle, and a third from eclipse.org.

![](img/f938eba5f15e231d828a6255e7ec5523_38_0.png)

The Oracle and Eclipse websites that I describe in this chapter are always changing. The software that you download from these sites changes, too. A specific instruction such as "click the button in the upper-right corner" becomes obsolete (and even misleading) in no time at all. So in this chapter, I provide long lists of steps, but I also describe the ideas behind the steps. Browse each of the suggested sites and look for ways to get the software that I describe. When a website offers you several options, check the instructions in this chapter for hints on choosing the best option. If your computer's Eclipse window doesn't look quite like the window in this chapter's figures, scan your computer's window for whatever options I describe. If, after all that, you can't find what you're looking for, check this book's website (http://allmycode.com/BeginProg) or send an e-mail to me at BeginProg@allmycode.com. You can also find me on Facebook at /allmycode or on Twitter at @allmycode.

### If You Don't Like Reading Instructions . . .

I start this chapter with a very brief (but useful) overview of the steps required to get the software you need. If you're an old hand at installing software, and if your computer isn't quirky, these steps will probably serve you well. If not, you can read the more detailed instructions in the next several sections.

Here's how you get the software for creating Java programs:

1. Visit http://allmycode.com/BeginProg and download a file containing all the program examples in this book.

2. Visit www.oracle.com/technetwork/java/javase/downloads and get the latest available version of the JDK.

   Choose a version of the software that matches your operating system (Windows, Macintosh, or whatever). If you have trouble choosing between 32-bit software and 64-bit software, the 32-bit versions are safer choices. If you have trouble choosing between the JRE and the JDK, pick the JDK.

If you're in a hurry (and who isn't?), you may benefit from a quick visit to http://java.com. The http://java.com website offers a hassle-free, one-click Java installer. (Simply click a big Java Download button. You can't miss it.) The Java Download button doesn't work on all computers. But if it works for you, with a wave of a virtual magic wand, you're finished with this step. You can bypass the complexities of the oracle.com website and move immediately to Step 3.

![](img/f938eba5f15e231d828a6255e7ec5523_39_0.png)

3. Visit http://eclipse.org/downloads and get the Eclipse IDE.

   Select the Eclipse IDE For Java Developers. The resulting download is a compressed archive file (for Windows, a .zip file; for other operating systems, including Macintosh OS X, a .tar.gz file).

4. Extract the contents of the downloaded Eclipse archive.

   The archive contains a folder named eclipse. Extract this eclipse folder to a handy place in your computer's hard drive. For example, on my Windows computer, I have a C:\eclipse folder. On my Mac, I have an eclipse folder inside my Applications folder.

   In Windows, the blank space in the name Program Files confuses some Java software. I don't think any of this book's software presents such a problem, but I can't guarantee it. So if you want, extract Eclipse to your C:\Program Files or C:\Program Files (x86) folder. But make a mental note about your choice (in case you run into any trouble later).

![](img/f938eba5f15e231d828a6255e7ec5523_39_1.png)

5. Launch Eclipse and click the Welcome screen's Workbench icon.

   Initially, the Welcome screen's icons have no text labels. But when you hover over an icon, a tooltip appears. Select the icon whose tooltip has the title Workbench.

6. In Eclipse, import the code that you downloaded in Step 1.

For details about any of this stuff, see the next several sections.

### Those pesky filename extensions

The filenames displayed in Windows File Explorer or in a Finder window can be misleading. You may browse one of your directories and see the name Mortgage. The file's real name might be Mortgage.java, Mortgage.class, Mortgage.somethingElse, or plain old Mortgage. Filename endings like .zip, .java, and .class are called filename extensions.

The ugly truth is that, by default, Windows and Macs hide many filename extensions. This awful feature tends to confuse programmers. So, if you don't want to be confused, change your computer's system-wide settings. Here's how you do it:

- In Windows XP: Choose Start→Control Panel→Appearance and Themes→Folder Options. Then follow the instructions in the In All Versions of Windows bullet.
- In Windows 7: Choose Start→Control Panel→Appearance and Personalization→Folder Options. Then follow the instructions in the In All Versions of Windows bullet.
- In Windows 8: In the Start screen, hold down the Windows key while pressing Q.

  In the resulting search box, type Folder Options and then press Enter. Then follow the instructions in the In All Versions of Windows bullet.

- In all versions of Windows (XP and newer): Follow the instructions in one of the preceding bullets. Then, in the Folder Options dialog box, click the View tab. Look for the Hide File Extensions for Known File Types option. Make sure that this check box is not selected.
- In Mac OS X: In the Finder application's menu, select Preferences. In the resulting dialog box, select the Advanced tab and look for the Show All File Extensions option. Make sure that this check box is selected.
- In Linux: Linux distributions tend not to hide filename extensions. So, if you use Linux, you probably don't have to worry about this. But I haven't checked all Linux distributions. So, if your files are named Mortgage instead of Mortgage.java or Mortgage.class, check the documentation specific to your Linux distribution.

### Getting This Book's Sample Programs

To get copies of this book's sample programs, visit http://allmycode.com/BeginProg and click the link to download the programs in this book. Save the download file (BeginProgJavaDummies4.zip) to your computer's hard drive.

![](img/f938eba5f15e231d828a6255e7ec5523_41_0.png)

In some cases, you click a download link, but your web browser doesn't offer you the option to save a file. If this happens to you, right-click the link (or control-click on a Mac). In the resulting context menu, select Save Target As, Save Link As, Download Linked File As, or a similarly labeled menu item.

Most web browsers save files to a Downloads directory on your computer's hard drive. But your browser may be configured a bit differently. One way or another, make note of the folder containing the downloaded BeginProgJavaDummies4.zip file.

### Compressed archive files

When you visit http://allmycode.com/BeginProg and you download this book's Java examples, you download a file named BeginProgJavaDummies4.zip. A .zip file is a single file that encodes a bunch of smaller files and folders. So, for example, my BeginProgJavaDummies4.zip file encodes folders named 06-01, 06-02, and so on. The 06-02 folder contains some subfolders, which in turn contain files. (The folder named 06-02 contains the code in Listing 6-2 — the second listing in Chapter 6.)

A .zip file is an example of a compressed archive file. Some other examples of compressed archives include .tar.gz files, .rar files, and .cab files. Uncompressing a file means extracting the original files stored inside the big archive file. (For a .zip file, another word for "uncompressing" is "unzipping.") Uncompressing normally recreates the folder structure encoded in the archive file. So, after uncompressing my BeginProgJavaDummies4.zip file, your hard drive has folders named 06-01, 06-02, with subfolders named src and bin, which in turn contain files named SnitSoft.java, SnitSoft.class, and so on.

When you download BeginProgJavaDummies4.zip, your web browser may uncompress the file automatically for you. If not, you can see the .zip file's contents by double-clicking the file's icon. (In fact, you can copy the file's contents and perform some other file operations after double-clicking the file's icon.) One way or another, don't worry about uncompressing my BeginProgJavaDummies4.zip file. When you follow this chapter's instructions, you import the contents of my BeginProgJavaDummies4.zip file into the Eclipse IDE. And behind the scenes, Eclipse's import process uncompresses the .zip file.
