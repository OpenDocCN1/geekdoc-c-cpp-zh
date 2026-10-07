# CREATING A SAS LIBRARY USING A DIALOG BOX

This SAS naming convention is used for SAS data sets in all types of computers and operating systems – mainframes, Windows, Mac OS X, UNIX, and so on. Once you learn how to use SAS in Windows, you can easily transfer that skill to any other computer platform.

To summarize, once you've created an SAS library named MYSASLIB that points to C: \SASDATA, the data set you refer to as MYSASLIB.MAY2016 is stored on your hard drive using the name C:\SASDATA\MAY2016.SAS7BDAT.

The following section illustrates how to create an SAS library name using two methods. The first method creates an SAS library name using a Dialog Box, and the second method creates the library name in SAS code.

# 3.4 CREATING A SAS LIBRARY USING A DIALOG BOX

An easy way to create an SAS library in the Windows version of SAS (with a custom name of your choosing) is to use the New library box. To display this dialog box, make the Explorer window active (click the Explorer tab at the bottom of the main SAS screen). Select File -> New, click the Library option, and then click OK. The New Library dialog box is shown in Figure 3.2.

In the Name field, enter the name you want to assign to the library. In this book, short name MYSASLIB is used. In the Path field, find the location of the directory. In this book, the files are assumed to be in the C: \SASDATA folder on the hard drive. You will typically not change anything in the Engine drop-down or the Options field. Once you've created the MYSASLIB library, all SAS data files in C: \SASDATA become part of the library.

![](bbox=[0.163, 0.584, 0.836, 0.854])

Figure 3.2 New Library dialog box. (Source: Created with SAS® software, Version 9.4. Copyright 2012, SAS Institute Inc., Cary, NC, USA. All Rights Reserved. Reproduced with permission of SAS Institute Inc., Cary, NC)