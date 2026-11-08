
We want to calculate the mean number of days for each subject, and FIRST.SUBJECT is used to

```sas
data labvisits(keep=subject count meanlength);
    set advrpt.lab_chemistry;
    by subject;

    array vdate (16) _temporary_;
    retain totaldays count 0;

    if first.subject then do;
       totaldays=0;
       count = 0;
       do i = 1 to 16;
          vdate(i)=.;
       end;
    end;
    vdate(visit) = labdt;
    if last.subject then do;
       do i = 1 to 15;
          between = vdate(i+1)-vdate(i);
          if between ne . then do;
             totaldays = totaldays+between;
             count = count+1;
          end;
       end;
       meanlength = totaldays/count;
       output;
    end;
run;
```

detect the initial observation for each subject ❷. This allows us to initialize the array and other variables used to generate the statistics of interest.

❸ The visit number provides the index to the array and the date itself (LABDT) is loaded into the array.

Once all the visits for this subject have been loaded into the array (LAST.SUBJECT=1) ❹, we can process across the array in whatever ways we need to solve the problem at hand. In this case we are interested in determining the number of days between any two nominal visit dates. This difference is calculated ❺ and summed ❻ so that the mean number of days between visits can be determined ❼.

This solution only considers intervals between nominal visits and not between actual visits. If a subject missed visit three, the intervals between visit two and visit four would not be calculated (both are missing and do not contribute to the number of intervals because visit 3 was missed). The change to the program to use all intervals based on actual dates is simple because all the visit dates are already in the array. Although not shown here, the alternate DATA step is included in the sample code for this section.

The beauty of this solution is that arrays are expandable and process very quickly. Arrays of thousands of values are both common and reasonable.

When processing arrays, as was done here, it is often necessary to clear the array when crossing boundary conditions ❷. In this example a loop was used to set each value to missing and an alternate technique would be to avoid the DO loop by taking advantage of the CALL MISSING routine.

```sas
do i = 1 to 16;
    vdate(i)=.;
end;
```

```sas
call missing(of vdate(*));
```

## 3.1.3 Using the LAG Function

The LAG function can be used to track values of a variable from previous observations. This is known as a look-back read. Effectively the LAG function retains values from one observation to the next. The function itself is executable and values are loaded into memory when the function is executed. This has caused users some confusion. In the following example the statement `lagvisit= lag(visit);` ❷ loads the current value of VISIT into memory where it is held, along with the value from the previous observation. Whenever the variable LAGVISIT is used in an expression, the value of VISIT from the previous observation is returned. Because the current value must be loaded for each observation, the LAG function must be executed for each observation. When the LAG function is conditionally executed with an IF statement or inside of a conditionally executed DO block, the LAG function may not return what you expect.

The following example uses the LAG function to determine the number of days since the previous visit.

```sas
data labvisits(keep=subject visit lagvisit interval lagdate labdt);
    set labdates;
    by subject;

    lagvisit = lag(visit);
    lagdate = lag(labdt);

    if not first.subject then do;
        interval = labdt - lagdate;
        if interval ne . then output;
    end;
    format lagdate mmddyy10.;
    run;
```

The data are sorted and the BY statement is used to establish the FIRST.SUBJECT temporary variable. The LAG function is used to save the value of the VISIT and LAGDATE variables. The first observation for each subject is used to establish a base visit date and the remaining observations are used to calculate interval length from the previous visit. For the first observation of each subject LAGVISIT and LAGDATE will contain the last values from the previous subject. These meaningless values are not used because they are excluded by the IF statement.

This PROC PRINT listing of the resultant data table shows the relationship between the current and lagged values.

**3.1.3 Using the LAG Function**

| SUBJECT | lagvisit | VISIT | lagdate | LABDT | interval |
|---:|---:|---:|---|---|---:|
| 200 | 1 | 2 | 07/06/2006 | 07/13/2006 | 7 |
|  | 2 | 5 | 07/13/2006 | 07/21/2006 | 8 |
|  | 5 | 6 | 07/21/2006 | 07/29/2006 | 8 |
|  | 6 | 7 | 07/29/2006 | 08/04/2006 | 6 |
|  | 7 | 8 | 08/04/2006 | 08/11/2006 | 7 |
|  | 8 | 9 | 08/11/2006 | 09/12/2006 | 32 |
|  | 9 | 9 | 09/12/2006 | 09/13/2006 | 1 |
|  | 9 | 10 | 09/13/2006 | 10/13/2006 | 30 |
| 201 | 1 | 2 | 07/07/2006 | 07/14/2006 | 7 |
|  | 2 | 5 | 07/14/2006 | 07/21/2006 | 7 |
|  | 5 | 4 | 07/21/2006 | 07/26/2006 | 5 |

....Portions of the table are not shown....

The DIF function is designed to calculate the difference between a value and its lag value, as we have done here. In the previous example the INTERVAL could have been calculated using the DIF function.

```sas
interval= dif(labdt);
```

The full code for this solution is shown in example program E3_1_3b.sas.

## SEE ALSO

Schreier (2007) discusses in detail the issues associated with conditionally executing the LAG function and shows how to do it appropriately.

## 3.1.5 Look-Ahead Using a Double SET Statement

Using two SET statements within the same DATA step can have a similar effect as the MERGE statement. While this technique can offer you some additional control, there may also be some additional overhead in terms of processing.

Like in the example in Section 3.1.4, the following example calculates the number of days to the next visit. An observation is read ❶ and then the look-ahead observation is conditionally read using a second SET statement ❹.

```sas
data nextvisit (keep=subject visit labdt days2nextvisit);
    set labdates (keep=subject visit labdt) ❶
        end=lastlab; ❷
    if not lastlab then do; ❸
        set labdates(firstobs=2 ❹
            keep=subject labdt
            rename=(subject=nextsubj labdt=nextdt));
        Days2NextVisit = ifn(subject=nextsubj,nextdt=labdt, ., .); ❺
    end;
    run;
```

- 1. The primary or current observation is read with the first SET statement.
- 2. The END= option on the SET statement creates the temporary variable LASTLAB that will take on the value of 1 only when the last observation is being read.
- 3. When the current observation is not the last, there will be at least one more look-ahead observation. Prepare to read that look-ahead observation. This is a minor additional overhead that the example in Section 3.1.4 does not have.
- 4. The look-ahead observation is read by using the FIRSTOBS= data set option to provide an initial off-set from the current observation. This value could be changed to look-ahead more than one observation.
- 5. The look-ahead calculations are performed.

A solution similar to the one shown here has been proposed by Jack Hamilton.

## MORE INFORMATION

A double SET statement is used with the POINT= option to look both forward and backward in the second example in Section 3.8.1.

## 3.1.6 Look-Back Using a Double SET Statement

A look-back for an unknown number of observations is not easily accomplished using the LAG function. Arrays can be used (see Section 3.1.2), but coding can be tricky. Two SET statements can be applied to the problem without resorting to loading and manipulating an array.

In this example we would like to find all lab visits that fall between the first and second POTASSIUM reading that meets or exceeds 4.2 inclusively. Patients with fewer than two such readings are not to be included, nor are any readings that are not between these two (first and second) peaks. Clearly we are going to have to find the second occurrence for a patient, if it exists, and then look-back and collect all the observations between the two observations of interest. This can be done using two SET statements. The first SET statement steps through the observations and notes the locations of the peak values. When it is needed the second SET statement is used to read the observations between the peaks.

```sas
data BetweenPeaks(keep=subject visit labdt potassium);
   set labdates(keep=subject labdt potassium);
   by subject labdt;
   retain firstloc .
          found ' ';
   obscnt+1;
   if first.subject then do;
      found=' ';
      firstloc=. ;
   end;
   if found=' ' and potassium ge 4.2 then do;
      if firstloc=. then firstloc=obscnt;
      else do;
         * This is the second find, write list;
         found='x';
         do point=firstloc to obscnt;
            set labdates(keep=subject visit labdt potassium)
                point=point;
            output betweenpeaks;
         end;
      end;
   end;
run;
```

- ❶ The variables that are used to remember information across observations are retained.
- ❷ The observation is counted. In this case _N_ could have been used instead of OBSCNT; however, since _N_ counts passes of the DATA step, it is not as robust when data are read from within a DO loop, such as is done here.
- ❸ The retained variables must be initialized for each subject.
- ❹ Initialize the flag variable FOUND. This variable notes whether or not a second peak value has been found.
- ❺ When true, either the first or second peak (value of POTASSIUM >= 4.2) has been found.
- ❻ This must be the first peak and the current observation number is stored. If a second peak is found, this will become the starting point for reading the data between peaks.
- ❼ The flag variable FOUND notes that the second peak has been found and that we no longer need to search for additional observations for this subject.
- ❽ The DO loop index variable POINT cycles through the observation numbers between the two peaks.
- ❾ The POINT= option is used to indicate the temporary variable (POINT) that holds the observation number that is to be read.
