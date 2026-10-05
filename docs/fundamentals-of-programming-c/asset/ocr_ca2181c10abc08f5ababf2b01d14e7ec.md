```
using namespace std;

// Draws a bar n segments long
// using iteration.
void segments1(int n) {
    while (n > 0) {
        cout << "*";
        n--;
    }
    cout << endl;
}

// Draws a bar n segments long
// using recursion.
void segments2(int n) {
    if (n > 0) {
        cout << "*";
        segments2(n - 1);
    } else {
        cout << endl;
    }
}

int main() {
    segments1(3);
    segments1(10);
    segments1(0);
    segments1(5);
    cout << "--------------------" << endl;
    segments2(3);
    segments2(10);
    segments2(0);
    segments2(5);
}
```

The outout of Listing 10.8 (histobar.cpp) shows that the two functions produce the same results:

```
***
********
*****
------
***
********
****
```