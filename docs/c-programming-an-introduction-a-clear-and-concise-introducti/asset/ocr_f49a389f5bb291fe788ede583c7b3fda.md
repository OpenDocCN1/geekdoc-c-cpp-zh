```
letterGrade = "F";
cout << numGrade << " is a " << letterGrade
     << endl;
```

This new version of the program eliminates the unnecessary tests when one of the conditions is true. If the user enters the score 74, the condition (numGrade >= 70) is true, so letterGrade is assigned the value “C” and the program skips to the first line after the last else if clause, and displays the output:

74 is a C

One improvement we can make on the program is to eliminate the last else if clause, since if none of the other conditions is found true then the letter grade for that score must be “F”. So we can rewrite the program this way:

```
int numGrade;
string letterGrade;
cout << "Enter the numerical score: ";
cin >> numGrade;
if (numGrade >= 90)
    letterGrade = "A";
else if (numGrade >= 80)
    letterGrade = "B";
else if (numGrade >= 70)
    letterGrade = "C";
else if (numGrade >= 60)
    letterGrade = "D";
else
```