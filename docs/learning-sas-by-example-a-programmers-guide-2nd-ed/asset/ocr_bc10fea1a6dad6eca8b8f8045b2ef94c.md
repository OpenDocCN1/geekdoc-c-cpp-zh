# 90 Learning SAS by Example: A Programmer’s Guide, Second Edition

When you write a program like this, you need to "play computer" and make sure your logic is correct. For example, if a person is 25 years old? The first IF statement is false because Age is not missing. The next ELSE IF statement is evaluated and found to be false. Finally, the third IF statement is evaluated and AgeGroup is set equal to 2. Because this IF statement is true, all the ELSE IF statements are skipped.

If you are working with large data sets and want to squeeze every last drop out of the efficiency tank, you should place the IF statements in order, the ones most likely to have a true condition to the ones least likely to have a true condition. This increases efficiency because SAS skips all the ELSE conditions when a previous IF condition is true. The disadvantage of using this technique is that it makes the program harder to read and more likely to have an error. With the speed of modern computers, you should consider these extreme efforts only for production programs that operate on very large data sets.

# 7.3 The Subsetting IF Statement

If you want to create a subset of data from a raw file or from an existing SAS data set, you can use a special form of an IF statement called a *subsetting IF*. For example, let’s use the raw data from 7.1, but restrict the data set to females only. Here is the program:

# Example 7.4: Demonstrating a Subsetting IF statement

```
data Females;
  length Gender $ 1
  Quiz $ 2;
  input Age Gender Midterm Quiz FinalExam;
  if Gender = 'F';
datalines;
21 M 80 B- 82
  F 90 A- 93
35 M 87 B+ 85
48 F 76
59 F 95 A+ 97
15 M 88 93
67 F 90 A 91
  M 62 F 67
35 F 77 C- 77
49 M 59 C 81;
  title "Listing of Females";n  proc print data=Females noobs;
run;
```

Notice that there is no THEN following the IF in this program. If the condition is true, the program continues to the next statement; if the condition is false, control returns to the top of the DATA step. In this case, the only statement following the subsetting IF statement is a DATALINES statement. If the value of Gender is F, the end of the DATA step is reached and an automatic output occurs. If the value of Gender is not equal to F, control returns to the top of the DATA step and the automatic output does not occur.

Here is the output:

![](bbox=[0.104, 0.923, 0.895, 0.995])