```
DATALINES;
A 88
A 89
...etc...
; PROC TTEST DATA=TEMP;
CLASS ; VAR ;
...etc...
RUN;
```

c. What is your conclusion?

# 11.2 Perform a t-test on pre- and postdata.

To test if memory technique was effective, a researcher provided five people with a list of 10 objects for 45 seconds then tested them to see how many they remembered (pretest). He taught them a memory technique and presented them with a list of 10 different (although similar) objects and administered a similar test (posttest). The results follow:

| Subject | Pretest | Posttest |
|---|---|---|
| AD | 6 | 10 |
| GE | 7 | 7 |
| KL | 9 | 10 |
| MM | 4 | 7 |
| OU | 7 | 9 |

+   a. Assuming that the differenced data are approximately normally distributed, analysis is appropriate to test the hypothesis that training subjects on a memory technique would improve their ability to remember a list of 10 objects?

+   b. Using code similar to that in the paired t-test Hands-on Example, write a SAS program to perform the appropriate test for this analysis. Here is some code to get started:

```
DATA MEMORY;
INPUT PRETEST
DATALINES;
6 10
...etc...
; PROC TTEST DATA=MEMORY;
...etc...
RUN;
```

+   c. What are your conclusions?