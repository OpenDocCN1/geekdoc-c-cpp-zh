# Display 3.2 (Edited) Output produced by PROC PRINT

The SAS System    09:21 Sunday, November 8, 2009    1
Obs   X    Y
1     1    5.7549
2     2    6.5498
3     3    8.8338
4     4    11.0139
5     5    12.8750
6     6    14.7235
7     7    16.8983
8     8    18.6677
9     9    20.8039
10    10   22.0728

The output is centered by default. In addition, the date and page number are stamped in the upper right corner of this output. You can change this by adding the following OPTIONS statement:

```
options nocenter nodate;
```

The output is shown in Display 3.3.

# Display 3.3 Modifying the output with NOCENTER and NODATE options

```
options nocenter nodate;
* generate a 10 observation data set with Y~N(3+2x,0.5^2);
data test;
call streaminit(0);
do X=1 to 10;
    Y=3+2*X+0.5* RAND('NORMAL');
    output;
end;
run;

proc print data=test;
run;
```

The NOCENTER option left justifies the output as shown in Display 3.4, while the NODATE option suppresses the printing of the date.