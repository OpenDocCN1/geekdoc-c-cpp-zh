# CHAPTER 3: READING, WRITING, AND IMPORTING DATA

# 3.5 CREATING A SAS LIBRARY USING CODE

Another way to create an SAS Library (nickname) is by using code. Creating a library within the code makes it active while the SAS software is running. When you exit the SAS software program (File → Exit), the library nickname is “forgotten” by SAS, although any permanent data sets you created stored in your folder referred to by the library. You may use these permanent data sets again by re-creating a library nickname pointing to the Windows folder where the data file is stored.

The following SAS code creates an SAS library named MYLIB2 at the location C:\SASDATA:

```
LIBNAME MYLIB2 "C:\SASDATA";
```

When SAS reads this code at the beginning of your SAS program, the library (library name) MYLIB2 is created and can subsequently be used as part of a permanent data set name. For example, suppose you have a data set name SURVEYDBAT in the folder C:\SASDATA. Once you define the library MYLIB2 pointing to that folder, you can refer to that data set using the SAS data name MYLIB2.SURVEY.

Note that for illustrative purposes we are creating the library named MYLIB2 that has a different name than MYSASLIB previously created, but they are both nicknames to the C:\SASDATA folder. There is no conflict in creating two SAS library names that point to the same folder on your drive, although in practice, you would not normally have two library examples.

# HANDS ON EXAMPLE

In this example, you will define an SAS library in code and use the library name to read in an SAS data file.

+   1. In SAS Explorer, display the window Contents of SAS Environment. Refer to previous examples if you don’t remember how to display this window. Double-click the Libraries icon, shown previously in Figure 3.3.
2. A new window named Active Libraries appears. Examine the active library names. There should be a library named MYLIB2.
3. In the window, open the program LIBNAME.SAS, which contains the following code:

LIBNAME MYLIB2 "C:\SASDATA";
RUN;
4. Run this program. The LIBNAME statement creates the SAS library nickname MYLIB2 but does not create any output. Examine the Active Libraries window in the SAS Explorer. There is now a library icon named MYLIB2. The folder represented by the filing cabinet icon indicates that SAS created the MYLIB2 library.
5. Double-click the MYLIB2 icon and verify that the library includes one or more data sets (including the data sets SOMEDATA, CARS, and others). Note that this new library contain the same data sets as the MYSASLIB library because they are both defined as nicknames for “pointing to” C:\SASDATA.