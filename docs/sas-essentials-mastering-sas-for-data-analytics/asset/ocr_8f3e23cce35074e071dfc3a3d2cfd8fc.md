9. Examine the SAS Log. Click on the tab at the bottom of your screen and note that it contains a SAS program code you just ran. It will include statements such as the following:

> NOTE: Writing HTML Body file: sashtml.htm
NOTE: There were 18 observations read from the data set WORK.EMPLOYEES.


This indicates that the output is in an html format (web file format) and that the data set contained 18 records.

10. Clear the contents of the Log by right-clicking and selecting Edit → Clear All from the pop-up menu. In the Editor Window, right-click and select Clear All. (We'll learn a shortcut to process this later in this chapter).

The Save command saves the contents of whatever is currently active. Thus, if the Results window is active, it saves the output as *.MHT; if the Log window is active, it saves the contents as an *.LOG file; and if the Editor Window is active, it saves the code as an *.SAS (SAS program) file.

That's it! You've run your first SAS program. But wait, there's more. Now that you have one SAS job under your belt, it's time to try another one. This time, you'll make a small change to the program before you run it.

Before running each Hands-On Example, clear the Log and Editor Windows so that you will not miss information from a previous example. To clear each window, use the right-click technique previously described, or go to the window and on the menu bar select Edit → Clear All. In the section “Using SAS Function Keys” of this chapter, we will create a way to shorten this process.

# HANDS-ON EXAMPLE

In this example, you make a small change in the program and see how that alters the output.

1. In the SAS Editor Window, open the program file SECOND.SAS. (It should be in your C: \SASDATA folder). The SAS code looks like this:

```
* PUT YOUR TITLE ON THE NEXT LINE;
DATA EXAMPLE;
INPUT AGE @;
DATALINES;
12 11 12 12 9 11 8 8 7 11 12 14 9 10 7 13
6 11 12 4 11 9 13 6 9 7 13 9 13 12 10 13
11 8 11 15 12 14 10 10 13 13 10 8 12 7 13
11 9 12
```

(continued)