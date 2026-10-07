# Chapter 26: Introducing the Structured Query Language 443

Figure 26.6: Matching Subj Numbers from Both Tables

| Subj_Health | Subj_Demog | Weight | Name | Gender |
| --- | --- | --- | --- | --- |
| 001 | 001 | 68 | Friedman | M |
| 003 | 003 | 74 | McGoldrick | F |
| 005 | 005 | 60 | Chien | F |

Only subjects who are in both tables are listed here. In SQL terminology, this is called an inner join. It is equivalent to a DATA step where each of the two data sets contributes to the merge.

Just so this is clear, here is the same (well almost—in PROC SQL, you get two Subj variables) result using a DATA step:

# Program 26.7: Performing an Inner Join Using a DATA Step

```
proc sort data=Learn.Health out=Health;
  by Subj;
run;

proc sort data=Learn.Demographic out=Demographic;
  by Subj;
run;

data Inner;
  merge Health(in=in_Health)
        Demographic(in=in_Demographic);
  by Subj;
  if in Health and in_Demographic;
run;

title "Performing an Inner Join Using a DATA Step";
proc print data=Inner;
  id Subj;
run;
```