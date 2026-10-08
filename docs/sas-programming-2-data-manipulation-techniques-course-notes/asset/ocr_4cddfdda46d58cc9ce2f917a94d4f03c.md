# Controlling Variable Output

The task is to drop Street_ID and Country from usa, drop Street_ID, Country, and State from australia, and keep all variables in other.

| ID | Employee_Name | Street_Name | City | State | Postal_Code |
|---|---|---|---|---|--|
| 120104 | Abbott, Roy | 627 | Edwards Mill Rd | FL | 39150 |
| 120769 | Akincluir, Tameka | 5 | Donkey Road | Philadelphia | PA | 19143 |
| 120868 | Cairns, Riley | 50 | California Ct | San Diego | CA | 92101 |

| ID | Employee_Name | Street_Name | City | Postal_Code |
|---|---|---|---|--|
| 120145 | Aliazetti, Sandy | 90 | Bingley Street | Melbourne | 2001 |
| 120508 | Durant, Kevin | 24 | Street Road | Sydney | 2118 |
| 120699 | Baker, Gabriela | 106 | Torak Road | |

| ID | Employee_Name | Street_ID | Street_Name | City | State | Postal_Code | Country |
|---|---|---|---|---|---|---|--|
| 120318 | Danielle, Scott | 80012167 | Sunderland | Philadelphia | 19150 | us |
| 120697 | Jonathan, Mary | 80012189 | 4623 | Philadelphia | PA | 19152 | us |
| 120747 | Farthing, Zelia | 80012756 | 789 | San Diego | CA | 92118 | us |

# DROP= Option in an Output Data Set

```
SAS-data-set(DROP=variable-1 <variable-2 ...variable-n>)
```

![](bbox=[0.115, 0.535, 0.675, 0.705])