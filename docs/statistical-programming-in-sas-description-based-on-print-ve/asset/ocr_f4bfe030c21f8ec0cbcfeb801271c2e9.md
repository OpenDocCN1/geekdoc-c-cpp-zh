The printout from Display 9.2 includes the following output lines:

```
Recoding missing values using arrays and DO loop
Obs    t1    t2    t3    t4    t5    time6    time_7    ielement
1      6     6     5     5     5     4        3         8
2      7     .     4     4     3     .        2         8
```

Notice the index variable ielement in the output data set. The value of this index, 8, is beyond the looping range, which is when the looping stops for each observation. You can eliminate the index variable from an output data set by using a DROP statement. (For example, insert a drop ielement statement before the datalines statement in the previous code). The list of variables included in an array can be implicitly defined as all numeric variables, all character variables, or all variables using the _NUMERIC_, _CHARACTER_, and _ALL_ options, respectively. The following example illustrates the power of this construction.

# 9.1.4 Recoding missing values for all numeric and character variables

Suppose the ADL data set included character variables for the name and sex of the resident and the seven ADL measurements recorded over time. The following program groups all of the numeric variables into an array named num_array. It groups all of the character variables into an array named char_array. The program loops over each array to change all missing values to . for the numeric variables, and to change all missing values to a blank space for the character variables. The dim function determines the number of elements in each array for the looping. The program is shown in Display 9.3.

# Display 9.3 Recoding missing values in numeric and character variables

```
data D5;
    input name $ sex $ t1 t2 t3 t4 t5 time6 time_7;

ARRAY num_array{*} _NUMERIC_;
ARRAY char_array{*} _CHARACTER_;

/* recode the numeric variables */
DO inum = 1 to dim(num_array);
    if num_array{inum}==-999 then num_array{inum}=.;
END;

/* recode the character variables */
Do ichar = 1 to dim(char_array);
```