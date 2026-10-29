```
{ int index = 0;
bool found = false;
while ((!found) && (index < numberUsed))
if (target == a[index])
found = true;
else
index++;
//If target was found, then
//found == true and a[index] == target.
if (found)
where = index;
return found;
}
```

20. 0 1 2 3
0 1 2 3
0 1 2 3
0 1 2 3

```
21. int a[4][5];
int index1, index2;
for (index1 = 0; index1 < 4; index1++)
for (index2 = 0; index2 < 5; index2++)
cin >> a[index1][index2];
```

```
22. void echo(const int a[][5], int sizeOfa)
//Outputs the values in the array a on sizeOfa lines
//with 5 numbers per line.
{
for (int index1 = 0; index1 < sizeOfa; index1++)
{
for (int index2 = 0; index2 < 5; index2++)
cout << a[index1][index2] << " ";
cout << endl;
}
}
```

# PROGRAMMING PROJECTS

![](bbox=[0.05, 0.9, 0.2, 0.96])

1. Write a program that reads in the average monthly rainfall for a city for each month of the year and then reads in the actual monthly rainfall for each of the previous 12 months. The program then prints out a nicely formatted table showing the rainfall for each of the previous 12 months as well as how much above or below average the rainfall was for each month. The average monthly rainfall is given for the months January, February, and so forth, in order. To obtain the actual rainfall for the previous 12 months, the program first