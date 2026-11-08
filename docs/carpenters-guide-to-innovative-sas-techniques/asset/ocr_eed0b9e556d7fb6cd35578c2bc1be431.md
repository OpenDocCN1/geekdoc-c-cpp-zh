# Numeric BY Variables

Extreme care must be taken if you ever need to use numeric BY variables, especially variables with non-integer values. Because of the way that numbers are stored within the computer, even numbers that appear to be integers may not actually be integers. This can be simply demonstrated by creating a value that is slightly different from 1.

```
data similar;
x = 1;
y = 3.00000000000001/3;
if x=y then put 'the same';
put x= best32.;
put y= best32.;
put x= hex16.;
put y= hex16.;
run;
```

```
x=1
y=1
x=3FF0000000000000
y=3FF0000000000001
```

Examining the LOG shows that even the BEST32. format displays this value (Y=) as 1. The HEX16. format does show these two numbers

differently, but really how often would you use the HEX format to double-check the integers? Worse if we were to use this variable as a BY variable is as done next, the difference is sufficient to sabotage the merge. The LOG shows that the data set BOTH has two observations—one for each value of Y, where there would only have been one observation if the values were seen as equal.

```
data other;
y=1; a='a';
run;
data both;
merge similar
      other;
by y;
run;
```

```
NOTE: There were 1 observations read from the data set
WORK.SIMILAR.
NOTE: There were 1 observations read from the data set WORK.OTHER.
NOTE: The data set WORK.BOTH has 2 observations and 3 variables.
```

At some point the fuzz rules come into play and the difference is so small that SAS considers them to be equal. In this example adding one more zero to the number of decimal places in the first definition of Y would have been sufficient for the merge to have been successful.

The take-away point is, be very careful when using numeric BY variables in a merge.

# SEE ALSO

Ron Cody wrote Sample Note 33-407 on issues associated with variable attribute inconsistencies, and suggests an automated solution http://support.sas.com/kb/33/407.html .

# 3.7.2 Variables in Common That Are Not in the BY List

After a merge or join, variables common to more than one data set will appear only once in the new data set. This means that there can be variables that overwrite each other.

In the following example we merge two data sets by SUBJECT. Each also contains the variable DATE; however, DATE is not included on the BY statement. In order to make the example a bit easier to follow the SORT steps have used the NODUPKEY option so that each SUBJECT appears only once.