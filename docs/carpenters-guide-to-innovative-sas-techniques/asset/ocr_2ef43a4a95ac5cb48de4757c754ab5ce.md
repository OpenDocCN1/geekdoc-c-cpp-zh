# 12.4  Controlling Order Using the NOTSORTED Option

Normally when a user-defined format is created, the format is internally placed into sorted order. Consequently it does not particularly matter what order the value/label pairings are specified in the value statement. However, this reordering can be prevented by using the NOTSORTED option on the VALUE statement ❶. When applied, the internal order of the format remains as it is defined. When an ORDER=FORMATTED option is applied to a format that is created using the NOTSORTED option, the order of the pairings in the format definition is used.

In the PROC TABULATE example in Section 12.3 ‘College’ appears first because it is first alphabetically. Here the format is created using the NOTSORTED option. Since the level for ‘High School’ is listed first in the following PROC FORMAT, ‘High School’ will appear before ‘College’ in the report.

```
```sas
proc format;
    value edlevel (notsorted) ❶
        9-12 = 'High School'
        13-high='College';
    run;

proc tabulate data=advrpt.demog;
    class edu sex;
    var wt;
    table edu all,
        sex*wt*(n*f=2. mean*f=5.1 stderr*f=6.2);
    format edu edlevel.; ❷
    run;
```
```

+   ❶ When the NOTSORTED option is used on the VALUE statement, the order that the item pairs are defined in the VALUE statement is preserved.
+   
+   ❷ The format is used as usual.

# CAVEAT

When a format is created it is optimized internally to make the assignment process as efficient as possible. Using the NOTSORTED option negates some of that optimization; however, for formats with fewer than a dozen or so value pairs it generally makes little practical difference. For very large formats (hundreds or thousands of items) there may be some performance access issues when using the NOTSORTED option. Be sure to experiment with your data and OS when using this option for larger formats.

**12.4 Formats Defined with NOTSORTED**

| years of education | patient sex |  |  |  |  |  |
|---|---|---|---|---|---|---|
|  | **F** |  |  | **M** |  |  |
|  | **weight in pounds** |  |  | **weight in pounds** |  |  |
|  | N | Mean | StdErr | N | Mean | StdErr |
| High School | 8 | 152.0 | 9.71 | 22 | 187.0 | 4.59 |
| College | 23 | 142.0 | 7.02 | 23 | 156.6 | 6.96 |
| All | 31 | 144.5 | 5.76 | 45 | 171.4 | 4.75 |