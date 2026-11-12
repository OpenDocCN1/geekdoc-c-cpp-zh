```
```cpp
int binarySearch(int x[], int n)
{
    int first = 0;
    int last = ARRAY_SIZE - 1; //SMALLEST INDEX VALUE WE ARE CONSIDERING
    int mid; //LARGEST INDEX VALUE WE ARE CONSIDERING
    int index = NOTFOUNDERROR; //MID POINT INDEX THAT WE ARE CONSIDERING
    //VALUE TO RETURN WHICH INDICATES LOCATION OR NOT FOUND

    do
    {
        mid = (first + last) / 2;

        if(n > x[mid])
        {
            first = mid + 1; //TARGET GREATER THAN VALUE AT MID -> UPDATE FIRST
        }
        else if(n < x[mid])
        {
            last = mid - 1; //TARGET LESS THAN VALUE AT MID -> UPDATE LAST
        }
        else
        {
            index = mid; //TARGET HAS BEEN LOCATED IN THE ARRAY
            last = first - 1; //WHAT DOES THIS DO? WOULD first = last + 1 ALSO WORK?
        }
    }while(first <= last);

    return(index);
}
```
```

The user-defined searching function will search the array until the first is greater than the last which would occur for one of the following reasons:

+   - The target is found.
+   - There are no elements in the array remaining as candidates to be searched.