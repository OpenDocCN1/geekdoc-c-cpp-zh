# GOING DEEPER: MORE TECHNIQUES FOR ENTERING DATA

TABLE 2.16 Output from Reading CSV File with Problems
| Obs | LAST | FIRST | ID | ROLE |
| 1 | ABRAMS | JJ | C0001 | Producer |
| 2 | BRISTOW | SYDNEY | C0015 | VAUGH |
| 3 | FLINKMAN | MARSHALL | C0123 | SLOAN |

This statement tells you that there are different record lengths. To solve this,

+   3. Add the option TRUNCVER; to the end of the INFILE statement to it reads:

```
INFILE "C:\SASDATA\INFILATED.txt" TRUNCVER;
```

+   4. Resubmit the code and observe that the data are read correctly. The TRUNCVER option forces the INPUT to stop reading when it gets to the end of a short line. The results are shown in Table 2.17.

+   5. Change the input statement to

```
INFILE "C:\SASDATA\TESTDATA.TXT" LRECL=44 PAD;
```

Submit the code and observe the results. This also reads in the data correctly. The PAD option pads short lines with blanks to the length of the LRECL= option. Try running this code without PAD and observe the results.

+   6. Change the input statement to

```
INFILE "C:\SASDATA\TESTDATA.TXT" MISSOVER;
```

Submit the code and observe the results. The data are not read correctly. MISSOVER prevents SAS from going to a new input line if it does not find values for all the variables in the current line of data. Since TEACHER didn't fill out the entire space (i.e., had only 7 characters and ended on column 43), it was skipped.

TABLE 2.17 Output from Reading CSV Using TRUNCVER
| Obs | LAST | FIRST | ID | ROLE |
| 1 | ABRAMS | JJ | C0001 | Producer |
| 2 | BRISTOW | SYDNEY | C0015 | Teacher |
| 3 | VAUGHN | MICHAEL | C0033 | Agent |
| 4 | FLINKMAN | MARSHALL | C0123 | Analyst |
| 5 | SLOAN | ARVIN | C0666 | |
| 6 | BRISTOW | JACK | | |
| 7 | DIXON | MARCUS | C0233 | Chief |

(continued)