You might be interested in attaching formats to the values of variables. Assigning formats is discussed in detail in Chapter 8, but a few basic uses of formats are discussed in this chapter. Formats can be attached to variables using an assignment in a DATA step. Or, they can be temporarily attached to a variable using a statement in a PROC. Attaching formats to variables is shown in Display 3.7.

The variable Y is defined with a FORMAT statement as part of the data block. The assigned format —dollar6.2— displays the values of Y as currency with a $ sign attached. The 6.2 in the format says that six total spaces are allocated for the output (including the $ sign and decimal point) with two digits to the right of the decimal point. (More discussion about formats follows in later chapters. However, this chapter gives you a taste of using formats.) This assigned format affects any procedure that references Y in this data set. In contrast, an assigned format is defined for variable X in the second PROC PRINT. When the format is assigned in the procedure, it operates for the duration of that procedure and not beyond. Titles are placed in the output using the TITLE and TITLE2 statements. Titles appear on every output page until they are reset. Up to 10 titles can appear on an output page. While TITLE specifies the first title line for the output, the statement TITLEn specifies the nth title line (n=2,...,10). More than three title lines (give or take) might limit the actual output on a page. Lines can be added to the bottom of each page of output by using the FOOTNOTEn option. This parallels TITLEn, with the exception that you are specifying text to include at the foot of each page.

# Display 3.7 Code with a few formatting options

```
options formdlim='=' pageno=1 ls=64 nocenter nodate;
data dl;
  input x y @@;
  format y dollar6.2;
  datalines;
1 2 4 3 5 6 12345 123456
;
run;

proc print data=dl;
  title "Y formatted in DATA";
run;

proc print data=dl;
  title2 "X now formatted in the 2nd PROC PRINT";
  format x dollar12.2;
run;

proc print data=dl;
  title2;
run;
```