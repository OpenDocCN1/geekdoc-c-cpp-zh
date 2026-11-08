
June 7, 2009 was a Sunday and since a week interval starts on a Sunday, each of these uses of the INTNX function advances the date to a Sunday. Clearly interval multipliers change the way the function views the start of the interval.

### 3.4.1 Interval Multipliers

| Obs | visdt | examdt_2 | examdt x2 |
| --- | --- | --- | --- |
| 1 | 25MAY2009 | 07JUN2009 | 07JUN2009 |
| 2 | 26MAY2009 | 07JUN2009 | 07JUN2009 |
| 3 | 27MAY2009 | 07JUN2009 | 07JUN2009 |
| 4 | 28MAY2009 | 07JUN2009 | 07JUN2009 |
| 5 | 29MAY2009 | 07JUN2009 | 07JUN2009 |
| 6 | 30MAY2009 | 07JUN2009 | 07JUN2009 |
| 7 | 31MAY2009 | 07JUN2009 | 14JUN2009 |
| 8 | 01JUN2009 | 07JUN2009 | 14JUN2009 |
| 9 | 02JUN2009 | 07JUN2009 | 14JUN2009 |
| 10 | 03JUN2009 | 07JUN2009 | 14JUN2009 |
| 11 | 04JUN2009 | 07JUN2009 | 14JUN2009 |
| 12 | 05JUN2009 | 07JUN2009 | 14JUN2009 |
| 13 | 06JUN2009 | 07JUN2009 | 14JUN2009 |
| 14 | 07JUN2009 | 21JUN2009 | 21JUN2009 |
| 15 | 08JUN2009 | 21JUN2009 | 21JUN2009 |
| 16 | 09JUN2009 | 21JUN2009 | 21JUN2009 |
| 17 | 10JUN2009 | 21JUN2009 | 21JUN2009 |
| 18 | 11JUN2009 | 21JUN2009 | 21JUN2009 |
| 19 | 12JUN2009 | 21JUN2009 | 21JUN2009 |
| 20 | 13JUN2009 | 21JUN2009 | 21JUN2009 |
| 21 | 14JUN2009 | 21JUN2009 | 28JUN2009 |

When an interval is expanded the new interval start date will relate back to the beginning of time (January 1, 1960). May 24th was a Sunday and it started both the WEEK and WEEK2 interval. May 25, therefore, was advanced to June 7 for both interval types. May 31st (also a Sunday), however, did NOT start a WEEK2 interval, but it did start a WEEK interval. Consequently these two INTNX functions give different results when based on dates in the range of May 31 to June 6, 2009 (Obs=7–13).

If we use an interval multiplier to create a three-year interval (YEAR3), the interval start date would be determined based on the first three-year interval, which would start on January 1, 1960.

### MORE INFORMATION

Alignment options are available for the INTNX function that can be helpful when the start of the interval that you are measuring from is not what you want. See Section 3.4.3.

### 3.4.2 Shift Operators

Both the INTNX and INTCK functions by default measure from the start of the base interval. Weeks start on Sunday, years start on January 1st, and so on. Shift operators can be used to change the way that the function determines the start of the interval. A week could start on Monday, or a fiscal year could start on July 1st.

The shift operator is designated by a number following a decimal point at the end of the interval name. The units of the shift depend on how the interval is defined. Weeks contain seven days and start on Sunday, which has the value of 1. The interval WEEK.2, therefore, would indicate a seven day week that starts on a Monday. The following example shows a series of shifts on a week interval (June 7, 2009 was a Sunday).

```sas
data ExamSchedule;
   do visdt = '01Jun2009'd to '15Jun2009'd;
      day = intnx('week',visdt,1);
      day1 = intnx('week.1',visdt,1);
      day2 = intnx('week.2',visdt,1);
      day3 = intnx('week.3',visdt,1);
      day4 = intnx('week.4',visdt,1);
      day5 = intnx('week.5',visdt,1);
      day6 = intnx('week.6',visdt,1);
      day7 = intnx('week.7',visdt,1);
      output;
   end;
   format visdt day: date7.;
run;
```

The WEEK interval starts on a Sunday and WEEK.1 does not change the interval start. WEEK.2, however, will change the start to a Monday.

Using a PROC PRINT on the resulting data set shows how the dates progress. More importantly, it shows us that the date is reset to the start of the adjusted interval first and then advanced 7 days. ❶ In the LISTING output below, notice the values based on the VISDT of Wednesday, June 3, 2009. DAY4 is advanced to June 10th (DAY4 was defined using WEEK.4, which is an interval starting on a Wednesday), so advancing 7 days yields June 10th. For DAY5 (WEEK.5 defines a week starting on Thursday), on the other hand, Wednesday is at the end of the interval and the measurement is taken from the previous Thursday (May 29).

| visdt | day | day1 | day2 | day3 | day4 | day5 | day6 | day7 |
|---|---|---|---|---|---|---|---|---|
| 01JUN09 | 07JUN09 | 07JUN09 | 08JUN09 | 02JUN09 | 03JUN09 | 04JUN09 | 05JUN09 | 06JUN09 |
| 02JUN09 | 07JUN09 | 07JUN09 | 08JUN09 | 09JUN09 | 03JUN09 | 04JUN09 | 05JUN09 | 06JUN09 |
| **03JUN09** | **07JUN09** | **07JUN09** | **08JUN09** | **09JUN09** | **10JUN09** | **04JUN09** | **05JUN09** | **06JUN09** |
| 04JUN09 | 07JUN09 | 07JUN09 | 08JUN09 | 09JUN09 | 10JUN09 | 11JUN09 | 05JUN09 | 06JUN09 |
| 05JUN09 | 07JUN09 | 07JUN09 | 08JUN09 | 09JUN09 | 10JUN09 | 11JUN09 | 12JUN09 | 06JUN09 |
| 06JUN09 | 07JUN09 | 07JUN09 | 08JUN09 | 09JUN09 | 10JUN09 | 11JUN09 | 12JUN09 | 13JUN09 |

*... portions of the listing are not shown ...*

A typical use of a shift operator is to create a fiscal year with the interval start on July 1. Since years are made up of months, the interval `YEAR.7` would shift the start of the year by seven months. Interval multipliers and shift operators can be used together. A five-year interval starting on July 1st could be specified as `YEAR5.7`.

### 3.4.3 Alignment Options

Although alignment options are now available for both INTNX and INTCK, they are not the same for the two functions.

**Alignment with the INTNX Function**

Since it is not always convenient to advance values based on the start of the interval, as was done in Sections 3.4.1 and 3.4.2, the INTNX function has the ability to change this behavior through alignment options. These options may be specified as an optional fourth argument, which can change how the function offsets from the interval start point. Without using the alignment options all displacements are measured from the start of the interval:

```sas
new = intnx('year','03jun2000'd,1);
```

consequently, if we advance a date by one year from June 3, 2000 the resulting date is January 1, 2001. Alignment options allow us to measure the displacement other than from the start of the interval.

The alignment option on the INTCK function has two settings:

- C continuous
- D discrete (this is the default)

The difference between these two option values can be demonstrated by counting the intervals between two dates. In this example the number of intervals (weeks) between the base date (START), which is fixed at Wednesday, September 14, 2011, and END which is a date that advances up to a month beyond START.

```sas
data check;
    start = '14sep2011'd; /* the 14th was a Wednesday;
    do end = start to intnx('month',start,1,'s');
        weeks = intck('weeks',start,end);
        weeksc = intck('weeks',start,end,'c');
        weeksd = intck('weeks',start,end,'d');
        output check;
    end;
format start end date9.;
run;
```

The resulting data set contains the number of elapsed weeks as calculated by the INTCK function using the alignment option. The variables WEEKS and WEEKSD are both incremented each time the interval boundary is crossed (Sunday – 18 and 25 September). However, the continuous alignment option causes WEEKSC to be incremented only when a full interval has elapsed—the interval boundary has effectively been adjusted to start at the date that starts the interval.

| Obs | start      | end        | weeks | weeksc | weeksd |
|---:|------------|------------|-----:|-------:|-------:|
| 1  | 14SEP2011  | 14SEP2011  | 0 | 0 | 0 |
| 2  | 14SEP2011  | 15SEP2011  | 0 | 0 | 0 |
| 3  | 14SEP2011  | 16SEP2011  | 0 | 0 | 0 |
| 4  | 14SEP2011  | 17SEP2011  | 0 | 0 | 0 |
| 5  | 14SEP2011  | 18SEP2011  | 1 | 0 | 1 |
| 6  | 14SEP2011  | 19SEP2011  | 1 | 0 | 1 |
| 7  | 14SEP2011  | 20SEP2011  | 1 | 0 | 1 |
| 8  | 14SEP2011  | 21SEP2011  | 1 | 1 | 1 |
| 9  | 14SEP2011  | 22SEP2011  | 1 | 1 | 1 |
| 10 | 14SEP2011  | 23SEP2011  | 1 | 1 | 1 |
| 11 | 14SEP2011  | 24SEP2011  | 1 | 1 | 1 |
| 12 | 14SEP2011  | 25SEP2011  | 2 | 1 | 2 |

*... portions of the listing are not shown ...*

### 3.4.4 Automatic Dates

Although the INTNX function is designed to advance a date or time value, it can be used in a number of other situations where its immediate application is not as obvious.

### Collapsing Dates

The INTNX function can be used to collapse a series of dates into a single date, thus allowing the new date to be used as a classification variable. When a format is available, most procedures can use the formatted value to form groups (ORDER=FORMATTED; see Section 2.6.2). However, when a format is not available the INTNX function can be used as an alternative.

To collapse dates we take advantage of the characteristic of the function that adjusts dates to the start of the interval (or the middle or end using the alignment option).

```sas
hourgrp = intnx('hour',datetime,0);
```

```sas
twohr = intnx('hour2',datetime,0);
```

If we advance each date by 0 intervals the dates are collapsed into a single date. In the manufacturing data (ADVRPT.MFGDATA) items are being built continuously with the manufacturing
