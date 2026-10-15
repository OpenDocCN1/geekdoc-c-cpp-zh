# Display 8.32 (continued)

```
* generate N1 observations ~ N(mu_1, sig_1^2);
do ix = 1 to N1;
    group = 1;
    Y = RAND('normal',mu_1,sig_1);
    output;
end;

* generate N2 observations ~ N(mu_2, sig_2^2);
do ix = 1 to N2;
    group = 2;
    Y = RAND('normal',mu_2,sig_2);
    output;
end;

end;  * of the do-loop over simulated experiments;
run;

/* calculate the test statistic */
ods rtf file="C:\Users\baileraj.IT\Desktop\Display-8-33.rtf";
ods trace on/listing;
proc ttest data=simulate_2group_t;
    by iexpt;
    class group;
    var Y;
run;
ods trace off;
ods rtf close;
```

The output objects from the ODS TRACE of PROC TTEST are listed in Display 8.33.

# Display 8.33 ODS TRACE listing of output objects and PROC TTEST output

Output Added:
-------------
Name:        Statistics
Label:       Statistics
Template:    Stat.TTest.Statistics
Path:        Ttest.ByGroup1.Y.Statistics
-------------

| group | N | Mean | Std Dev | Std Err | Minimum | Maximum |
|---|---|---|---|---|---|---|
| 1 | 10 | -0.2653 | 1.4593 | 0.4615 | -2.8812 | 1.4800 |
| 2 | 10 | 0.4281 | 0.8525 | 0.2696 | -0.7776 | 1.8097 |
| Diff (1-2) |  | -0.6934 | 1.1951 | 0.5344 |  |  |