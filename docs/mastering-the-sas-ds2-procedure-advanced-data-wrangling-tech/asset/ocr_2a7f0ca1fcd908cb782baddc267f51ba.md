# Mastering the SAS DS2 Procedure: Advanced Data Wrangling Techniques

#  3.2.3.2 UPDATE AND MODIFY STATEMENTS

DS2 includes neither an UPDATE nor a MODIFY statement. You can produce the same effects with a little additional coding using the SQLSTMT package. We'll show you more about that when we discuss predefined packages in Chapter 5.

#  3.2.3.3 ATTRIB, LABEL, LENGTH, FORMAT, AND INFORMAT Statements

Although DS2 does not include ATTRIB, LABEL, LENGTH, FORMAT, and INFORMAT statements, the same functionality is provided by the DECLARE package statement HAVING clause. Because each of those statements had their own syntax, I consider it a great benefit to have only one statement to accomplish all of these things!

```
data testl;
  length A $;
  attrib A=$UPCASE4;
  format B comma10.2;
  label A='Text (Test1)' B='Number (Test1)';
  a='xx';
  b=10000.00000;
run;

proc ds2;
  data test2 /overwrite=yes;
  dcl char(2) having $upcase4.label 'Text (Test2)';
  dcl double B having format comma10.2 label 'Number (Test2)';
  method run();
    a='xx';
    b=10000.00000;
  end;
enddata;
run;
quit;
```

Figure 3.3: Specifying Formats and Labels with the DECLARE Statement HAVING Clause

| Text (Test1) | Number (Test1) | Text (Test2) | Number (Test2) |
|---|---|---|--|
| XX | 10,000.00 | XX | 10,000.00 |

#  3.2.3.4 ARRAY Statement

I was also distressed to find that DS2 did not include an ARRAY statement. However, if you think about the DATA step ARRAY statement, you can clearly see that, in the traditional SAS DATA step, the ARRAY statement is used to produce two different types of array: an array with elements that reference variables in the PDV and a _TEMPORARY_ array with elements stored in memory and not associated variables. DS2 also provides both of these array types, but they are produced with different statements. Temporary arrays are created with a DECLARE statement. Arrays with elements that reference PDV variables are created with the VARARRAY statement.

```
data testl;
  array N [5];
  array C [5] $1 _temporary_;
  do i=1 to dim(n);
```