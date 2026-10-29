```
//if target was found, then
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
21.
int a[4][5];
int index1, index2;
for (index1 = 0; index1 < 4; index1++)
    for (index2 = 0; index2 < 5; index2++)
        cin >> a[index1][index2];
```

```
22.
void echo(const int a[][5], int sizeOfa)
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

# Programming Projects

+   1. Write a program that reads in the average mileage in kilometers per liter of a car at 10 different speeds ranging from 10 kilometers per hour to 100 kilometers per hour, and then reads in the actual mileage obtained for a test drive at each of the 10 speeds. The program then prints out a nicely formatted table showing the mileage obtained during the 10 test drives and whether it was above or below the average mileage at that speed, and by how much it varied. The average mileage should be given for the 10 different speeds in 10 kmph steps. To obtain the mileage during the test drives, the program repeatedly asks the user to enter the mileage for each speed. The output should correctly label each speed.
+   
+   After you have completed the previous program, produce an enhanced version that also outputs a graph showing the average and actual mileage of the car at each speed. The graph should be similar to the one shown in Display 5.4, except that there should be two bars for each speed and they should be labeled as average and actual mileage at each speed.