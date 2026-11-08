
## 12.2.2 Picture Formats Showing Decimals

When working with values that are less than one, be sure to force at least one significant digit by using the 9 as the placeholder in the format label.

Truncation is another area that warrants extra consideration when dealing with picture formats. Values that do not fit into the picture template (the format label) are truncated. The variable X in this example ranges from a small fraction to a value over one thousand.

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

❶ The format is defined with two decimal places and 9 in the units digit. Notice that the implied format used for X does not have sufficient range to display both the largest and smallest value. Something like the format 8.3 would have had the range to show all the values.

| Obs | x | y |
| --- | --- | --- |
| 1 | 0.007 | 0.00 ❷ |
| 2 | 0.017 | 0.01 |
| 3 | 0.123 | 0.12 |
| 4 | 1.234 | 1.23 |
| 5 | 12.345 | 12.34 ❸ |
| 6 | 1234.000 | 34.00 ❹ |

- ❷ The value less than .01 (the smallest permitted by the format) is not surprisingly truncated.
- ❸ Only two of the three least significant digits can be displayed. The display value for X is rounded but for Y the thousandths are truncated.
- ❹ We have only allowed for values up to 99.99. Values over 100 have the most significant digits truncated.

The rounding and truncation issues can be addressed in the format definition. The SHOWDECR. format shown here allows both rounding and numbers up to 99999.99.

```sas
proc format;
  picture showdecr (round) ❼
    other = '00009.00.'; ❽
run;
```

❼ The ROUND option causes the format to round fractional values.

### 12.2.2 Working with Fractional Values Showing Decimals

| Obs | x | y |
| --- | --- | --- |
| 1 | 0.007 | 0.01 |
| 2 | 0.017 | 0.02 |
| 3 | 0.123 | 0.12 |
| 4 | 1.234 | 1.23 |
| 5 | 12.345 | 12.35 |
| 6 | 1234.000 | 1234.00 |

❽ Be sure to include a sufficient number of placeholders to accommodate the largest number.

## 12.2.3 Using the MULT and PREFIX Options

While text that is to be included, either within or following the formatted value can be included as part of the picture definition, text that is to precede the display value is ignored. When you want preceding text to be a part of the displayed value, the PREFIX= option can be used.

The MULT= option allows the application of a multiplier. This value is multiplied against the incoming value and the result is displayed.

A common alternative solution to handling fractional values involves the use of the MULT= and PREFIX= options.

```sas
proc format;
   picture showdec;
      0           = '9'
      0 < _ < .01 = '9'       (prefix='<.01')
      .01 - <1    = '99'      (prefix='0.' mult=100)
      other       = '00000.0';
run;
data x;
   do x = 0, .001, .012, .123, 1.234, 12.345, 1234;
      y=x;
      output;
   end;
   format y showdec.;
run;
```

- 1. The zero is handled separately.
- 2. Values that are smaller than .01 add a prefix value that includes the <.01 text.
- 3. For values from .01 up to 1, multiply the value by 100 and add the ‘0.’ prefix.

| Obs | x | y |
| ---: | ---: | ---: |
| 1 | 0.00 | 0 |
| 2 | 0.00 | <.01 |
| 3 | 0.01 | 0.01 |
| 4 | 0.12 | 0.12 |
| 5 | 1.23 | 1.23 |
| 6 | 12.35 | 12.34 |
| 7 | 1234.00 | 1234.00 |

- 4. Make sure that there are sufficient significant digits.
- 5. Since we did not use the (ROUND) option this value has been truncated.

Since the numbers in this example have two decimal places, multiplying them by 100 (10^n where n is the number of significant digits to be displayed) turns the number into an integer. The decimal is then inserted via the picture format.

In the following example dollars are being converted to British pounds (the conversion constant used for this example is 0.635, which is almost certainly not the current currency conversion constant).

```sas
title2 'Using the MULT and PREFIX options';
proc format;
   picture pounds
      1 - 10   = '9,00'   (mult=63.5  prefix='£');
      10< - 100 = '9,0'    (mult=6.35  prefix='£');
      100< - high = '000.00' (mult=.635 prefix='£');
run;

data money;
   do dollars = 1.23, 12.3, 123, 1230, 12300;
      pounds = dollars;
      output;
   end;
   format dollars dollar10.2 pounds pounds.;
run;

proc print data=money;
   run;
```

- 6. The display value template specifies two decimal places (using the European style with a comma separating the whole numbers from the fractions).
- 7. The multiplication factor is specified using the MULT= option.
- 8. The PREFIX= option is used to designate one or more leading symbols.

Here the option is applied to each value/label pair; however, it does not need to be constant, as it is in this example.

### 12.2.3a Picture Formats Using the MULT and PREFIX Options

| Obs | dollars | pounds |
| --- | --- | --- |
| 1 | $1.23 | £0,78 |
| 2 | $12.30 | £7,8 |
| 3 | $123.00 | £78 |
| 4 | $1,230.00 | £781 |
| 5 | $12,300.00 | £7.810 |

❶ The multiplication factor changes to accommodate the number of decimal places.

The symbol for pounds, £, which was used in this example, does not appear on most US keyboards. Since special characters such as this one exist in most fonts, utilizing them in SAS is fairly straightforward. From your word processor insert the character or symbol of choice into a document. From the document, copy it and then paste it into the SAS editor, where it can now be used in your code.

In the following expansion of the POUNDS. format, we allow for the inclusion of negative values as well as values between 0 and 1.

```sas
picture pounds
  -1 - <0 = '99' (mult=63.5 prefix='£-0,') ❷
   0   = '9'  (prefix='£')
  0 < - <1 = '99'  (mult=63.5 prefix='£0,')
  1   - 10 = '9,00'(mult=63.5 prefix='£')
 10< - 100 = '99,0'(mult=6.35 prefix='£')
100< - high= '000.000.000' (mult=.635 prefix='£');
```

❷ Because the absolute value is taken on mapped values, the minus sign must also be added as a prefix character.

### 12.2.3b Using the PREFIX and MULT Options Including Negative Values

| Obs | dollars | pounds |
| --- | --- | --- |
| 1 | $-0.12 | £-0,07 |
| 2 | $0.00 | £0 |
| 3 | $0.12 | £0,07 |
| 4 | $1.00 | £0,63 |
| 5 | $1.23 | £0,78 |
| 6 | $12.30 | £07,8 |
| 7 | $123.00 | £78 |
| 8 | $1,230.00 | £781 |
| 9 | $12,300.00 | £7.810 |

SEE ALSO

Chapman (2003) has a number of examples of PICTURE formats that use the MULT= option.

## 12.2.4 Display Granularity Based on Value Ranges – Limiting Significant Digits

Sometimes we want the precision of the displayed value to self-adjust as the size of the numbers change. This was shown, but not really commented on, in the examples in the previous section. In the following example we want to limit the displayed value to no more than 6 digits; however, the values themselves range from 0 to billions.

```sas
title2 'Limiting Significant Digits';
proc format;
   picture Tons
      other = '9'
      0< -    <1 = '99' (prefix='0.' mult=100)
      1 - <10 = '9.99'
      10 - <1000 = '000.9'
      1000 - <1e06 = '000,000' ❶
      1e06 - <1e09 = '000.999M' ❷ (mult=1e-03) ❸
      1e09 - <1e12 = '000.999B' ❹ (mult=1e-06);
run;

data imports;
   do tons = 0, .15, 1.5,1.5e2, 1.5e4, 1.5e7, 1.5e10;
      fmttons = tons;
      output;
   end;
   format fmttons tons.;
   run;
proc print data=imports;
   run;
```

- ❶ Values between 1000 and 1,000,000 (1e6) are shown without any decimal places.
- ❷ For values in the millions, an ‘M’ is displayed following the 6 most significant digits.
- ❸ We have shifted the decimal six places; however, only three have been lost.
- ❹ The decimal shift is now 9 digits and of these only three are shown before the decimal point. The multiplication factor is therefore 1e-06.

| Obs | tons | fmttons |
| ---: | ---: | ---: |
| 1 | 0.00 | 0 |
| 2 | 0.15 | 0.15 |
| 3 | 1.50 | 1.50 |
| 4 | 150.00 | 150.0 |
| 5 | 15000.00 | 15.000 |
| 6 | 15000000.00 | 15.000M |
| 7 | 15000000000.00 | 15.000B |

This type of format can be especially useful on graphs where we need to control the width of the tick mark values on the axis.

## 12.3 Multilabel (MLF) Formats

When creating formats, overlapping format ranges are generally not allowed. Multilabel formats overcome this limitation; however, only selected procedures are able to utilize this special type of format. Multilabel formats are created using the MULTILABEL option on the VALUE statement.

### 12.3.1 A Simple MLF

In the following example we summarize the years of education into high school and college. At the same time we want to see the graduate school subset of those attending college. This can easily be accomplished using a multilabel format.
