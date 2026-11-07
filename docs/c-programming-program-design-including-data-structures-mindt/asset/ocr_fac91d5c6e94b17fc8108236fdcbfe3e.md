```
```cpp
for (i = 1; i <= 4; i++)
{
    sum = 0;

    if (i != 4)        //software patch
    {
        for (j = 1; j <= 4; j++)
        {
            infile >> num;
            cout << num << " ";
            sum = sum + num;
        }

        cout << "sum = " << sum << endl;
    }
}
return 0;
}
```
```

# Sample Run:

```
87 78 83 94  sum = 342
23 89 92 70  sum = 274
92 78 34 56  sum = 260
```

Clearly, the program is working correctly now.

As we can see, the programmer merely observed the symptom and addressed the problem by adding a software patch. However, if you look at the code, not only does the program execute extra statements, it is also an example of a partially understood concept. It appears that the programmer does not have a good grasp of why the earlier program produced four lines rather than three. Adding a patch eliminated the symptom, but it is a poor programming practice. The programmer must resolve why the program produced four lines. Looking at the program closely, we can see that the four lines are produced because the outer loop executes four times. The values assigned to loop control variable i are 1, 2, 3, and 4. This is an example of the classic “off-by-one” problem. (In an “off-by-one” problem, either the loop executes one too many or one too few times.) We can eliminate this problem by correctly setting the values of the loop control variable. For example, we can rewrite the loops as follows:

```
```cpp
for (i = 1; i <= 3; i++)
{
    sum = 0;

    for (j = 1; j <= 4; j++)
    {
        infile >> num;
        cout << num << " ";
        sum = sum + num;
    }

    cout << "sum = " << sum << endl;
}
```
```