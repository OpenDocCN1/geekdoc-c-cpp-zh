Since the C2FF() and F2CC() functions do not have more than one argument, they can be used directly in the label portion of a user-defined format. Although in this example the format name and the function name are the same, this is not in any way a requirement.

```
```sas
proc format;
    value c2ff (default=10)
        other=[c2ff()];
    value f2cc (default=10)
        other=[f2cc()];
run;

data null_;
    c=100; put c=c2ff.;
    f=212; put f=f2cc.;
run;
```
```

❼ When using a function in the label it is best to set the default display width.

❽ The function is called from within the label by enclosing it in square brackets.

❾ The format is requested on the PUT statement. This request results in the execution of the function, and generates this text in the LOG.

```
```text
c=212°F
f=100°C
```
```

The initial versions of these functions were written by Rick Langston, senior manager in software development at SAS.

# Return the Quarter without the Year (Qq instead of yyQq)

In Section 15.2.1 the QNUM() function is created to remove the year portion of the value that is returned by the YYQ. format. In that example a second DATA step was required before we could use the results of the function in a PROC FREQ step. By using that function in a format, we can use the format directly in the PROC step and thereby avoid an additional pass of the data.

```
```sas
proc format;
    value qfmt other=[qnum()];
run;

options cmplib=(advrpt.functions);
proc freq data=advrpt.lab_chemistry
    order=formatted;
    table visit*labdt;
    format labdt qfmt.;
run;
```
```

Here the QNUM() function is used in the format label. The format is then used in the PROC FREQ step. The elimination of steps will almost always improve processing efficiency.

### 12.5.5 Functions as Format Labels

**The FREQ Procedure**

| Frequency | Table of VISIT by LABDT |
|---|---|
| Percent | **LABDT (LAB TEST DATE)** |
| Row Pct | VISIT (VISIT NUMBER) | Q1 | Q2 | Q3 | Q4 | Total |
| Col Pct | 1 | 3 | 3 | 7 | 4 | 17 |
|  | 1.78 | 1.78 | 4.14 | 2.37 | 10.06 |
|  | 17.65 | 17.65 | 41.18 | 23.53 |  |
|  | 8.33 | 7.50 | 12.73 | 10.53 |  |
|  | 2 | 3 | 2 | 7 | 4 | 16 |
|  | 1.78 | 1.18 | 4.14 | 2.37 | 9.47 |
|  | 18.75 | 12.50 | 43.75 | 25.00 |  |
|  | 8.33 | 5.00 | 12.73 | 10.53 |  |