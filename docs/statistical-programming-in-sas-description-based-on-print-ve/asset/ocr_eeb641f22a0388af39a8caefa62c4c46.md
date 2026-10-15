NOTE: The data set WORK.IN_BOTH has 3 observations and 15 variables.

```
...
237 data in_weather;  * city in weather2 data set;
238    set in_either;
239    if weather2_in=1;
240 run;
...
```

NOTE: There were 5 observations read from the data set WORK.IN_EITHER.
NOTE: The data set WORK.IN_WEATHER has 4 observations and 15 variables.

```
242 data in_demog;  * city in demog2 data set;
243    set in_either;
244    if demog2_in=1;
245 run;
```

NOTE: There were 5 observations read from the data set WORK.IN_EITHER.
NOTE: The data set WORK.IN_DEMOG has 4 observations and 15 variables.

Key features of this program are denoted by *** comment #.

# *** comment 0

Denotes options that suppress date and page number information that is included by default in SAS output.

# *** comment 1

Denotes data sets that need to be sorted by the variable that will be used in the merge operation. In this example, the CITY variable matches observations to be merged.

# *** comment 2

The parenthetical statement (in=in1) defines an indicator variable in1 that identifies that a particular city is in the weather2 data set. The variable in1 is available for use in this DATA step. However, it needs to be assigned to a different variable to be used in other steps. Here, the in1 variable is assigned to the variable weather2_in. The default behavior of a merge operation is equivalent to the observation being in either or both data sets. In equivalent SAS code,

```
if weather2_in=1 OR demog2_in=1;
```

# *** comment 3

Denotes that if the contents of the merged data set contain cities in either the weather or demography data set, then the cities are assigned to the in both data set.

# *** comment 4

Denotes that a subsetting IF statement is used to select observations that are in both the weather and the demography data sets.