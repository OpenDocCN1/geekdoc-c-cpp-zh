
# 148 Introduction to C++

```cpp
if(found == 0)
{
    code[pos] = num;
    pos++;
}
cout << "\nCodes: ";
for(i = 0; i < pos; i++)
    cout << code[i] << '\n';
return 0;
```

**C.7.8** Write a program that reads 100 integers and stores them in an array. Then, the program should find and display the two higher different values.

```cpp
#include <iostream>
using std::cout;
using std::cin;

int main()
{
    const int SIZE = 100;
    int i, max_1, max_2, arr[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        cout << "\nEnter number: ";
        cin >> arr[i];
    }
    max_1 = max_2 = arr[0];
    for(i = 1; i < SIZE; i++)
    {
        if(max_1 != arr[i])
        {
            max_2 = arr[i]; /* We assign that value to max_2, to compare it with the remaining elements. */
            break;
        }
    }
    if(i == SIZE)
    {
        cout << "\Array contains the same value: " << max_1 << '\n';
        return 0;
    }
    /* Continue with the loop execution from the point the second loop ended. */
    for(i = i; i < SIZE; i++)
    {
        if(arr[i] > max_1)
        {
            max_2 = max_1; /* The second higher value becomes the highest so far. */
            max_1 = arr[i];
        }
        else if(arr[i] > max_2 && arr[i] != max_1) /* Search for the
        second higher value that is not equal to the first one. */
            max_2 = arr[i];
        }
    }
    cout << "First Max: " << max_1 << " Sec Max: " << max_2 << '\n';
    return 0;
}
```

Comments: The typical approach to find the n-th minimum or maximum element of an array is to sort the array by some sorting algorithm, like the ones presented in Chapter 12. Then, the element are searching for the arr[n-1].

**C.7.9** Write a program that declares an array of ten integers and assigns values within [5, 20] to its elements. The program should check if the array contains duplicates and, if any, delete them. When an element is deleted, the next elements should be shifted one position to the left. The empty positions should be given the value -1. For example, if the array is: {9, 12, 8, 12, 17, 8, 18, 19} it should become: {9, 12, 8, 17, 18, 19, -1, -1}. To remember how to use srand() and rand() read the example C.6.2.

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
int main() {
    const int SIZE = 10;
    int i, j, k, size, arr[SIZE];

    srand(time(NULL));
    for(i = 0; i < SIZE; i++)
        arr[i] = rand()%16+5;

    size = SIZE;
    for(i = 0; i < size; i++) {
        j = i+1;
        while(j < size) {
            if(arr[i] == arr[j] && k < size-1, k++) {
                for(k = j; k < size-1; k++)
                    arr[k] = arr[k+1]; /* Shift the elements
                position to the left. */
                size--; /* decrement their number. /* Since the element is deleted, we
            }
            else {
                j++;
            }
        }
    }
    for(i = size; i < SIZE; i++)
        arr[i] = -1;
    for(i = 0; i < SIZE; i++)
        std::cout << arr[i] << ' ';
    return 0;
}
```

**C.7.10** Write a program that reads the order of preference for that 100 tourists answered the question:
“What did you enjoy the most in Greece?”

- 1. The natural diversity
2. The climate
3. The islands
4. The night life
5. The monuments
6. The people
7. The food

Each answer takes 1–7 points according to its rank order. The first answer takes 7 points, the second one takes 6 points, and the last one takes 1 point. For example, if two tourists answered the following, the program should display:

| 1ST TOURIST | 2ND TOURIST | PROGRAM OUTPUT |
|---|---|---|
| 5 (7p.) | 3 (3p.) | Answer_1 gets 6 points |
| 4 (6p.) | 7 (6p.) | Answer_2 gets 8 points |
| 6 (5p.) | 2 (5p.) | Answer_3 gets 11 points |
| 3 (4p.) | 1 (4p.) | Answer_4 gets 8 points |
| 2 (3p.) | 5 (3p.) | Answer_5 gets 10 points |
| 1 (2p.) | 4 (2p.) | Answer_6 gets 6 points |
| 7 (1p.) | 6 (1p.) | Answer_7 gets 7 points |

The program should read values in [1, 7] and check if the answer is already given. If it is, the program should display a message and prompt the user to enter a new.

```cpp
#include <iostream>
#include <string>
using std::cout;
using std::cin;

int main() {
    const int ANSWERS = 7;
    int i, j, sel, pnts[ANSWERS] = {0}; /* This array holds points of each answer. For example, pnts[0] holds the points of the first answer, pnts[1] holds the points of the second answer and so on. */
    int given_ans[ANSWERS] = {0}; /* This array is used to check if an answer is given. If an element's value is 1 it means that the respective answer is chosen. For example, if the user chooses the third answer, given_ans[2] becomes 1. */
    for (i = 0; i < ANSWERS; i++) {
        cout << "\nEnter answer for " << i+1 << " :\n";
        memset(given_ans, 0, sizeof(given_ans)); /* The values must be before reading the answers of a new tourist. I don't know memset(), it fills a block of memory with a particular value (e.g., 0). Yes, we could make an iteration instead. */
    }
    for(j = 0; j < ANSWERS; j++) {
        while(1) /* Infinite loop until the user enters a valid, not already given. */
        cout << "Answer_" << j+1 << " [1-" << ANSWERS << "];";
        cin >> sel;
        if(sel < 1 || sel > ANSWERS)
            cout << "Wrong answer...\n";
        else if(given_ans[sel-1] == 1)
            cout << "Error: This answer is already given...\n";
        else
            break;
        pnts[sel-1] += ANSWERS - j; /* For example, if the first choice, then pnts[sel-1] += 7 that is, 7 points are added to the points of the fifth choice. */
        given_ans[sel-1] = 1;
    }
    cout << "\n***** Results *****\n";
    for(i = 0; i < ANSWERS; i++)
        cout << "Answer_" << i+1 << " gets " << pnts[i] << " points\n";

    return 0;
}
```

**C.71** Write a program that simulates an on-line lottery game. Suppose the winning numbers are 10 and their values are within [0, 100]. The program should be written in a way to control the winning numbers. In particular the "cheat" is that 3 of the winning numbers in each lottery should have been drawn in the previous one. The program should ask the user if he wants to play, and if the user answers no, the program terminates. For simplicity, suppose that the same number may appear more than once.

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
using std::cout;
using std::cin;

int main()
{
    const int SIZE = 10;
    int i, pos1, pos2, pos3, ans, arr[SIZE];

    srand(time(NULL));
    // First lottery.
    for(i = 0; i < SIZE; i++)
    {
        arr[i] = rand()%101;
        cout << arr[i] << " ";
    }

    while (1)
    {
        cout << "\nContinue to play? (O:No): ";
        cin >> ans;
        if(ans == 0)
            return 0;
        /* We choose three random positions. The numbers stored in
positions will be "drawn" in the next lottery. */
        pos1 = rand()%SIZE;
        do {
            pos2 = rand()%SIZE;
        } while(pos1 == pos2);

        do {
            pos3 = rand()%SIZE;
        } while(pos1 == pos3) || (pos2 == pos3);

        // Next lottery.
        for(i = 0; i < SIZE; i++)
            if((i == pos1) || (i == pos2) || (i == pos3))
            {
                cout << arr[i] << " "; // Here is the cheat.
                continue;
                arr[i] = rand()%101;
                cout << arr[i] << " ";
            }

    }
    return 0;
}
```

**Comments:** With this simple example of an "unfair" lottery I just wanted to show you that a betting software can be written in a way to manipulate the winning results. Therefore, stay away from betting sites that advertise big profits in on-line lotteries.
