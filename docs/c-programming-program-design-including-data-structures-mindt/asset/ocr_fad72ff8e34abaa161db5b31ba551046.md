```
```cpp
inFile.open("test.txt"); //open the input file

if (!inFile)
{
    cout << "Cannot open the input file. "
         << "The program terminates." << endl;
    return 1;
}

outFile.open("testavg.out");  //open the output file

outFile << fixed << showpoint;
outFile << setprecision(2);

cout << "Processing data" << endl;

inFile >> firstName >> lastName;
outFile << "Student name: " << firstName
        << " " << lastName << endl;

inFile >> test1 >> test2 >> test3
       >> test4 >> test5;
outFile << "Test scores: " << setw(4) << test1
        << setw(4) << test2 << setw(4) << test3
        << setw(4) << test4 << setw(4) << test5
        << endl;

average = (test1 + test2 + test3 + test4 + test5) / 5.0;

outFile << "Average test score: " << setw(6)
        << average << endl;

inFile.close();
outFile.close();

return 0;
}
```
```

# Confusion between the Equality Operator (==) and the Assignment Operator (=)

Recall that if the decision-making expression in the if structure evaluates to true, the statement part of the if structure executes. In addition, the expression is usually a logical expression. However, C++ allows you to use any expression that can be evaluated to either true or false as an expression in the if structure. Consider the following statement:

```
```cpp
if (x = 5)
    cout << "The value is five." << endl;
```
```