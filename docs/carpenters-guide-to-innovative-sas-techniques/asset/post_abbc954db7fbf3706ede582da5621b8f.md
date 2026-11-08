
## CONTENTS

The CONTAINS operator works much like the INDEX function to determine if a text string can be found within another string. The word CONTAINS can be replaced with its mnemonic, the question mark (?).

```
title2 'CONTAINS';
proc print data=advrpt.demog;
    var lname fname edu;
    where lname contains 'son';
/*  where lname ? 'son';*/
/*  where index(lname,'son');*/
    run;
```

- 3. All last names that contain the letters ‘son’ will be printed. Like all string comparisons, the search is case sensitive.
- 4. The question mark could be used to replace the CONTAINS operator.
- 5. The INDEX function could also be used.

CONTAINS is negated by preceding the operator with a NOT or other negation mnemonic.

### IS MISSING

The IS MISSING operator can be used to check for missing values. One advantage is that it can be used to check for either a numeric or a character missing value. Either the IS MISSING or the IS NULL operator can be used.

```
title2 'IS MISSING';
proc print data=advrpt.demog;
    var lname fname edu symp;
    where edu is missing or symp is missing;
/*  where edu is null or symp is null;*/
/*  where edu = . or symp = ' ';*/
    run;
```

- 6. The syntax is the same for numeric variables (EDU) and character variables (SYMP).
- 7. IS NULL can be used instead of IS MISSING.
- 8. When checking for missing values using the ‘traditional’ approach, the programmer must be aware of the variable’s type.

Negation is formed using NOT (or other negation operator). The NOT may appear either before the IS or between the IS and MISSING.

```
where edu is not missing or symp not is missing;
```

### LIKE

The LIKE operator allows for simple pattern matching. When appropriate, more complex pattern matching can be accomplished using regular expressions in the RX() family of functions. This operator uses the percent sign (%) and the underscore (_) as wildcards. The % will stand for any number of characters and the _ is a place holder for exactly one character.

The following table shows some examples using the LIKE operator and alternate equivalent expressions.

| Using the LIKE Operator | Without the LIKE Operator | What It Does |
| --- | --- | --- |
| `lname like 'S%'` | `lname =: 'S'`<br>`substr(lname,1,1) = 'S'` | Find all last names beginning with a capital S. |
| `lname like '%ly%'` | `index(lname,'ly') > 0`<br>`lname contains 'ly'` | Find all last names containing an 'ly'. |
| `lname like 'Ch__'` | `substr(lname,1,2) = 'Ch' and`<br>`length(lname)<5` | Any two, three, or four letter last names starting with Ch. |

When using the % and _ with the LIKE operator, you need to be careful, as it is possible to return unanticipated values.

- A trailing _ will not select anything if the _ is past the length of the variable.
- Whenever the % is followed by other search characters, be sure to enclose the string in single quotes to prevent the macro parser from interpreting the % as a macro trigger.
- When the searched string contains either a _ or a %, there can be confusion between the wildcards and the actual characters. Be sure that you specify what you really mean. Since the CONTAINS operator does not utilize wildcards, it can be used when your target string contains an underscore or percent sign.

Negation of the LIKE operator is achieved using the standard negation operators.

### SAME

The SAME operator allows you to specify a composite clause through the use of separate WHERE statements. Primarily used in interactive or run-group processing, it has little use in other programming situations, since the clause cannot be maintained across step boundaries.

The first clause is specified as usual, and the second is appended with the SAME operator. If the SAME operator had not been included on the second WHERE statement, the second clause would have replaced the first.

```
proc print data=advrpt.demog;
    var lname fname edu symp;
    where lname like 'S%';
    where same edu le 15;
    run;
```

When joining two WHERE clauses with the SAME operator, the two clauses are effectively joined with an AND (both clauses have to be true for the overall result to be true).

```
where lname like 'S%';
where same and edu le 15;
```

It is common to explicitly specify the AND on the subsequent WHERE clauses. This can reduce ambiguity.

In both cases the resulting WHERE statement could have been written as:

```
where lname like 'S%' and edu le 15;
```

### Sounds like

The sounds like operator, which is coded using the mnemonic =*, uses the same algorithm as the SOUNDEX function:

- The first letter is preserved
- Vowels are eliminated
- Double letters are compressed
- The remaining letters are converted to numbers using a scheme that nominally groups letters that sound similarly in English

### 2.7.2 WHERE and BY Group Processing

| Obs | CLINNUM | SYMP | subject |
| --- | --- | --- | --- |
| 1 | 031234 | 01 | 127 |
| 2 | 031234 | 01 | 168 |
| 3 | 031234 | 04 | 110 |
| 4 | 031234 | 04 | 156 |
| 5 | 033476 |  | 148 |
| 6 | 033476 |  | 161 |
| 7 | 033476 | 09 | 116 |
| 8 | 033476 | 09 | 157 |
| 9 | 036321 | 02 | 128 |
| 10 | 036321 | 02 | 147 |
| 11 | 036321 | 06 | 135 |
| 12 | 036321 | 06 | 169 |
| 13 | 038362 |  | 145 |
| 14 | 038362 |  | 175 |
| 15 | 043320 |  | 132 |
| 16 | 043320 |  | 134 |
| 17 | 043320 | 02 | 124 |
| 18 | 043320 | 02 | 152 |
| 19 | 046789 | 10 | 107 |
| 20 | 046789 | 10 | 121 |
| 21 | 049060 | 02 | 101 |
| 22 | 049060 | 02 | 108 |
| 23 | 049060 | 02 | 164 |
| 24 | 049060 | 02 | 165 |

```
if symp ne ' ';
```

Using the subsetting IF statement 6 instead of the WHERE statement 1 changes the way that the BY groups are formed. If the DATA step that uses the IF statement 6 does not take this formation process into account, the results will be incorrect.

**2.7.2 WHERE and BY Group Processing Showing Counts**

| Obs | CLINNUM | IFsympcnt | Waympcnt |
| --- | --- | --- | --- |
| 1 | 031234 | 2 | 2 |
| 2 | 033476 | 3 | 1 |
| 3 | 036321 | 2 | 2 |
| 4 | 043320 | 3 | 1 |
| 5 | 046789 | 1 | 1 |
| 6 | 049060 | 1 | 1 |

The table above shows the counts for these two methods for a few of the clinics. Clearly we can see that there is disagreement for two of these clinics, and the reason for this difference is at the heart of the problem.

Examination of the data used to form the counts shows that the variable SYMP has at least one missing value for each of the clinics that have an incorrect count.

When the subsetting IF statement 6 executes, it eliminates these rows, but more importantly these rows are also the rows for which FIRST.CLINNUM is true. Since the row is eliminated, the counter cannot be reset 7. This does not happen when the WHERE statement 1 is used because the BY groups are formed after the elimination of rows. As a result FIRST.CLINNUM will be available for testing and will not be eliminated inappropriately.

You are not constrained to using the WHERE with BY-group processing, but you must be careful. If we remove the subsetting IF statement from the DATA step and add the same logic to the line that counts the symptoms, the counting problem is corrected.

```
if first.symp & symp ne ' ' then IFsympcnt+1;
```

Interestingly a comparison of the WHERE statement and the corrected logic using the IF statement highlights another difference between the two approaches.

**2.7.2 WHERE and BY Group Processing Showing Counts Using the Corrected IF**

| Obs | CLINNUM | IFsympcnt | Waympcnt |
| --- | --- | --- | --- |
| 1 | 031234 | 2 | 2 |
| 2 | 033476 | 1 | 1 |
| 3 | 036321 | 2 | 2 |
| 4 | 038362 | 0 |  |
| 5 | 043320 | 1 | 1 |
| 6 | 046789 | 1 | 1 |
| 7 | 049060 | 1 | 1 |

Notice that a clinic number (038362), which was not in the previous report, now appears. All observations for this clinic have SYMP=' '; consequently, it was completely removed from consideration by both the WHERE and the subsetting IF statements 1 6. Since the revised DATA step does not eliminate
