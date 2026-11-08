Because of the flexibility for structuring options in the OUTPUT statement, the previous MAXID option could also have been written as:

```
```sas
var ht wt;
output out=stats
   mean= meanHT MeanWT
   max=maxHT maxWT
   maxid(ht(subject))=maxHtSubject
   maxid(wt(subject))=maxWtSubject
;
```
```

When more than one variable is needed to identify the observation with the extreme value, the MAXID supports a list. As before when specifying lists, there is a one-to-one correspondence between the two lists (the list of ID variables and the list of generated variables). In this OUTPUT statement both the SUBJECT and SSN are used in the list of identification variables. Consequently a new variable is created for each in the summary data set.

```
```sas
var ht wt;
output out=stats
   mean= meanHT MeanWT
   max=maxHT maxWT
   maxid(ht(subject ssn))= MaxHtSubject MaxHtSSN
   maxid(wt(subject ssn))= MaxWtSubject MaxWtSSN
;
```
```

# ## 7.4.2 Using the IDGROUP Option

The MAXID and MINID options allow you to capture only a single extreme. It is also possible to display a group of the extreme values using the IDGROUP option.

Like the MAXID and MINID options, this option allows you to capture the maximum or minimum value and associated ID variable(s). More importantly, however, you may select more than just the single extreme value.

```
```sas
proc summary data=advrpt.demog;
   class race;
   var wt;
   output out=stats
      mean= MeanWT
      max(wt)=maxWT ❶
      idgroup (max(wt) out[2] (subject sex)=maxsubj) ❷❸❹
      ;
run;
```
```

In this example the maximum WT has been requested using the MAX statistic ❶. In addition the IDGROUP option has been requested to identify the two ❷ individuals (identified by using SUBJECT and SEX ❸) with the largest values of WT ❹.

❶ The prefix for the variable name that will hold SUBJECT number with the maximum weight is MAXSUBJ. Since there is no corresponding prefix for SEX, the original variable will be used as the prefix. Because we have only one analysis variable, there will not be a naming conflict; however, not specifying the new variable's name is generally to be avoided. Even with the /AUTONAME option in force there can be naming conflicts with only moderately complex IDGROUP options that do not name the new variables.