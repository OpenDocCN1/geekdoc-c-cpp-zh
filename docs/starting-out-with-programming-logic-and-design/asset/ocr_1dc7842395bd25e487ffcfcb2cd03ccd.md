# 10.2 Using Loops to Process Files 393

Take a closer look at line 15:

```
While NOT eof(salesFile)
```

When you read this pseudocode, you naturally think: *While not at the end of the file...* This statement could have been written as:

```
While eof(salesFile) == False
```

Although this is logically equivalent, most programmers will prefer to use the NOT operator as shown in line 15 because it more clearly states the condition that is being tested. Figure 10-14 shows a flowchart for the program.

Figure 10-14 Flowchart for Program 10-4

![](bbox=[0.125, 0.308, 0.737, 0.906])