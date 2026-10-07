# EXERCISES 109

| DATALINES; | Lucius | 201-876-0987 |
| Jones | Pam | 987-998-2948 |
| Abby | Adams | 214-876-0987 |
| Smith | Bev | 213-765-0987 |
| Zoll | Tim Bob | 303-987-2309 |
| Baker | Crusty | 222-324-3212 |
| Smith | John | 234-943-0987 |
| Smith | Arnold | 234-321-2345 |
| Jones | Jackie | 456-987-8077 |

```
* Modify to sort by first name within last (by last first);
PROC SORT; BY LAST;
PROC PRINT LABEL;
TITLE 'ABC Company';
TITLE 'Telephone Directory';
RUN;
```

# 4.2 Create subset sets.

Using the permanent SAS data set, write SAS code to do the following:

+   a. Create a subset (into an SAS data set named SMALL) consisting of all whose engine size is less than 2.0L. On the base of this data set, find the average city and highway miles per gallon for these vehicles

```
DATA SMALL;SET "C:\SASDATA\CARS";
IF ENGINESIZE LT 2;
```

+   b. Create a subset (into an SAS data set named HYBRID) of all hybrid vehicles in the dataset. For these vehicles:
I. List the BRAND and MODEL names.
II. Find the average city and highway miles per gallon.
c. Create a subset (into an SAS data set named AWDSUV) consisting of all vehicles that are SUVs and have all-wheel drive. For these vehicles:
I. List the BRAND and MODEL names.
II. Use PROC MEANS to find the average city and highway miles per gallon.
D. Sort the data in AWDSUV by highway miles per gallon (smallest to largest). List the BRAND, MODEL, and highway miles per gallon for this sorted data set.

# 4.3 DROP or KEEP.

Using the SOMEDATA permanent SAS dataset, write SAS code to do the following:

+   a. Calculate the changes from baseline (i.e., 6-month reading minus baseline, etc.) for 6, 12, and 24 months. Times are given as:

```
TIME1 is BASELINE
```