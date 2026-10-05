value of the last one, and so on. If it is not symmetric, the program should check if there is a duplicated value and, if so, it should terminate. If not, the program should display a message that all values are different.

```
#include <iostream>
#include <vector>
using std::cout;
using std::cin;
using std::vector;

int main() {
    bool flag;
    int i, j, size;
    vector<int> v;

    while (1) {
        cout << "Enter number: ";
        cin >> i;
        if(i == -1) {
            break;
        }
        v.push_back(i);
    }
    size = v.size();
    flag = 1;
    for(i = 0; i < size/2; i++) {
        if(v[i] != v[size-1-i]) {
            flag = 0;
            break; /* Since we found out that the vector is symmetric, the loop ends. */
        }
    }
    if(flag) {
        cout << "Symmetric\n";
    } else {
        cout << "Not symmetric with ";
        for(i = 0; i < size; i++) {
            for(j = i+1; j < size; j++) { /* This loop checks if there is another element with the value of v[i]. */
                if(v[i] == v[j]) {
                    cout << "same values\n";
                    return 0; /* Since we found out that two elements have the same value, the program terminates. */
                }
            }
        }
        cout << "different values\n";
    }
    return 0;
}
```

**Comments:** If one wonders what happens if the number of elements is odd, the code is still valid, since the middle element is not compared with any other element.