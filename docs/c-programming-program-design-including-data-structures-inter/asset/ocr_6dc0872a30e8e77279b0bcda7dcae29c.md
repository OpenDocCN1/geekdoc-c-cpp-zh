```
```cpp
void timeOnJob(int arvHr, int arvMin, bool arvIsAM,
               int depHr, int depMin, bool depIsAM)
{
    int arvTimeInMin;
    int depTimeInMin;
    int timeOnJobInMin;

    else if (arvIsAM == true && depIsAM == false)
    {
        arvTimeInMin = arvHr * 60 + arvMin;
        depTimeInMin = depHr * 60 + depMin;

        timeOnJobInMin = (720 - arvTimeInMin) + depTimeInMin;
        cout << "Time spent of job: "
             << timeOnJobInMin / 60 << " hour(s) and "
             << timeOnJobInMin % 60 << " minutes." << endl;
    }

    else
    if (arvTimeInMin <= depTimeInMin)
    {
        timeOnJobInMin = depTimeInMin - arvTimeInMin;
        cout << "Time spent of job: "
             << timeOnJobInMin / 60 << " hour(s) and "
             << timeOnJobInMin % 60 << " minutes." << endl;
    }
    else
        cout << "Invalid input." << endl;
    if ((arvIsAM == true && depIsAM == true)
        || (arvIsAM == false && depIsAM == false))
    {
        cout << "Invalid input." << endl;
    }

    void timeOnJob(int arvHr, int arvMin, bool arvIsAM,
                   int depHr, int depMin, bool depIsAM);
}
```
```

+   17. The function printGrade in Example 6-12 is written as a void function
+       to compute and output the course grade. The course score is passed as
+       a parameter to the function printGrade. Rewrite the function
+       printGrade as a value-returning function so that it computes and returns
+       the course grade. (The course grade must be output in the function main.)
+       Also, change the name of the function to calculateGrade.
+   18. In this exercise, you are to modify the Classify Numbers programming
+       example in this chapter. As written, the program inputs the data from the
+       standard input device (keyboard) and outputs the results on the standard