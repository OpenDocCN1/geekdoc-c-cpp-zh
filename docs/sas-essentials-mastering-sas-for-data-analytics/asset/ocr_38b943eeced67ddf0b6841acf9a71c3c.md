# GOING DEEPER: MORE TECHNIQUES FOR ENTERING DATA 39

+   2. Modify the INPUT statement to read in only the variables ID, GP, AGE, and TIME3.
3. Rerun the program and observe the difference in output. Note that the new output\includes statistics for AGE and TIME3. Why are statistics for ID and GP not included
in the output?

# 2.6 GOING DEEPER: MORE TECHNIQUES FOR ENTERING DATA

SAS includes myriad ways to read in data. Techniques covered far are the most common methods. The following additional techniques can also be helpful when your data are listed in multiple records per subject and when your data are in comma-delimited format.

# 2.6.1 Reading Multiple Records per Observation

Occasionally, data will be stored in such a way that multiple lines (records) are used to hold one subject's information. SAS is able to associate observations that span more than one to one subject. Suppose input records are designed so that each subject's information is contained on three lines:

```
10011 M 15 115
120 80 254
15 65 102
10012 F 25 180
130 70 240
34 120 132
10013 M 89 170
140 100 279
19 89 111
```

etc.

One method for reading this data into a SAS data set is to have three consecutive INPUT statements. Each INPUT statement advances to the next record (but stays with the same subject). Thus, the three records in the data file combine to become one “subject” in the SAS data set:

```
INPUT ID $ SEX AGE WT;
INPUT SBP DBP BLDCHL;
INPUT OBS1 OBS2 OBS3;
```

Another method for reading this data uses the / indicator in the INPUT statement to advance to the next line. Each time a / is seen in the INPUT statement, it tells SAS to go to the next physical record in the data file to find additional data for the same subject:

```
INPUT ID $ SEX AGE WT/ SBP DBP BLDCHL/ OBS1 OBS2 OBS3;
```

A third way to read this is by using the #n indicator to advance to the first column of the nth record in the group. In this case, #2 instructs SAS to begin reading the second line in the data file. The highest #n used in the INPUT statement tells SAS how many lines are used for each subject: