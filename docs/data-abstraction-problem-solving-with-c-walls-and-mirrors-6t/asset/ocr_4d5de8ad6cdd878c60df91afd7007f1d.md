fail-safe programming. A program that appears to have been running correctly may at some point behave unexpectedly, even if the data that it reads is valid. For example, the program may not have accounted for the particular data that elicited the surprise behavior, even though you tried your best to test the program's logic. Or perhaps you modified the program and that modification invalidated an assumption that you made in some other part of the program. Whatever the difficulty, a program should have built-in safeguards against these kinds of errors. It should monitor itself and be able to indicate that something is wrong and that you should not trust the results.

# B.5.1 Guarding Against Errors in Input Data

Suppose that you are computing statistics about the people in income brackets between $10,000 and $100,000. The brackets are rounded to the nearest thousand dollars: $10,000, $11,000, and so on to $100,000. The raw data is a file of one or more lines of the form

G N

where N is the number of people with an income that falls into the G-thousand-dollar group. If several people have compiled the data, several entries for the same value of G might occur. As the user enters data, the program must add up and record the number of people for each value of G. From the problem's context, it is clear that G is an integer in the range 10 to 100, inclusive, and N is a nonnegative integer.

As an example of how to guard against errors in input, consider an input function for this problem. The first attempt at writing this function will illustrate several common ways in which a program can fall short of the fail-safe ideal. Eventually you will see an input function that is much closer to this ideal than the original solution.

A first attempt at the function might be

```
```cpp
const int LOW_END = 10; // 10-thousand-dollar income
const int HIGH_END = 100; // 100-thousand-dollar income
const int TABLE_SIZE = HIGH_END - LOW_END + 1;
typedef int TableType[TABLE_SIZE];

/** Reads and organizes income statistics.
@param incomeData A TableType of income statistics.
Pre: The calling module gives directions to the user.
Input data is error-free, and each input line has the form
G N, where N is the number of people with an income in the
G-thousand-dollar group and LOW_END <= G <= HIGH_END.
An input line with values of zero for both G and N
terminates the input.
Post: incomeData[G - LOW_END] is the total number of people
with an income in the G-thousand-dollar group for each
read. The values in read are displayed. */
void readData(TableType incomeData)
{
    bool terminateInput = false;
    int group, number; // input values

    // Clear array
    for (group = LOW_END; group <= HIGH_END; group++)
        incomeData[group - LOW_END] = 0;

    do
    {
        cout << "Please enter group and number of ";
        cout << "people in group, separated by a space: ";
        cin >> group >> number;
```
```

This function is not fail-safe