```
```cpp
Program 4.15  Finding the student score based on three tests (Continued)
49  {
50    temp += 1;
51  }
52  score = temp / 2;
53  // Print results
54  cout << "Scores: " << score1 << " " << score2 << " " << score3 << endl;
55  cout << "minimum and maximum scores: ";
56  cout << minScore << " " << maxScore << endl;
57  cout << "Student score: " << score;
58  return 0;
59  }
Run:
Enter the first score: 78
Enter the second score: 92
Enter the third score: 79
Scores: 78 92 79
minimum and maximum scores: 78 92
Student score: 85
Run:
Enter the first score: 65
Enter the second score: 93
Enter the third score: 60
Scores: 65 93 60
minimum and maximum scores: 60 93
Student score: 77
```
```

# 4.5.2 Finding the Tax for a Given Income

Let us design a program that calculates and prints the tax for a given income.

# Understand the Problem

Income tax in many countries is bracketed, which means there are different tax rates for each bracket as shown in Figure 4.14.

The total tax is the sum of the taxes in each bracket (Table 4.4). A person in bracket1 pays tax1. A person in bracket2 pays the sum of tax1 and tax2. A person in bracket3 pays tax1, tax2, and tax3. A person in bracket4 pays tax1, tax2, tax3, and tax4. The *diff* in the table means the difference between the income and the previous limit.

![](bbox=[0.28, 0.855, 0.85, 0.925])

Figure 4.14 Concept of bracketed tax