When working with values that are less than one be sure to force at least one significant digit by using the 9 as the placeholder in the format label.

Truncation is another area that warrants extra consideration when dealing with picture formats. Values that do not fit into the picture template (the format label) are truncated. The variable X in this example ranges from a small fraction to a value over one thousand.

```
```sas
proc format;
  picture showdec
    other = '09.00.'; ❶
  run;
data x; ❷
do x = .007,.017,.123,1.234, 12.345, 1234; ❸
  y=x;
  output;
end;
format y showdec. x 8.3; ❹
run;
```
```

❶ The format is defined with two decimal places and 9 in the unit's digit. Notice that the implied format used for X does not have sufficient range to display both the largest and smallest value. Something like the

12.2.2 Picture Formats Showing Decimals

| Obs | x | y |
| --- | --- | --- |
| 1 | 0.007 | 0.00 ❷ |
| 2 | 0.017 | 0.01 |
| 3 | 0.123 | 0.12 |
| 4 | 1.234 | 1.23 |
| 5 | 12.345 | 12.34 ❸ |
| 6 | 1234.000 | 34.00 ❹ |

format 8.3 would have had the range to show all the values.

+   - ❷ The value less than .01 (the smallest permitted by the format) is not surprisingly truncated.
+   - ❸ Only two of the three least significant digits can be displayed. The display value for X is rounded but for Y the thousandths are truncated.
+   - ❹ We have only allowed for values up to 99.99. Values over 100 have the most significant digits truncated.

The rounding and truncation issues can be addressed in the format definition. The SHOWDECR. format shown here allows both rounding and numbers up to 99999.99.

```
```sas
proc format;
  picture showdecr (round) ❼
    other = '00009.00.'; ❽
run;
```
```

❼ The ROUND option causes the format to round fractional values.

12.2.2 Working with Fractional Values
Showing Decimals

| Obs | x | y |
| --- | --- | --- |
| 1 | 0.007 | 0.01 |
| 2 | 0.017 | 0.02 |
| 3 | 0.123 | 0.12 |
| 4 | 1.234 | 1.23 |
| 5 | 12.345 | 12.35 |
| 6 | 1234.000 | 1234.00 |

❽ Be sure to include a sufficient number of placeholders to accommodate the largest number.

# ### 12.2.3 Using the MULT and PREFIX Options

While text that is to be included, either within or following the formatted value can be included as part of the picture definition, text that is to precede the display value is ignored. When you want preceding text to be a part of the displayed value, the PREFIX= option can be used.