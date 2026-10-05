# 12 • Searching and Sorting Arrays 347

Comments: To see how the algorithm works, suppose that the user enters the number 45.

First iteration. The initial value of start is 0 and end is 6, middle becomes (start+end)/2 = 6/2 = 3. Since arr[middle] is 40, less than 45, the next statement to be executed is start = 3+1 = 4.

Second iteration. middle becomes (start+end)/2 = (4+6)/2 = 5. Since arr[middle] is 60, greater than 45, the next statement is end = middle-1 = 4.

Third iteration. middle becomes (start+end)/2 = (4+4)/2 = 4. Since arr[middle] is 50, greater than 45, the next statement is end = middle-1 = 3.

Since start is greater than end, the loop terminates and the function returns -1.

# C.12.4 Write a program that reads an integer within [0, 1000] and uses the binary search algorithm to "guess" that number. The program should make questions to determine if we are searching for less or greater than the maximum of the interval examined. The answer must be given in form of 0 (no) or 1 (yes). The program should display how many tries the number was found.

```
#include <iostream>
using std::cout;
using std::cin;
int main() {
    int x, ans, low, high, middle, times;

    do
    {
        cout << "Enter number in [0, 1000]: ";
        cin >> x;
    } while (x < 0 || x > 0);

    times = 1;
    low = 0;
    high = 1000;
    middle = (high+low)/2;
    while (high >= low)
    {
        cout << "Is " << middle << " the hidden number (0 = No, 1 = Yes)?" ";
        cin >> ans;
        if(ans == 1) {
            cout << "Num " << ans << " is found in " << times << " tries\n";
            return 0;
        }
        times++;
        cout << "Is the hidden number < " << middle << " (0 = No, 1 = Yes)?" ";
        cin >> ans;
        if(ans == 1) {
            high = middle-1;
            middle = (high+low)/2;
        }
    }\}
```