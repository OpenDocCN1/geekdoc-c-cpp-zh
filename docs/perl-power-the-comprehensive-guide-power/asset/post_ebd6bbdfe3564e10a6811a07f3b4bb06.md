
## CHAPTER 2 Getting Started

### Obtaining the DzSoft Perl Editor

As Table 2.1 indicates, the internet address of DzSoft is http://www.dzsoft.com. Figure 2.18 illustrates the home page for DzSoft with a view of the DzSoft Perl Editor. Click the Perl Editor link.

**Figure 2.18** DzSoft lists the Perl Editor among other selections.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_42_0.png)

In the page that describes the Perl Editor (see Figure 2.19), click on the Click Here to Download link. The download dialog immediately appears. Click the Save option and save the executable to your local drive.

Generally, it is best to save the installation executable to your local drive. Figure 2.20 illustrates a folder set up as c:\executables\DzSoft. Create such a folder and save the executable (currently, the version is dzperl57.exe) to it.

DzSoft provides half off prices if you are a student, so you might want to keep this in mind if you are in that category. Otherwise, you see the price posted. When you buy your license, DzSoft sends it to you in an e-mail. As a precaution, save a copy of the license to the directory in which you store the installation executable. Figure 2.21 illustrates a saved file with the license and the DzSoft installation file.

**Figure 2.19** The Click Here to Download link immediately starts the download.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_43_0.png)

**Figure 2.20** Save the installation executable in case problems occur.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_43_1.png)

**Figure 2.21** If you purchase DzSoft's Perl Editor, you receive a key in an e-mail, which you can save to a text file and then cut and paste into the license window.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_43_2.png)

To begin the installation, use the Windows Start > Control Panel option. Select Add or Remove Programs. Click Add New Programs. Click CD or Floppy and the Next button. Click the Browse button and select the directory in which you have placed the DzSoft installation executable for the Perl Editor. You must set the Files of Type field to _All Files_ to see the DzSoft installation executable. Then select the DzSoft executable and click Open. The Run Installation Program dialog appears. Click Finish.

You’ll then see a security warning. The publisher, DzSoft, is identified. You can safely install the program. Click Run. As Figure 2.22 illustrates, you’ll then see the standard installer for DzSoft.

**Figure 2.22** DzSoft is ready to install.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_44_0.png)

After that you see the license dialog. Click the radio button and Next to show you agree with the terms of the license.

Use the default directory DzSoft provides (see Figure 2.23). Click Next.

In Select Start Menu folder, allow DzSoft to create a shortcut for you using the default name (DzSoft Perl Editor). Click Next.

In the Select Additional Tasks dialog, leave the first two options as they are. (See Figure 2.24.) Still, if you do not want a desktop icon or a Quick Launch icon (this appears in the tray of your desktop), you can certainly deselect these options.

**One important point!** Deselect the option for Associate with Perl Files. You can always associate the *.pl extension with DzSoft, but for now do not do so. It is best if you allow the *.pl extension to invoke the Perl interpreter rather than DzSoft. Click Next.

**Figure 2.23** Accept the default directory.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_45_0.png)

**Figure 2.24** Deselect the box for Associate with Perl Files.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_45_1.png)

In the Ready to Install dialog, you’ll see the files and directories to be created. Click Install. You’ll see a window with a progress bar, and then the final dialog appears. Leave the Launch DzSoft Perl Editor item checked and click Finish.

### First View of the Perl Editor

**Figure 2.25** By default, you’ll see a Perl program that prints an HTML message.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_46_0.png)

As Figure 2.25 illustrates, your first view of the DzSoft Perl Editor provides you with a Perl file that is ready to be run. Notice the Edit and Run tabs on the left and the Perl program in the edit area on the left.

As you can see from Figure 2.25, the first message you see creates an HTML document. The document consists of three lines. The first line is called the “bang” line. This identifies the directory in which the Perl interpreter resides. A blank line follows. Then you’ll see two lines that begin with `print`. In each line, the Perl code consists of the word `print`, double quotation marks, and a semicolon at the end of the line. Inside the double quotation marks on each line are HTML messages. When these messages appear in a browser, you see standard HTML.

### HTML Output

To execute the file, select Run > Quick Run from the top menu. Alternatively, press F9.

As illustrated in Figure 2.26, the window changes immediately. You see As Text and In Browser tab options. By default, the display shows the In Browser tab, so in the case of the program DzSoft provides, you see the printed HTML line as it might appear in a standard browser.

**Figure 2.26** DzSoft parses your file to allow you to check the syntax of your program and to show HTML output.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_47_0.png)

> If your DzSoft Perl Editor window differs from what you see in the screenshots in this chapter, select View > Status Bar or View > Toggle Code Explorer. To eliminate line numbers, select View > Options > Editor and deselect both Show Line Numbers and Show Line Numbers on Gutter.
>
> Also, when you use your DzSoft Perl Editor, use Shift + F9 to execute the files in this book. They are developed for command line interaction. When you press F9 alone, you invoke the interpreter for web content, and some of the programs are not designed to display in this mode.

To gain a sense of how easy it is to edit your code, click the Edit tab. Then change the Perl file so it reads as follows. (Do not save your work for now. When you finish, click the Run tab. Then click In Browser.)

```perl
#! /usr/bin/perl

print "Content-type: text/html\n\n";
print "<html><h1>Hello</h1>\n";
print "<h1>World!</h1></html>\n";
```

Figure 2.27 illustrates the code as changed in the edit area.

**Figure 2.27** Click the In Browser tab to view web content.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_47_1.png)

### Text Output and the DOS Window

Now that you have had a chance to look at how the DzSoft Perl Editor handles HTML, click on the As Text tab. The As Text tab allows to see the output as it appears at the command line (most of the programs you write in this book during the first several chapters involve the command line rather than the browser). Figure 2.28 shows you the result.

In the course of this book, you’ll work both from the text view and the browser view as you work with your Perl code. For the programs in this text, execute them by pressing Shift + F9. This approach does not display your programs in the DzSoft Text area but instead allows you to see them in a separate DOS window. When you execute the programs in the DOS window, you put yourself in a much better position to work with the programs outside of any given editing environment. To close the programs, you press Return. This returns you directly to the DzSoft Editor, and you can make changes as needed.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_47_2.png)

**Figure 2.28** You see the text output as it might appear if processed at the command prompt of the operating system.

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_48_0.png)

### Saving Files

To save a file, select File > Save. Navigate to MyPerlPrograms. Save the file you have modified as HelloWorld01. You’ll see files with the *.pl file. This is the extension for Perl files. (See Figure 2.29.)

**Figure 2.29** You’ll see the file type as Perl Files (the *.pl extension).

![](img/fd17b6cf7ddc9bc7e6f1529936c3ac84_48_1.png)
