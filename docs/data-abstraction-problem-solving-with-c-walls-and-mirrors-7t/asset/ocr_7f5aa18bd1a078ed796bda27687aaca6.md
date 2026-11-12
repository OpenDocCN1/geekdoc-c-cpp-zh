```
bool readData(TableType incomeData)
{
    int group = -1;
    int number = -1;    // Input values
    bool dataCorrect = true; // No data error found as yet
    bool userFinished = false;
    for (group = LOW_END; group <= HIGH_END; group++)
        incomeData[group - LOW_END] = 0;
    do
    {
        cout << "Please enter group and number of ";
        cout << "people in group, separated by a space: ";
        cin >> group >> number;
        cout << "Input line specifies that income group "
             << group << "contains " << number
             << " people.\n";
        if ((group >= LOW_END) && (group <= HIGH_END) &&
            (number >= 0))
        // Input data is valid - add it to tally
            incomeData[group - LOW_END] += number;
        else if ((group == 0) && (number == 0))
            userFinished = true; // User signaled input is finished
        else
        {
            // Error in input data:
            // Set error flag and ignore input line
            dataCorrect = false;
        } // end if
    } while (dataCorrect && !userFinished); // end do-while
    return dataCorrect;
} // end readData
```

Although this input function will behave gracefully in the face of most common input errors, it is not completely fail-safe. What happens if an input line contains only one integer? What happens if an input line contains a noninteger? The function would be more fail-safe if it reads its input behavior by character, converted the characters to an integer, and checked for the end of the input line. In most contexts, this processing would be a bit extreme. However, if the people who enter the data frequently err by typing nonintegers, you could alter the input function easily because the function is an isolated module. In any case, the function's initial comments should include any assumptions it makes about the data and an indication of what might make the program abort abnormally.

# B.5.2 Guarding Against Errors in Program Logic

Now consider the second type of error that a program should guard against: errors in its own logic. These are errors that you may not have caught when you debugged the program or that you may have introduced through program modification.

Unfortunately, a program cannot reliably let you know when something is wrong with it. (Could you rely on a program to tell you that something is wrong with its mechanism for telling you that something is wrong?) You can, however, build into a program checks that ensure that certain conditions always hold when the program is correctly implementing its algorithm. For example, all integers in the array incomeData of the previous example must be greater than or equal to zero. Although we