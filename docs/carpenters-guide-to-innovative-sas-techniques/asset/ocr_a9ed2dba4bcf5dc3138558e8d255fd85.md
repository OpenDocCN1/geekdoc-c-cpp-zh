# 7.1.2 GROUPINTERNAL Option

When a classification variable is associated with a format, that format is used in the formation of the groups. In the next example, the EDULEVEL format maps the years of education into levels of education.

```
title1 '7.1.2 CLASS Statement Options';
proc format;
    value edulevel
        0-12 = 'High School'
        13-16= 'College'
        17-high= 'Post Graduate';
    run;

title2 'GROUPINTERNAL not used';
proc summary data=advrpt.demo;
    class edu;
    var ht wt;
    output out=stats
        mean= MeanHT MeanWT
        ;
    format edu edulevel.;
    run;
proc print data=stats;
    run;
```

+   1. The EDULEVEL format maps years of education into three ranges.
+   
+   2. In the SUMMARY step the FORMAT statement has been used to create the association between EDU and the EDULEVEL format.
+   
+   3. The MISSING option has not been applied; consequently missing values of EDU will not be included in the summary.
+   
+   A PROC PRINT LISTING of the resulting data table shows that the SUMMARY procedure has used the format to collapse the individual levels of EDU into the three levels of the formatted classification variable.

| Obs | edu | _TYPE_ | _FREQ_ | MeanHT | MeanWT |
|---:|---|---:|---:|---:|---:|
| 1 | . | 0 | 76 | 67.5526 | 160.461 |
| 2 | High School | 1 | 30 | 68.6333 | 177.633 |
| 3 | College | 1 | 32 | 67.0938 | 147.438 |
| 4 | Post Graduate | 1 | 14 | 66.2857 | 153.429 |

To use the original data values (internal values) to form the groups, rather than the formatted values, the GROUPINTERNAL option is added to the CLASS statement. `class edu/groupinternal;`

| Obs | edu | _TYPE_ | _FREQ_ | MeanHT | MeanWT |
|---:|---|---:|---:|---:|---:|
| 1 | . | 0 | 76 | 67.5526 | 160.461 |
| 2 | High School | 1 | 11 | 71.3636 | 194.091 |
| 3 | High School | 1 | 19 | 67.0526 | 168.105 |
| 4 | College | 1 | 4 | 70.0000 | 197.000 |
| 5 | College | 1 | 11 | 64.1818 | 108.091 |
| 6 | College | 1 | 7 | 65.2857 | 155.571 |
| 7 | College | 1 | 10 | 70.4000 | 165.200 |
| 8 | Post Graduate | 1 | 10 | 65.2000 | 145.200 |
| 9 | Post Graduate | 1 | 4 | 69.0000 | 174.000 |

Notice that although the original values of EDU are used to form the groups, the formatted values are still displayed. In this example we could have achieved similar results by using the

ORDER=INTERNAL option shown in Section 7.1.3.