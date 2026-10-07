# TIPS AND TRICKS FOR RUNNING SAS PROGRAMS

```
DATA – Create a SAS data set

PROC – Use SAS procedures to perform an analysis

OUTPUT – Results of the analysis
```

Figure 1.4 How SAS works

# 1.4 TIPS AND TRICKS FOR RUNNING SAS PROGRAMS

This section contains tips and tricks that can help you if something in your program goes wrong. Now you have seen two sample SAS jobs, you should have an idea of how SAS programs are constructed. This section provides general rules for writing SAS programs.
Within a SAS program, each statement begins with an identifying keyword (DATA, PROC, INPUT, DATALINES, RUN, etc.) and ends with a semicolon (;). For example:

```
DATA TEMP;
PROC PRINT DATA=TEMP;
```

SAS statements are free-format – they do not have to begin in any particular column. Thus.

+   - Statements can begin anywhere and anywhere. One statement can continue over several lines with a semicolon at the end of the last line signaling the end of the statement.
- Several statements may be on the same line, with each statement terminated with a semicolon.
- Blanks, as many as you want but at least one, may be used to separate the components (words) in a SAS program statement.
- Case (lower- and upper-) matters data and quoted information. When you enter character data values (such as M or m for “male”), case will matter when you are sorting or selecting the data. Moreover, the contents of a title or footnote are placed in quotation marks and are printed in the output using the uppercase and lowercase characters you indicate in the program code.