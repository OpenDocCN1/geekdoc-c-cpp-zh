# DISPLAY 7.14 Two-Dimensional Array (part 3 of 3)

```
87        cout << setw(10) << stNum
88            << setw(5) << stAve[stNum - 1] << " ";
89        for (int quizNum = 1; quizNum <= NUMBER_QUIZZES; quizNum++)
90            cout << setw(5) << grade[stNum - 1][quizNum - 1];
91        cout << endl;
92    }
93
94    cout << "Quiz averages = ";
95    for (int quizNum = 1; quizNum <= NUMBER_QUIZZES; quizNum++)
96        cout << setw(5) << quizAve[quizNum - 1];
97    cout << endl;
98 }
```

# Sample Dialogue

<The dialogue for filling the array grade is not shown.>

| Student | Ave | Quizzes |  |  |
|---|---|---|---|---|
| 1 | 10.0 | 10 | 10 | 10 |
| 2 | 1.0 | 2 | 0 | 1 |
| 3 | 7.7 | 8 | 6 | 9 |
| 4 | 7.3 | 8 | 4 | 10 |
| Quiz averages = |  | 7.0 | 5.0 | 7.5 |

# DISPLAY 7.15 The Two-Dimensional Array grade

![](bbox=[0.15, 0.68, 0.85, 0.9])