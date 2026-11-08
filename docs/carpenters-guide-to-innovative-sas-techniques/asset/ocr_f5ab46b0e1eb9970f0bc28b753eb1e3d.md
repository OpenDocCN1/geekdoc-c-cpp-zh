**4.4a Showing SORT Metadata**

**The CONTENTS Procedure**

| Property | Value | Property | Value |
|---|---|---|---|
| Data Set Name | WORK.LAB_CHEM | Observations | 165 |
| Member Type | DATA | Variables | 6 |
| Engine | V9 | Indexes | 0 |
| Created | Thu, Nov 05, 2009 02:26:48 PM | Observation Length | 56 |
| Last Modified | Thu, Nov 05, 2009 02:26:48 PM | Deleted Observations | 0 |
| Protection |  | Compressed | NO |
| Data Set Type |  | Sorted | **YES** ❶ |

When the SORTED flag ❶ contains YES, indicating that the data are sorted, an additional section is added to the PROC CONTENTS output. This section lets us know more about the conditions of the sort, and the include the BY variables ❷ and sort options ❹.

| Sort Information |
|---|
| **Sortedby** SUBJECT VISIT LABDT ❷ |
| **Validated** YES ❸ |
| **Character Set** ANSI |
| **Sort Option** NODUPREC ❹ |

❸ When SAS does the sorting the VALIDATED flag is set to YES.

# The SORTEDBY Data Set Option

When the data are already sorted, but not by SAS, the SORTED metadata flag will not be changed to YES, and we can miss out on performance enhancements that take advantage of known sort order. We can let SAS know that the data are actually sorted by setting the SORTED flag set to YES. You can set the SORTED metadata indicator flag directly by using the SORTEDBY data set option.

```
title1 '4.4b Using the SORTEDBY Option';
data lab2(sortedby=subject visit);
    set lab_chem;
    run;
proc contents data=lab2;
    run;
```

| Sort Information |
|---|
| **Sortedby** SUBJECT VISIT |
| **Validated** NO ❺ |
| **Character Set** ANSI |

Not only is the SORTED flag set to YES, but the sort information section is also completed. Notice, however, that the VALIDATED indicator is still set to NO ❺. We are trusted, but only trusted so far.

# 4.5 Using Threads

Some operations within a computer are computationally intensive. This is especially true for sorting operations and also for the calculation of large numbers of summary statistics. When multiple CPUs are available, some procedures will follow the principle of ‘divide and conquer,’ and they can split up computationally challenging tasks by spreading the work out among the available CPUs. This distributed work load can offer substantial improvements in the elapsed time to complete tasks.