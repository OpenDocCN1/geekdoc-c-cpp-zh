A variation on the use of the UNTIL can also be seen in the following example which counts the number of visits within clinics (CLINNUM). PROC FREQ could also have been used and would have probably been more efficient, but that is quite beside the point.

```
```sas
data frq;
   set demog;
   by clinum;
   if first.clinum then cnt=0;
   cnt+1;
   if last.clinum then output frq;
run;
```
```

A common approach to this type of counting problem is to use FIRST. and LAST. processing to detect the group (clinic number) boundaries. This solution requires us to track and maintain the counter (CNT) and to control the process with two IF statements. We can simplify the code and increase efficiencies by taking

advantage of DO loops.

The DO loop surrounds the SET statement (see more about DOW loops in Section 3.9.1), and the UNTIL is used to terminate the loop. Since we do not know the upper bound of the loop, notice

```
```sas
data frq;
   do cnt = 1 by 1 until(last.clinum);
      set demog;
      by clinum;
   end;
run;
```
```

that the iterative portion of the loop specification (cnt=1 by 1) does not contain a TO keyword, which effectively creates an infinite loop. The loop is terminated with the UNTIL. A side benefit of this approach is that the counter variable, CNT, is automatically

taken care of for us. By using the DOW loop and by eliminating the IF statements, this DATA step will execute more quickly than the first approach.

**3.9.3 Special Loop Specifications**

| Obs | cnt | clinum |
|---|---|---|
| 1 | 2 | 011234 |
| 2 | 2 | 014321 |
| 3 | 3 | 023910 |
| 4 | 4 | 024477 |
| 5 | 2 | 026789 |
| 6 | 4 | 031234 |
| ... portions of the table are not shown ... | | |

> **SEE ALSO**
> The SAS Forums thread
> http://communities.sas.com/message/57412
> has a similar counting example with alternate solutions.

In this example we need to assign a value (of the variable I) from the last observation in the data set to a macro variable using

```
```sas
data _null_;
   set big;
   call symputx('bigx',i);
run;

data _null_;
   set big end=eof;
   if eof then call symputx('bigx',i);
run;
```
```

SYMPUTX, what is the best approach? Two typical solutions are shown here. Which will be more efficient—the step that executes SYMPUTX for each observation, or the one that executes the IF for each observation, but the SYMPUTX only once?

more overhead than even the IF, so the second approach is faster. However, while discussing this issue with John King, he suggested the following even more efficient approach. It is presented here mostly as an aid in understanding DATA step execution.