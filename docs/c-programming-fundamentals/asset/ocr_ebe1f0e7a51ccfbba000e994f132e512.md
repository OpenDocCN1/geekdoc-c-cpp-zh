# Algorithm for a Binary Search

+   1. Start.
+   2. Take the size and element input from the user if the array is not given.
+   3. Input the search element from the user.
+   4. Call the binary search function and pass the array, size, `firstindex`, and `lastindex`.
+   5. Execute the nested if loop search element == `array[mid]` or < `array[mid]` or > `array[mid]`.
+   6. If the result is true, then the match is found, return mid.
+   7. If the result is false, then return 0 and exit the loop.
+   8. Stop.

# Code: An Example of a Binary Search

```
```cpp
#include<iostream>
using namespace std;
int binarySearch(int array[], int a, int b, int s) {
    if (a <= b) {
        int mid = (a + b)/2;
        if (array[mid] == s)
            return mid;
        if (array[mid] > s)
            return binarySearch(array,a, mid-1, s);
        if (array[mid] < s)
            return binarySearch(array, mid+1, b, s);
    }
    return 0;
}
int main(void) {
    int array[] = {23,67,45,11,33,44,55};
    int size = sizeof(array)/sizeof(array[0]);
    int s;
    cout << "Enter the element to search: \n";
    cin >> s;
    int flag = binarySearch (array, 0, size-1, s);
    if(flag){
        cout<< s <<" found at index "<< flag <<"\n";
    }else{
        cout<< s <<" is not in the array sorry!";
    }
```

```