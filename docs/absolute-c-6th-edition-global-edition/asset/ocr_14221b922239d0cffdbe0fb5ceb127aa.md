```
```cpp
int num;
string s = "10";
stringstream ss(s);
ss >> num;
```
```

20. The stringstream variable ssNum that is used to convert field to a double needs to be cleared for each new string that is processed. This can be accomplished by invoking the clear function inside the while loop.

```
```cpp
stringstream ssList, ssNum;
string numbers = "1.1, 1.2, 1.3";

double total = 0;
double num;

ssList.clear();
ssList.str(numbers);

string field;
while (getline(ssList, field, ','))
{
    ssNum.clear();
    ssNum.str(field);
    ssNum >> num;
    total += num;
}
cout << total << endl;
```
```

# Programming Projects

+   1. Write a program that will search a file of numbers of type int and print all the prime numbers in that file on the screen. The file contains nothing but numbers of type int separated by blanks or line breaks.
+   
+   2. Write a program that takes its input from a file of numbers of type double and outputs the average of the numbers in the file to the screen. The file contains nothing but numbers of type double separated by blanks and/or line breaks.
+   
+   3. a. Compute the median of a data file. The *median* is the number that has the same number of data elements greater than the number as there are less than the number. For purposes of this problem, you are to assume that the data is sorted (that is, is in increasing order). The median is the middle element of the file if there are an odd number of elements, or is the average of the two middle elements if the file has an even number of elements. You will need to open the file, count the members, close the file and calculate the location of the middle of the file, open the file again (recall the “start over” discussion at the beginning of this chapter), count up to the file entries you need, and calculate the middle.