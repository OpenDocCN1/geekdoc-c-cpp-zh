# 10 Learning SAS by Example: A Programmer's Guide, Second Edition

```
title "Summary Statistics";nproc means data=Demographic;
var Age Height Weight;
run;
```

Notice that this program consists of one DATA step followed by PROC steps. As we mentioned in Chapter 1, the DATA step begins with the word DATA. In this program, the SAS data set being created is Demographic. The next line (INFILE statement) tells SAS where the data values are coming from. In this example, the file Mydata.txt is in the folder C:\books\learning on a Windows system.

If you decide to run some of the programs in this book, you can download all the programs and data files from the website (support.sas.com/copy) and place them in a folder of your. For example, if you placed the file Mydata. txt in a folder C:\SASdata, your INFILE statement would be:

```
infile "C:\SASdata\Mydata.txt";
```

If you are using the SAS University Edition, you may want to place all the data files in the folder C:\UniversityEdition\Folders, which is the default location you set up when you configured your virtual machine.

The INPUT statement shown here is one of four methods that SAS has for reading data. This program uses the list method, appropriate for data values separated by delimiters. The default delimiter for SAS is blank. SAS can also read data separated by any other delimiter (for example, commas or tabs) to make the INFILE statement. If you use the list method for reading data, you need to list only the names you want to give each data value. SAS calls these variable names. As mentioned in Chapter 1, these names must correspond to the SAS naming convention.

Notice the dollar sign ($) following the variable name Gender. The dollar sign following any variable name tells SAS that these variables are stored as character values. Without a dollar sign, SAS assumes values are numbers and should be stored as SAS numeric values.

Finally, the DATA step ends with a RUN statement. You will see that, depending on what platform you are running your program, RUN statements are not always necessary.

In Program 2 we placed a blank line between each step to make the program easier to read. Feel free to include blank lines whenever you wish to make the program more readable.

There are several TITLE statements in this program. You will see this statement in many of the SAS programs in this book. As you have guessed, the keyword TITLE (placed in single or double quotes, or even no quotes—as long as the line doesn't contain any quotes) is printed on the top of each page of output. Statements such as the TITLE are global statements. The term global refers to the fact that the operations performed are not tied to one single DATA or PROC step. They affect the SAS environment. In addition, the operations performed by these global statements remain effect effect they are changed. For example, if you use a single TITLE statement in the beginning of your program, that title will head every page of output from that point until you write another TITLE statement. It is a good practice to place a TITLE statement before any procedure that produces output to make it easy for someone to read and understand the information on the page. If you exit your SAS session, your titles are reset and you need to submit new TITLE statements if you want them to appear.