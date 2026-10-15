In Display 2.21, the *.csv file produced with ODS CSV and PROC PRINT with ID ANIMAL causes animal number to be a character variable in the *.csv file. (Notice the double quotation marks around the numbers 1 through 50.)

# Display 2.21 *.csv files produced by ODS CSV and PROC EXPORT

```
nitrofen.csv (from PROC PRINT with ODS CSV specified)
"animal","conc","total"
"1",0,27
"2",0,32
"3",0,34
...
"48",310,4
"49",310,6
"50",310,5

nitrofen2.csv (produced from PROC EXPORT via File > Export Data ...)
animal,conc,brood1,brood2,brood3,total
1,0,3,14,10,27
2,0,5,12,15,32
3,0,6,11,17,34
...
48,310,4,0,0,4
49,310,6,0,0,6
50,310,5,0,0,5
```

# 2.4 Concatenating Data Sets and Adding Observations

When creating an analysis data set, you might need to add new observations. In this situation, you have the same variables for different collections of observations. This task is shown in Display 2.22. In this illustration, a data set containing seven observations is supplemented by a data set containing five observations to produce a data set containing 12 observations.

# Display 2.22 Adding observations or rows—concatenating data sets

| Observation ID | Variable 1 | Variable 2 | Variable 3 |
|---|---|---|---|
| 1 |  |  |  |
| 2 |  |  |  |
| 3 |  |  |  |
| 4 |  |  |  |
| 5 |  |  |  |
| 6 |  |  |  |
| 7 |  |  |  |