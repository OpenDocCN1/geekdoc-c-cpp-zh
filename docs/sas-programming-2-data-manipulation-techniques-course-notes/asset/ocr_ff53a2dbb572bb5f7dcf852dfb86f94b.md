# 5.07 Multiple Choice Poll

What expression completes the assignment statement to correctly extract 2007 from the Text variable?

```
data Scan Quiz;
Text="New Year's Day, January 1st, 2007";nYear= ?
run;
```

+   a. scan(Text,-1);
b. scan(Text,6);
c. scan(Text,6, ' ');
d. All of the above would work.

# Creating SCAN Mailing List Data

Using the SCAN function gives an easy way to separate the names for the mailing list.

```
data labels;
set orion.contacts;
length FName LName = $15;
FName=scan(Name,2,', ');
LName=scan(Name,1,', ');
run;
```

# Partial labels data set

| ID | Name | Title | FName | LName |
|---|---|---|---|---|
| AQI | Farr, Sue | Ms. | Sue | Farr |
| CCI | Cox, Kay B. | Dr. | Ray B. | Cox |
| CNI | Mason, Ron | | Ron | Mason |
| CS | Ruth, G. H. | Ms. | G. H. | Ruth |