# APPENDIX A Answers to Mini-Quizzes and Labs

```
else if (totalPoints >= 280)
grade = 'B';
else if (totalPoints >= 245)
grade = 'C';
else if (totalPoints >= 210)
grade = 'D';
else
grade = 'F';
```

```
//display the total points, grade, and number of scores
cout << "Total points earned: " << totalPoints << endl;
cout << "Grade: " << grade << endl;
cout << "Number of scores: " << numScores << endl;
system("pause");
return 0;
```

# LAB 7-4 Desk-Check

![](bbox=[0.305, 0.431, 0.365, 0.485])

First desk-check:

| squaredNumber | number |
|---|---|
| 6 | 2 |
| 8 | 3 |
| 9 | 4 |
| 16 | 5 |

Corrected code:

```
//declare variables
int squaredNumber = 0;
for (int number = 1; number = number + 1)
{
  squaredNumber = number * number;
  cout << squaredNumber << endl;
} //end for
```

Second desk-check:

| squaredNumber | number |
|---|---|
| 6 | 2 |
| 8 | 3 |
| 9 | 4 |
| 16 | 5 |
| 25 | 6 |