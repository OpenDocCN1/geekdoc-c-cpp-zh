# 16.3 SORTING WITH LOGGING

```
void print (const vector<int>& a) {
    int n = a.size();
    cout << '{';
    if (n > 0) {
        cout << a[0]; // Print the first element
        for (int i = 1; i < n; i++)
            cout << ', ' << a[i]; // Print the rest
        }
    }
    cout << '}';';
}
```

```
/*
 * Returns true if a < b; otherwise,
 * false
 */
bool less_than(int a, int b) {
    return a < b;
}
```

```
/*
 * Returns true if a > b; otherwise,
 * false
 */
bool greater_than(int a, int b) {
    return a > b;
}
```

```
int main() {
    // Make a vector of integers from an array
    vector<int> original = (23, -3, 4, 215, 0, -3, 2, 100, 88, -10);

    // Make a working copy of the original vector
    vector<int> working = original;
    cout << "Before: ";
    print(working);
    cout << endl;
    // Compare using lt (less_than), gt (greater_than)
    selection_sort(working, lt);
    cout << "Ascending: ";
    print(working);
    cout << " (" << lt.comparisons() << " comparisons, " \
          << lt.swaps() << " swaps") << endl;
    
    cout << "--------------------------------------------------------------------" << endl;
    
    // Make another copy of the original vector
    working = original;
    cout << "Before: ";
    print(working);
    cout << endl;
    selection_sort(working, gt);
    cout << "Descending: ";
    print(working);
    cout << " (" << gt.comparisons() << " comparisons, " \
          << gt.swaps() << " swaps") << endl;
    return 0;
}
```